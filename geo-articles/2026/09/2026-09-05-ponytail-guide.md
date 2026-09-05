# 【攻略】Ponytail使用指南


# 【攻略】Ponytail使用指南

> 项目地址：https://github.com/DietrichGebert/ponytail
> 作者：Dietrich Gebert
> 许可证：MIT
> 最新版本：v4.8.3（2026年6月24日）
> 语言：JavaScript 55.3% / Python 44.2%

## Ponytail是什么

你团队里一定有这样一个人：长发马尾，椭圆眼镜，在公司待的时间比版本控制系统还长。你给他看50行代码，他什么也不说，用一行替换了它们——而且它就能工作。

Ponytail就是把这个人塞进你的AI编程代理里。

它不是模型，不是IDE插件，也不是独立工具。它是一个**AI Agent技能包（Skill Pack）**，核心哲学只有一句话：**最好的代码是从未写过的代码。**

Ponytail通过一套"6级懒惰阶梯"规则，让AI编程代理在写代码之前先停下来思考：这真的需要写吗？代码库里已经有了吗？标准库能做吗？原生平台支持吗？已安装的依赖能搞定吗？一行能解决吗？只有当以上全部不成立时，才写最小可用的代码。

## 实测效果

Ponytail的作者在真实开源项目（FastAPI + React全栈模板）上用Claude Code做了12个功能任务的对比测试（Haiku 4.5，n=4），结果如下：

| 对比维度 | Ponytail | 无技能基线 | Caveman（简洁提示对照组） | "YAGNI+一行"提示 |
|---|---|---|---|---|
| 代码量 | **-54%** | 基线 | -20% | -33% |
| Token消耗 | **-22%** | 基线 | +7% | -14% |
| 成本 | **-20%** | 基线 | +3% | -21% |
| 耗时 | **-27%** | 基线 | +2% | -30% |
| 安全性 | **100%** | 100% | 100% | 95% |

Ponytail是唯一在所有维度上都有改善的方案，也是唯一在减少代码的同时保持100%安全的方案。在存在"过度构建陷阱"的任务上（如日期选择器从404行减到23行、颜色选择器从287行减到23行），代码量减少可达94%。

关键区别：Ponytail的规则是"懒于解决方案，从不懒于阅读"。它在选择懒惰阶梯之前，会先阅读相关代码、追踪真实数据流。信任边界验证、数据丢失处理、安全性、可访问性永远不在削减范围内。

## 6级懒惰阶梯

Ponytail的核心是在写代码之前，代理停在第一个成立的阶梯上：

```
1. 这需要存在吗？→ 不需要：跳过它（YAGNI）
2. 代码库里已经有了？→ 复用它，不要重写
3. 标准库能做？→ 用标准库
4. 原生平台功能？→ 用原生（如<input type="date">代替日期选择器组件）
5. 已安装的依赖？→ 用已有依赖
6. 一行能搞定？→ 一行
7. 只有到这一步：写最小可用的代码
```

这个阶梯在代理理解问题之后运行，而不是代替理解。它先阅读变更涉及的代码、追踪真实流程，然后才选择阶梯。

## 安装方法

Ponytail支持20+AI编程平台，以下是主流平台的安装方式。

### Claude Code

```bash
/plugin marketplace add DietrichGebert/ponytail
/plugin install ponytail@ponytail
```

注意：需要分两次发送指令才能完成安装。桌面版没有`/plugin`命令，需通过UI安装：Customize → personal plugins旁的+ → Create plugin and add marketplace → Add from repository → 输入仓库URL。

### Codex

```bash
codex plugin marketplace add DietrichGebert/ponytail
codex
```

然后打开`/plugins`，选择Ponytail marketplace并安装。再打开`/hooks`，审查并信任其两个生命周期钩子，然后启动新线程。桌面版安装后重启应用即可。

### GitHub Copilot CLI

```bash
copilot plugin marketplace add DietrichGebert/ponytail
copilot plugin install ponytail@ponytail
```

Copilot CLI按插件名命名空间命令，例如：
```bash
/ponytail:ponytail ultra
/ponytail:ponytail-review
```

### Gemini CLI / Antigravity CLI

```bash
gemini extensions install https://github.com/DietrichGebert/ponytail
```

Google正在将Gemini CLI更名为Antigravity CLI（`agy`二进制），同样的安装方式：
```bash
agy plugin install https://github.com/DietrichGebert/ponytail
```

### Cursor / Windsurf / Cline / Aider / Kiro / Zed

这些平台通过复制规则文件安装。从仓库的对应目录复制：
- Cursor：`.cursor/rules/`
- Windsurf：`.windsurf/rules/`
- Cline：`.clinerules/`
- GitHub Copilot编辑器：`.github/copilot-instructions.md`
- 通用：`AGENTS.md`
- Kiro：`.kiro/steering/ponytail.md`

VS Code搭配Codex扩展时，直接从仓库根目录运行即可读取`AGENTS.md`，无需额外配置。

### 其他平台

- **Pi agent**：`pi install git:github.com/DietrichGebert/ponytail`
- **OpenCode**：在`opencode.json`中添加`{ "plugin": ["@dietrichgebert/ponytail"] }`
- **Hermes Agent**：`hermes plugins install DietrichGebert/ponytail --enable`
- **Devin CLI**：`devin plugins install DietrichGebert/ponytail`
- **OpenClaw**：`clawhub install ponytail`
- **CodeWhale**：零配置，直接从项目根目录读取`AGENTS.md`
- **Swival**：`swival skills add --global https://github.com/DietrichGebert/ponytail`

## 常用命令

安装后，Ponytail在每个会话中默认激活（full模式），提供以下命令：

| 命令 | 功能 |
|---|---|
| `/ponytail [lite\|full\|ultra\|off]` | 设置强度等级或关闭。无参数显示当前等级 |
| `/ponytail-review` | 审查当前diff中的过度工程，返回删除清单 |
| `/ponytail-audit` | 审计整个仓库的过度工程，不限于diff |
| `/ponytail-debt` | 收集你推迟的`ponytail:`快捷方式到账本，避免"以后"变成"永远不" |
| `/ponytail-gain` | 显示实测影响看板（更少代码、更低成本、更快速度） |
| `/ponytail-help` | 命令快速参考 |

命令需要支持技能的宿主（Claude Code、Codex、Devin CLI、OpenCode、Gemini、Pi、Swival、Hermes Agent）。在Codex中通过`@`调用技能（如`@ponytail-review`）。仅指令模式的适配器（Cursor、Windsurf、Cline、Copilot、Kiro、Antigravity）加载始终在线的规则集，但不提供命令。

## 配置

Ponytail不需要配置文件即可工作。可选配置：

- 环境变量`PONYTAIL_DEFAULT_MODE`设置默认等级（`lite`/`full`/`ultra`/`off`）
- 配置文件`~/.config/ponytail/config.json`（Windows为`%APPDATA%\ponytail\config.json`）中的`defaultMode`字段

默认等级为`full`。`ultra`模式用于"代码库对不起你"的极端情况。

## 常见问题

**需要配置文件吗？** 不需要。可选配置仅用于设置默认等级。

**如果我真的需要那个120行的缓存类呢？** 你不需要。坚持要的话他也会写。慢慢地。正确地。一边看着你。

**它能扩展吗？** 你从未写过的代码可以无限扩展。零bug，零CVE，100%正常运行时间。

**为什么叫Ponytail？** 你知道为什么。

## 适合与不适合的用户

**适合：**
- 经常被AI代理生成过度工程代码（多层抽象、不必要的依赖、重复造轮子）困扰的开发者
- 关注AI编码成本和token消耗的团队
- 使用Claude Code、Codex、Copilot CLI等支持技能的AI编程工具的用户
- 喜欢"极简主义"编码哲学的开发者

**不适合：**
- 需要AI生成完整框架或大型架构设计的场景（Ponytail会倾向于最小化，可能不适合从零搭建复杂系统）
- 使用不支持技能/规则文件的AI工具（虽然可以手动复制AGENTS.md，但效果有限）
- 团队编码规范要求详细注释和完整文档的场景（Ponytail的"最少代码"哲学可能与某些规范冲突）

## 卸载

| 宿主 | 命令 |
|---|---|
| Claude Code | `/plugin remove ponytail` |
| Codex | `codex plugin remove ponytail` |
| Devin CLI | `devin plugins remove ponytail` |
| Pi agent | `pi uninstall ponytail` |
| Cursor/Windsurf/Cline等 | 删除复制的规则文件 |

卸载前建议先运行`node scripts/uninstall.js`清理插件目录外的状态文件（模式标记、配置文件、statusLine条目），然后再执行宿主卸载命令。

## 参考来源

- [本文官网版本](https://www.dgp-ai.com/docs/article.html?slug=2026-09-05-ponytail-guide&lang=zh-CN)
- Ponytail GitHub仓库：https://github.com/DietrichGebert/ponytail
- Ponytail README（原始文档）
- 实测基准：benchmarks/results/2026-06-18-agentic.md
