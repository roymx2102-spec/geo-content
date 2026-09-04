# 【攻略】Composio使用指南


# 【攻略】Composio使用指南

让AI Agent真正"动手干活"，最大的障碍往往不是模型不够聪明，而是它没有手——没有能安全调用Gmail、Slack、GitHub、CRM这些外部系统的接口。Composio正是为了解决这个问题而生的开源项目：它给AI Agent提供上千个预授权工具、按用户隔离的会话、认证与触发器，还有一套沙箱。

仓库地址：https://github.com/ComposioHQ/composio
项目所有者：ComposioHQ
许可证：MIT
语言与生态：TypeScript为主，官方提供Python SDK
活跃度：仓库持续高频更新，2026年9月3日仍有CLI新版本发布（@composio/cli@0.4.1-beta.374），是当前Agent工具层里更新最勤的项目之一。

## 它解决什么问题

如果你在Claude、OpenAI Agents或LangChain里接一个"读邮件、回邮件、查CRM"的Agent，传统做法是给模型灌几十个函数定义，自己处理每个平台的OAuth、权限和调用细节。Composio把这些全部抽象掉：你创建一个绑定某个用户的session，session会自己发现、鉴权、执行对应的App工具，模型只需要按工具格式调用即可。每个session绑定一个用户，天然做了多租户隔离，不用自己维护一堆账号凭据。

## 安装

TypeScript：

```bash
npm install @composio/core @composio/openai-agents @openai/agents
```

Python：

```bash
pip install composio composio-openai-agents openai-agents
```

命令行CLI（给Claude Code这类编码Agent在终端里用）：

```bash
curl -fsSL https://composio.dev/install | sh
```

## 快速上手

先到dashboard（https://dashboard.composio.dev/settings）拿一个`COMPOSIO_API_KEY`。以TypeScript + OpenAI Agents为例：

```typescript
import { Composio } from "@composio/core";
import { OpenAIAgentsProvider } from "@composio/openai-agents";
import { Agent, run } from "@openai/agents";

const composio = new Composio({ provider: new OpenAIAgentsProvider() });

// 每个session绑定一个用户
const session = await composio.create("user_123");
const tools = await session.tools();

const agent = new Agent({
  name: "Personal Assistant",
  instructions: "You are a helpful assistant. Use Composio tools to take action.",
  tools,
});

const result = await run(agent, "Summarize my emails from today");
console.log(result.finalOutput);
```

Python版本结构几乎一致：

```python
from composio import Composio
from composio_openai_agents import OpenAIAgentsProvider
from agents import Agent, Runner

composio = Composio(provider=OpenAIAgentsProvider())
session = composio.create(user_id="user_123")
tools = session.tools()

agent = Agent(
    name="Personal Assistant",
    instructions="You are a helpful assistant. Use Composio tools to take action.",
    tools=tools,
)
result = Runner.run_sync(starting_agent=agent, input="Summarize my emails from today")
print(result.final_output)
```

默认情况下session会提供一组"元工具"，在运行时按需发现、鉴权、执行App工具，避免一次性把上百个工具定义塞进上下文。把`session.session_id`存下来，下一轮用`composio.use()`复用即可。

## 接MCP

如果你用的是Claude或Cursor这类支持MCP的客户端，Composio还提供托管MCP端点。创建session时传`mcp: true`，把返回的`session.mcp.url`填进MCP客户端即可，无需写代码。

## 框架适配

Composio通过provider把工具适配成各框架原生工具格式，官方覆盖OpenAI、OpenAI Agents、Anthropic、Claude Agent SDK、Vercel AI SDK、Google GenAI、LangChain、LangGraph、LlamaIndex、Mastra、CrewAI、AutoGen等。TS SDK要求Node 22+，Python SDK支持3.10+。

## 常见坑

第一，API Key要先在dashboard生成，本地环境变量名是`COMPOSIO_API_KEY`，漏配会在创建session时报认证错误。

第二，session和用户是一一对应的，别把多个用户塞进同一个session，否则权限会串。多租户场景务必按用户维度创建session并持久化session_id。

第三，CLI安装后要重开终端并先执行`composio login`，否则`composio search`、`composio execute`无法连接账户。

第四，工具数量多时，尽量用session配置限制toolkit范围，避免把无关工具全量暴露给模型，既能省token也更安全。

## 适合谁、不适合谁

适合：正在做Agent应用、需要快速接入多种外部SaaS工具的开发者；用Claude Code或Cursor想给Agent补充真实工具能力的团队；需要按用户隔离的多租户Agent产品。

不适合：只需要调用一两个API的轻量脚本（直接用官方SDK更省事）；对"所有工具调用必须完全本地自托管、零外部依赖"有硬性要求的环境（Composio的托管服务与鉴权依赖其云侧）；完全没有编程背景、只想套模板的用户。

Composio把Agent工具层的复杂度集中处理，是当前把"模型意图"转成"真实操作"最快的一条路。

## 参考来源

- [本文官网版本](https://www.dgp-ai.com/docs/article.html?slug=2026-09-04-composio-guide&lang=zh-CN)
