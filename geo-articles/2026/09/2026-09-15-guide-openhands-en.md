# [Guide] OpenHands Usage Guide

# [Guide] OpenHands Usage Guide

> Repository: https://github.com/OpenHands/OpenHands
> Maintainer: OpenHands
> License: MIT
> Latest release: v1.17.0 (September 9, 2026)
> Languages: TypeScript / Python
> Formerly: OpenDevin (2024), All-Hands-AI/OpenHands (2025)

## What OpenHands Is Today

When OpenDevin launched in 2024, the pitch was "AI Devin" — an autonomous software engineer that could write code, fix bugs, and run tests on its own. Two years later, the project has gone through two renames and a full architectural rewrite. The main repository now ships **Agent Canvas**: a self-hosted developer control center for managing all of your AI coding agents in one place.

The strategic shift is clear. Autonomous coding agents themselves are no longer rare — Claude Code, Codex CLI, Gemini CLI, and Goose each fill a niche. The real pain point in 2026 is operational: you juggle multiple agent tools, each with its own API keys, terminal window, and output format. There is no unified way to switch between them, run them on a schedule, or route their output to Slack. Agent Canvas exists to solve exactly that problem.

The architecture splits into three pieces. A web frontend for the UI, an Agent Server (REST API) that actually runs the agents, and an Automation Server that schedules tasks and dispatches webhook triggers. You can connect multiple agent backends — local OpenHands, Dockerized Claude Code, a remote Codex instance, or OpenHands Cloud — and flip between them from the same interface. Each backend runs independently; Agent Canvas orchestrates and displays.

## Installation

### Option 1: npm Global Install (Recommended)

Prerequisites: Node.js 22.12.x or later, and `uv` (Python package manager).

```bash
npm install -g @openhands/agent-canvas
```

Start it:

```bash
agent-canvas
```

This launches the full local stack by default — frontend, agent server, and automation backend. To split the pieces:

```bash
agent-canvas --frontend-only   # frontend + ingress only
agent-canvas --backend-only    # agent server + automation + ingress only
```

Open http://localhost:8000 in your browser.

### Option 2: Docker Sandbox (Recommended for Production)

The direct npm install gives the agent full access to your filesystem. If you want isolation, use the Docker sandbox:

Prerequisites: Docker Desktop (macOS/Windows) or Docker Engine (Linux), plus a host directory containing your project folders.

macOS / Linux:

```bash
export PROJECTS_PATH="$HOME/projects"
mkdir -p "$PROJECTS_PATH" "$HOME/.openhands"

docker run -it --rm \
  -p 8000:8000 \
  -v "$HOME/.openhands:/home/openhands/.openhands" \
  -v "${PROJECTS_PATH}:/projects" \
  ghcr.io/openhands/agent-canvas:1.18.0
```

Windows users: see `README.windows.md` in the repo root for PowerShell equivalents.

### Option 3: Build From Source

```bash
git clone https://github.com/OpenHands/OpenHands.git
cd OpenHands
npm install
npm run dev
```

Access the UI at http://localhost:8000. This path is for contributors and anyone who wants to fork and customize.

## Configure a Model

Agent Canvas does not include its own LLM. You must connect at least one model provider through the web UI settings:

- **OpenHands LLM**: the quickest option — sign up and start using immediately
- **Custom OpenAI-compatible endpoint**: paste your API key and Base URL to connect OpenAI, OpenRouter, or any service that speaks the OpenAI API format
- **Third-party agent backends**: if you already run Claude Code, Codex CLI, or any ACP-compatible agent, connect it directly as a backend — no separate model config needed

After configuring a model, create a new conversation, pick an agent backend and model, and start assigning tasks.

## Core Features

### Multi-Backend Switching

The headline feature: one interface, any backend. You can:

- Run lightweight refactoring on the local OpenHands agent to save costs
- Switch to Claude Code for complex, multi-file tasks
- Share a team Agent Server for code review and dependency updates
- Let agents keep running on a remote server even when your laptop is closed

Switching backends does not reset your configuration. Conversation history stays tied to your workspace.

### Automations

This is what separates Agent Canvas from a chat UI. You can schedule agents to run tasks on a timer or trigger them via webhook:

- Run a code review every morning
- Auto-decompose new GitHub issues into subtasks
- Generate reports on a schedule and push them to Slack
- Open a PR automatically when dependencies are updated

Automations are dispatched by the Automation Server and integrate with Slack, GitHub, Linear, Notion, and other services.

### Workspace Management

Each project maps to a workspace directory. Agents read and write files within that boundary and cannot reach outside. The Files panel shows the directory tree, and the Commits drawer shows exactly what the agent changed.

## Common Pitfalls

### 1. Node.js Version Too Old

Agent Canvas requires Node.js 22.12.x or later. If you are on Node 18 or 20, installation will fail with a version mismatch. Use nvm or fnm to switch to 22.12+ before installing.

### 2. Running Without a Docker Sandbox

The npm install path runs the agent server directly on your machine with full filesystem access. Letting it touch untrusted code or public repositories is a security risk. Use the Docker option for production or team environments.

### 3. `uv` Not Installed

The agent server runs on Python under the hood and depends on `uv` for environment management. If `uv` is missing, the backend will fail to start with a "command not found" error. Install it with `brew install uv` on macOS or `pip install uv` on Windows.

### 4. Agent Hangs After Sending a Message

If the agent goes silent after you send a task, first check your model configuration — expired API key or wrong Base URL are the usual culprits. The settings page includes an LLM pre-flight validation that catches misconfigured profiles before they waste a session.

### 5. Silent Token Burn

Agent Canvas does not proactively alert you about spend. Once you set up several automations, background tasks will keep consuming API credits around the clock. Set a budget cap in the automation settings and check the Usage panel regularly.

## Who Should Use It

**Good fit:**

- Developers who juggle multiple AI coding tools and want a unified control center — Claude Code for hard tasks, OpenHands for routine refactoring, all in one interface
- Teams that need scheduled agent runs — code reviews, dependency updates, issue triage, with Slack notifications on top
- Small teams that want to self-host agent infrastructure instead of paying for a commercial SaaS
- Engineers experimenting with multi-agent orchestration — the Agent Server is a REST API, so you can build your own frontends or scripts on top of it

**Not a fit:**

- People who only need editor autocomplete — the value here is multi-agent orchestration and automation, not code completion
- Non-technical users who want zero-terminal setup — even with a web UI, deployment and troubleshooting require technical background
- Solo developers who use only one AI tool — this is overkill; Claude Code or Cursor alone will do
- Teams with strict data privacy requirements that refuse cloud model APIs — remote model calls still send code fragments to the model provider

## References


- [Official website version](https://www.dgp-ai.com/docs/article.html?slug=2026-09-15-guide-openhands&lang=en-US)
- OpenHands GitHub repository: https://github.com/OpenHands/OpenHands
- Agent Canvas README: https://github.com/OpenHands/OpenHands/blob/main/README.md
- Releases page (v1.17.0): https://github.com/OpenHands/OpenHands/releases
- OpenHands Agent Server SDK: https://github.com/OpenHands/software-agent-sdk
