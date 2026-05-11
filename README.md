# hmz-personal-ai-infrastructure
the full AI stack — one machine, 20+ models, zero idle capacity

![Stack](https://img.shields.io/badge/AI_Stack-Production-6C3EE8?style=flat&labelColor=000) ![Models](https://img.shields.io/badge/models-20%2B-blue?style=flat&labelColor=555) ![Local](https://img.shields.io/badge/local-7_GPU_models-orange?style=flat&labelColor=555) ![Cloud](https://img.shields.io/badge/cloud-13%2B_APIs-green?style=flat&labelColor=555) ![Cost](https://img.shields.io/badge/cost-75--95%25_below_all--Claude-brightgreen?style=flat&labelColor=555)

The complete personal AI infrastructure powering DigiMinds — local GPU inference, cloud API routing, MCP servers, LaunchAgents, autonomous agents, and the cost optimization layer. Everything runs on a single M1 Pro MacBook Pro. Zero idle capacity — every free service is deployed, every local GPU cycle is used.

[Hardware](#hardware) · [Full Stack](#stack) · [Cost Model](#cost) · [Service Map](#services) · [Tips](#tips) · [Gotchas](#gotchas)

## 🧠 ARCHITECTURE

```
┌─────────────────────────────────────────────────────────────┐
│  USER INTERFACE                                              │
│  Claude Code CLI  |  OpenCode Terminal  |  n8n Dashboard    │
├─────────────────────────────────────────────────────────────┤
│  ORCHESTRATION                                               │
│  Paperclip AI (port 3100) — 50 agents, CEO control         │
│  OpenClaw MCP Gateway (port 51827)                          │
├─────────────────────────────────────────────────────────────┤
│  MODEL ROUTING (G0DM0D3 — 3 tier waterfall)                 │
│  Tier 0: Ollama GPU → Groq → Gemini → DeepSeek → Kimi      │
│           → GPT-4o-mini → Mistral → OpenRouter → GLM        │
│  Tier 1: Claude Haiku (last resort)                         │
│  Tier 2: Claude Sonnet (final output only)                  │
├─────────────────────────────────────────────────────────────┤
│  MCP TOOL LAYER                                              │
│  Gmail | Notion | Airtable | Composio (250+ apps)           │
│  GitHub | Slack | Calendar | Apollo | Facebook Ads          │
│  Google Ads | Canva | LinkedIn | Paperclip | Computer Use   │
├─────────────────────────────────────────────────────────────┤
│  DATA & MEMORY                                               │
│  ~/.claude/projects/*/memory/  (persistent cross-session)   │
│  ~/.paperclip/ceo-decisions.log                             │
│  ~/Downloads/ (all generated outputs)                       │
│  ~/.claude/tier0-cache.json (prompt dedup cache)            │
└─────────────────────────────────────────────────────────────┘
```

<a id="hardware"></a>
## ⚙️ HARDWARE

| Component | Spec | AI Role |
|---|---|---|
| CPU | Apple M1 Pro (10-core) | Orchestration, API calls |
| GPU | 16-core Apple GPU | Ollama Metal inference |
| RAM | 16GB unified | Shared CPU+GPU — critical constraint |
| Storage | 512GB SSD | Model storage (~20GB), workflow data |
| Network | WiFi 6 | Cloud API calls, webhooks |

**RAM allocation at full load:**
```
macOS system:          ~4GB
Ollama (2 models hot): ~9.4GB (llama3 + codellama)
Paperclip AI:          ~500MB
OpenClaw:              ~200MB
n8n:                   ~300MB
Chrome (browser):      ~800MB
Available for tasks:   ~800MB
```

**RAM constraint rule:** When <2GB free, `tier0-check` skips Ollama, routes to Groq instead.

<a id="stack"></a>
## 💡 FULL STACK

■ **Always-On Services (LaunchAgents)**

| Service | Port | Process | RAM |
|---|---|---|---|
| Paperclip AI | 3100 | Node.js | ~500MB |
| OpenClaw Gateway | 51827 | Node.js | ~200MB |
| Ollama (GPU inference) | 11434 | Go binary | varies (model-dependent) |
| Open Design | 51827 | Node.js | ~100MB |

■ **Local LLM Models (Ollama)**

| Model | Size on disk | VRAM hot | Speed |
|---|---|---|---|
| llama3:latest | 4.7GB | 4.7GB | 45 t/s |
| llama3.2:3b | 2.0GB | 2.1GB | 85 t/s |
| mistral:7b | 4.1GB | 4.3GB | 42 t/s |
| codellama:7b | 3.8GB | 4.2GB | 40 t/s |
| phi3:mini | 2.2GB | 2.3GB | 70 t/s |
| deepseek-coder:6.7b | 3.8GB | 4.0GB | 38 t/s |

■ **Cloud APIs (Tier 0)**

| Provider | Free Tier | Paid | Models |
|---|---|---|---|
| Groq | 6K req/day | $0.59/1M | llama3-70b, mixtral |
| Gemini | 1500 req/day | $0.075/1M | flash, 1.5-pro |
| DeepSeek | — | $0.27/1M | V3, R1 |
| Moonshot/Kimi | — | low | K2.5 (262K), v1-128k |
| OpenRouter | free models | varies | 100+ models |
| OpenAI | — | $0.15/1M | gpt-4o-mini |
| GLM | free quota | — | glm-4.5, glm-5 |
| Dashscope | — | — | wan2.7-image, Qwen |

■ **MCP Servers (50+ tools)**

| Server | Tools | Auth |
|---|---|---|
| OpenClaw | 7 (routing, skills, memory) | Local |
| Composio | 250+ app connectors | OAuth per app |
| Gmail | read, search, draft, send | OAuth2 |
| Notion | pages, databases, comments | API key |
| Airtable | bases, records, views | API key |
| GitHub | repos, PRs, issues, actions | PAT |
| Slack | channels, messages, search | OAuth2 |
| Calendar | events, scheduling | OAuth2 |
| Apollo | leads, enrichment, sequences | API key |
| Facebook Ads | campaigns, insights | OAuth2 |
| Google Ads | campaigns, keywords, reports | OAuth2 |

<a id="cost"></a>
## 📊 COST MODEL

**Monthly AI spend (before G0DM0D3):** ~$200-400 (all-Claude)
**Monthly AI spend (with G0DM0D3):** ~$15-40 (75-95% reduction)

| Cost Driver | Without Routing | With Tier 0 Routing |
|---|---|---|
| Research tasks (100/day) | $6/day (Claude) | $0.05/day (Groq/Gemini) |
| Code generation (50/day) | $3/day (Claude) | $0.10/day (DeepSeek) |
| Content drafts (20/day) | $1.20/day (Claude) | $0.02/day (GPT-4o-mini) |
| Sub-agent work (200/day) | $12/day (Claude) | $0/day (Ollama) |
| Final synthesis (10/day) | $0.60/day (Claude) | $0.60/day (Claude — same) |
| **Daily total** | **~$22.80** | **~$0.77** |

<a id="services"></a>
## 🔧 SERVICE MANAGEMENT

```bash
# Full health check
launchctl list | grep "ai\." | awk '{print $1"	"$2"	"$3}'

# Service status
curl -s localhost:3100/api/health       # Paperclip
curl -s localhost:11434/api/tags        # Ollama
curl -s localhost:51827/health          # OpenClaw

# Model availability
~/.claude/bin/tier0-check

# RAM usage
sudo memory_pressure
vm_stat | grep "Pages free"

# Full system status (auto-troubleshoot)
~/.claude/bin/auto-troubleshoot
```

<a id="tips"></a>
## 💡 TIPS

| Tip | Note |
|---|---|
| Keep Chrome closed during heavy Ollama inference — Chrome takes 800MB+ that GPU-shared RAM needs | M1 Pro has unified memory — RAM IS VRAM |
| Only load 1 Ollama model at a time when doing large-context tasks (>4K tokens) — VRAM fragmentation | `OLLAMA_MAX_LOADED_MODELS=1` |
| DeepSeek V3 is the best value API for code — $0.27/1M input, outperforms GPT-4o on code benchmarks | First choice for all code generation |
| Keep Paperclip LaunchAgent priority low (`ProcessType=Background`) — avoids thermal pressure | |
| Groq 6K req/day free tier resets midnight UTC = 10AM AEST — plan heavy usage after reset | |
| GPT4All is on-demand only (not LaunchAgent) — `gpt4all-start` script, uses ~500MB RAM when active | |

<a id="gotchas"></a>
## ☠️ GOTCHAS

| Gotcha | Fix |
|---|---|
| Ollama crashes when RAM < 500MB free — other processes starving it | Kill Chrome tabs, reduce OLLAMA_MAX_LOADED_MODELS=1 |
| Paperclip Node.js process leaks memory over 48h — exits code 0 but stops responding | LaunchAgent ThrottleInterval=5 catches and restarts |
| OpenClaw and Open Design both try to use port 51827 — one fails silently | Check which is configured in `.mcp.json` — only one should run |
| Groq rate limits are per-API-key, not per-IP — rotating keys doesn't help | Stay under 6K req/day on free tier |
| DeepSeek API latency spikes during Chinese business hours (9AM-6PM CST = 11PM-8AM AEST) | Pre-schedule DeepSeek tasks for AEST 8AM-11PM |
| `tier0-cache-inject` caches responses by prompt hash — stale responses if data changes | Set TTL = 1h for any task that reads live data |
