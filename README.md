<p align="center">
  <img src="https://img.shields.io/badge/HMZ-PERSONAL%20AI%20INFRA-2C3E50?style=for-the-badge&logoColor=white" alt="HMZ Personal AI Infrastructure" height="60">
</p>

<h1 align="center">HMZ Personal AI Infrastructure</h1>

<p align="center">
  <strong>Complete personal AI operating system — LaunchAgents, model routing, memory systems, MCP servers, and skill pipelines for a one-person AI agency</strong>
</p>

<p align="center">
  <a href="https://github.com/hmzainjamil"><img src="https://img.shields.io/badge/By-HMZ-6C3EE8?style=for-the-badge" alt="By HMZ"></a>
  <a href="#components"><img src="https://img.shields.io/badge/LaunchAgents-12-2C3E50?style=for-the-badge" alt="12 LaunchAgents"></a>
  <a href="#"><img src="https://img.shields.io/badge/Models-55%2B-F86606?style=for-the-badge" alt="55+ Models"></a>
  <a href="#"><img src="https://img.shields.io/badge/MCP%20Servers-15%2B-246DFF?style=for-the-badge" alt="15+ MCP Servers"></a>
  <a href="#"><img src="https://img.shields.io/badge/Auto--Sync-Daily-20A34E?style=for-the-badge" alt="Daily Auto-Sync"></a>
</p>

<p align="center">
  <a href="#overview">Overview</a> &bull;
  <a href="#components">Components</a> &bull;
  <a href="#quick-start">Quick Start</a> &bull;
  <a href="#architecture">Architecture</a> &bull;
  <a href="#use-cases">Use Cases</a> &bull;
  <a href="#installation">Installation</a>
</p>

---

## Overview

**HMZ Personal AI Infrastructure** documents the complete personal AI operating system running on a single MacBook — the foundation that makes a one-person AI agency possible. Every component works together to minimize cost, maximize capability, and ensure everything runs autonomously.

The system replaces a $50,000+/year team with:
- **210 specialist AI agents** — available on demand, zero salary
- **55+ AI models** — racing in parallel, best answer wins, 75–95% cheaper than Claude alone
- **8,000+ n8n workflows** — automating every repeatable task
- **12 LaunchAgents** — running critical processes at login and on schedule
- **15+ MCP servers** — giving Claude Code direct API access to every business tool

---

## Components

### Always-On Services (LaunchAgents — start at login)

| Service | LaunchAgent | What it does |
|---|---|---|
| **OpenClaw Gateway** | `ai.openclaw.gateway` | MCP bridge — persistent tool connections |
| **Ollama** | `ai.hmz.ollama` | Local AI server (llama3 on Apple Silicon GPU) |
| **n8n** | `ai.hmz.n8n` | Workflow automation server (port 5678) |
| **Open Design** | `ai.hmz.open-design` | Design server (port 51827) |

### Scheduled Automations (LaunchAgents — cron)

| Service | Schedule | What it does |
|---|---|---|
| **github-sync** | Daily 6:30 AM | Full system → GitHub push, README audit, new repo discovery |

### AI Model Stack (Tier 0 — zero or near-zero cost)

| Model / Provider | Type | When used |
|---|---|---|
| GPT4All (7 models) | Local | Offline tasks, zero cost, always available |
| Ollama llama3 | Local GPU | Fast local inference, Apple Silicon optimized |
| Groq llama3-70b | Cloud free | Fastest cloud inference, free tier |
| Gemini 2.0 Flash | Cloud free | Research, analysis, long docs |
| DeepSeek-V3 | Cloud cheap | Reasoning, complex code |
| Kimi K2.6 | Cloud cheap | 262K context, vision — Opus replacement at 5% cost |
| GLM 4.5 Air | Cloud cheap | Multilingual, fast |
| OpenRouter free | Cloud free | 100+ models, cheapest routing |

### MCP Servers (15+)

| MCP Server | Provides |
|---|---|
| Apify | Web scraping — 25,000+ Actors |
| Apollo | Prospecting, enrichment, sequences |
| Vibe Prospecting | Business data, lead extraction |
| Composio | 250+ app integrations |
| Gmail | Read, send, search emails |
| Google Calendar | Events, scheduling |
| Slack | Channels, messages, search |
| Notion | Pages, databases, blocks |
| Airtable | Records, bases, views |
| Playwright | Browser control |
| GitHub | Repos, PRs, issues, code |
| Cloudflare | DNS, workers, analytics |
| OpenClaw | Unified model routing |
| +3 more | Custom HMZ MCP servers |

---

## Architecture

```
Personal MacBook (Apple Silicon)
│
├── LaunchAgents (always-on background services)
│   ├── OpenClaw Gateway (MCP bridge)
│   ├── Ollama (local AI server)
│   ├── n8n (automation engine)
│   └── github-sync (daily at 6:30 AM)
│
├── Claude Code (primary interface)
│   ├── 45+ Active skills (auto-activation)
│   ├── 210 Specialist agents
│   └── 15+ MCP servers wired in
│
├── Model Routing (Tier 0 → Tier 1 → Tier 2)
│   ├── Tier 0: GPT4All + Ollama (local, zero cost)
│   ├── Tier 1: Groq + Gemini + DeepSeek (cloud free)
│   └── Tier 2: Claude (final synthesis only)
│
├── Automation
│   ├── 8,159 n8n workflows (local server)
│   └── 12 LaunchAgents (scheduled tasks)
│
└── Memory
    ├── Claude persistent memory (~/.claude/projects/)
    ├── session-queue.jsonl (auto-learn queue)
    └── MEMORY.md index (cross-session context)
```

---

## Quick Start

```bash
# Check that all services are running
launchctl list | grep "openclaw\|ollama\|n8n\|github"

# Test model routing
~/.claude/bin/llm-burst "What is the best cold email hook for B2B SaaS?"

# Force GitHub sync
~/.claude/bin/github-sync

# Check local AI
ollama list
curl http://localhost:11434/api/tags

# Check n8n
open http://localhost:5678
```

---

## Use Cases

| Goal | How the infrastructure handles it |
|---|---|
| **Client work with sensitive data** | Ollama local model — data never leaves device |
| **Cost-sensitive sub-tasks** | Groq/Gemini free tier via llm-burst — zero cost |
| **Long document analysis** | Kimi K2.6 (262K context) at 5% of Opus cost |
| **Daily system backup** | github-sync LaunchAgent at 6:30 AM — automatic |
| **App integrations** | Composio MCP — 250+ apps, one connection |
| **Web scraping** | Apify MCP — 25,000+ Actors, no Claude tokens |
| **Workflow automation** | n8n local server — 8,159 templates to import |
| **Offline AI** | GPT4All (7 models) + Ollama — works with no internet |

---

## Installation

```bash
# Clone the infrastructure config
git clone https://github.com/hmzainjamil/hmz-personal-ai-infrastructure.git

# Install Ollama
brew install ollama && ollama pull llama3

# Install n8n
npm install -g n8n

# Install GPT4All
brew install gpt4all

# Install Claude Code
npm install -g @anthropic-ai/claude-code

# Configure environment variables
cat >> ~/.zshrc << EOF
export GITHUB_TOKEN="your-token"
export OPENROUTER_API_KEY="your-key"
export GROQ_API_KEY="your-key"
export GOOGLE_API_KEY="your-key"
export KIMI_API_KEY="your-key"
export AIRTABLE_API_KEY="your-key"
export APIFY_TOKEN="your-token"
EOF

# Install LaunchAgents
cp launchagents/*.plist ~/Library/LaunchAgents/
launchctl load ~/Library/LaunchAgents/ai.hmz.github-portfolio-sync.plist
launchctl load ~/Library/LaunchAgents/ai.openclaw.gateway.plist
```

---

## Resources

- **[claude-ai-system](https://github.com/hmzainjamil/claude-ai-system)** — Full system repo synced by this infrastructure
- **[claude-ai-automations](https://github.com/hmzainjamil/claude-ai-automations)** — Automation scripts
- **[hmz-g0dm0d3](https://github.com/hmzainjamil/hmz-g0dm0d3)** — Model racing system
- **[hmz-ollama](https://github.com/hmzainjamil/hmz-ollama)** — Local AI setup
- **[hmz-composio](https://github.com/hmzainjamil/hmz-composio)** — App integrations

## License

MIT

---

<p align="center">Built by <a href="https://github.com/hmzainjamil">Hafiz Muhammad Zulqarnain</a> &mdash; HMZ AI Agency</p>
<p align="center"><sub>One person. One MacBook. The output of a 10-person team.</sub></p>