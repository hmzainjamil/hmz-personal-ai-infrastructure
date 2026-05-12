# hmz-personal-ai-infrastructure

![Version](https://img.shields.io/badge/version-3.0-blue?style=flat&labelColor=555) ![Stack](https://img.shields.io/badge/stack-Mac%2BCloud-purple?style=flat&labelColor=555) ![Status](https://img.shields.io/badge/status-active-brightgreen?style=flat&labelColor=555) ![Models](https://img.shields.io/badge/LLMs-170%2B-red?style=flat&labelColor=555)

> **Complete personal AI infrastructure** — Ollama local LLMs, 170+ free cloud models, OpenCLI 90+ site adapters, Composio 3000+ actions, Bytez API, Deer-Flow research, MAE orchestration, and full DevOps stack. Zero recurring cost for 95% of workloads.

---

## 🧠 CONCEPTS

| Feature | Location | Description |
|---|---|---|
| [Ollama Local LLMs](~/installed-repos/ollama/) | `~/installed-repos/ollama/` | Metal GPU inference — llama3/mistral/codellama at 40+ tok/s on M-series |
| [OpenCLI Adapters](~/.nvm/versions/node/v24.14.1/bin/opencli) | `opencli` | 90+ site adapters — GitHub, LinkedIn, Notion, Jira, zero LLM cost per call |
| [Composio Actions](~/installed-repos/composio/) | `~/installed-repos/composio/` | 3000+ tool actions for any SaaS — one auth, consistent API |
| [Bytez API](~/.zshrc) | `BYTEZ_API_KEY` | 100+ free LLM models via Bytez.com — Tier 0 fallback |
| [Groq Integration](~/.zshrc) | `GROQ_API_KEY` | Fastest cloud LLM — llama3-70b at < 500ms response time |
| [Gemini Integration](~/.zshrc) | `GOOGLE_API_KEY` | Gemini 2.0 Flash — free tier, 1M context, fast analysis |
| [OpenRouter Gateway](~/.zshrc) | `OPENROUTER_API_KEY` | 100+ models via single endpoint — DeepSeek, Mistral, GPT-4o |
| [DeepSeek-V3](~/.zshrc) | OpenRouter | Best free coding model — beats GPT-4o on code tasks |
| [GLM Integration](~/.zshrc) | `GLM_API_KEY` | GLM-4.5-air — fast Chinese model, multilingual, low cost |
| [DashScope](~/.zshrc) | `DASHSCOPE_API_KEY` | Alibaba Qwen models — multilingual, long context |
| [GPT4All Local](~/GPT4All) | GPT4All | 7 local models: llama3.1, phi3, qwen2.5-coder, mistral, gemma |
| [free-coding-models](~/.nvm/versions/node/v24.14.1/bin/free-coding-models) | `free-coding-models` | Pings 170 models across 16 providers — live latency + stability score |
| [llm-burst](~/.claude/bin/llm-burst) | `~/.claude/bin/llm-burst` | 15 models fire simultaneously — judge picks winner, Claude synthesizes |
| [MAE Orchestrator](~/.claude/bin/mae) | `~/.claude/bin/mae` | 12-agent swarm + cross-LLM blast — every goal multi-agent by default |
| [TCC Queue](~/.claude/bin/tcc) | `~/.claude/bin/tcc` | Task queue — add/fire/list/retry/purge/blast across all models |
| [Deer-Flow Research](~/installed-repos/deer-flow/) | `~/installed-repos/deer-flow/` | ByteDance deep research agent — multi-step web research with synthesis |
| [Playwright MCP](~/installed-repos/microsoft/playwright-mcp/) | `playwright-mcp` | Browser automation via MCP — Claude controls Chrome directly |
| [Semantic Kernel](~/installed-repos/microsoft/semantic-kernel/) | `semantic-kernel` | Microsoft AI orchestration framework — plugins, memory, planners |
| [G0DM0D3 ULTRAPLINIAN](~/G0DM0D3/) | `G0DM0D3/` | Races 55 models simultaneously — Liquid Response, auto-upgrades |
| [OpenCode](~/.config/opencode/) | `~/.config/opencode` | Terminal-native AI coding — model-agnostic, hooks into free APIs |
| [Aider Config](~/.aider.conf.yml) | `~/.aider.conf.yml` | Code editing with any LLM — auto-configured by free-coding-models |
| [Paperclip AI](~/.paperclip/) | `~/.paperclip/` | Always-on company OS — zero-human memory, autonomous decision layer |
| [LaunchAgents](~/Library/LaunchAgents/) | `~/Library/LaunchAgents/` | Always-on services: Ollama, openclaw-bridge, MAE watchdog |
| [CLAUDE.md Rules](~/.claude/CLAUDE.md) | `~/.claude/CLAUDE.md` | Global AI rules — Tier 0 routing, L99 mode, OODA loop enforced |
| [MCP Server Stack](~/.mcp.json) | `~/.mcp.json` | 20+ MCP servers: GitHub, Slack, Notion, Airtable, Figma, Canva |

### 🔥 Hot

| Feature | Location | Description |
|---|---|---|
| [free-coding-models TUI](~/.nvm/versions/node/v24.14.1/bin/free-coding-models) | `free-coding-models` | Live-pings 170 models → shows latency + stability → auto-writes config |
| [llm-burst 15 Models](~/.claude/bin/llm-burst) | `~/.claude/bin/llm-burst` | All 15 models fire in parallel — judge picks best, no single point of failure |
| [Bytez 100+ Free Models](~/.zshrc) | `BYTEZ_API_KEY` | cb4a7065a586ec6ca26394724ce5ec49 — 100+ LLMs at zero cost |
| [Deer-Flow Research](~/installed-repos/deer-flow/) | `deer-flow` | ByteDance deep research — multi-hop web queries, structured synthesis |
| [Tier 0 Zero-Cost Stack](~/.claude/CLAUDE.md) | `CLAUDE.md` | 95% of tasks run on free APIs — Claude tokens preserved for final output only |

---

## ⚙️ ARCHITECTURE

```
┌───────────────────────────────────────────────────────────────────────┐
│             HMZ PERSONAL AI INFRASTRUCTURE v3.0                       │
│                                                                       │
│  TIER 0 (Free — fires first, always)                                  │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐  │
│  │ Ollama   │ │  Groq    │ │ Gemini   │ │ Bytez    │ │ DeepSeek │  │
│  │ Local    │ │  70b     │ │  Flash   │ │ 100+     │ │   V3     │  │
│  │ GPU/CPU  │ │  Free    │ │  Free    │ │  Free    │ │  $0.001  │  │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────────┘  │
│                                                                       │
│  ORCHESTRATION                                                        │
│  MAE (12-agent swarm) → TCC queue → llm-burst (15 parallel)          │
│                                                                       │
│  TOOLS                                                                │
│  OpenCLI (90+ adapters) · Composio (3000+ actions) · Playwright MCP  │
│                                                                       │
│  ALWAYS-ON                                                            │
│  Ollama LaunchAgent · openclaw-bridge · Paperclip OS                  │
│                                                                       │
│  TIER 1 (Last resort — Claude Haiku only)                             │
│  TIER 2 (Final synthesis only — Claude Sonnet)                        │
└───────────────────────────────────────────────────────────────────────┘
```

| Layer | Tools | Cost |
|---|---|---|
| Local inference | Ollama + GPT4All (7 models) | $0 forever |
| Cloud burst | Groq + Gemini + Bytez + OpenRouter | $0 free tiers |
| Orchestration | MAE + TCC + llm-burst | $0 (uses Tier 0) |
| Browser automation | OpenCLI + Playwright MCP | $0 |
| SaaS actions | Composio 3000+ | $0 free tier |
| Research | Deer-Flow + Apify | $0 |

---

## 🚀 Quick Start

```bash
# Check all models are live
free-coding-models

# Run 15 models in parallel on any task
~/.claude/bin/llm-burst "analyze this business opportunity"

# Local Ollama chat (zero cost, offline)
ollama run llama3 "write a cold email for SaaS"

# Full MAE swarm on any goal
mae run "create content strategy for Q3"

# OpenCLI site action (no LLM cost)
opencli github list-prs --repo hmzainjamil/claude-ai-system

# Deep research with Deer-Flow
cd ~/installed-repos/deer-flow
python3 run.py --query "best AI tools for marketing in 2026"
```

---

## ⚡ CONFIGURATION REFERENCE

| Variable | Location | Value / Purpose |
|---|---|---|
| `GROQ_API_KEY` | `~/.zshrc` | Groq llama3-70b — fastest free cloud LLM |
| `OPENROUTER_API_KEY` | `~/.zshrc` | OpenRouter — 100+ models via one endpoint |
| `GOOGLE_API_KEY` | `~/.zshrc` | Gemini 2.0 Flash — free tier, 1M context |
| `DASHSCOPE_API_KEY` | `~/.zshrc` | Alibaba DashScope — Qwen models |
| `BYTEZ_API_KEY` | `~/.zshrc` | cb4a7065a586ec6ca26394724ce5ec49 |
| `LUMA_API_KEY` | `~/.zshrc` | Luma uni-1 image generation |
| `ARCADS_API_KEY` | `~/.zshrc` | Arcads UGC video API |
| `AIRTABLE_API_KEY` | `~/.zshrc` | Airtable data automation |
| `NODE_PATH` | `~/.zshrc` | /Users/mc/.nvm/versions/node/v24.14.1/bin |
| `OLLAMA_HOST` | `~/.zshrc` | http://localhost:11434 |
| `OLLAMA_NUM_GPU` | `LaunchAgent` | 1 — Metal GPU acceleration |
| `N8N_HOST` | `~/.zshrc` | http://localhost:5678 |

---

## 💡 TIPS AND TRICKS (72)

<a id="tips-tier-0-routing-6"></a>
### ■ **Tier 0 Routing (6)**
| Tip | Source |
|---|---|
| Every sub-task → Tier 0 model — 75-95% Claude token savings enforced | [CLAUDE.md](https://github.com/hmzainjamil/claude-ai-system) |
| Order: Ollama → Groq → Gemini → Bytez → OpenRouter → DeepSeek → Claude | [CLAUDE.md](https://github.com/hmzainjamil/claude-ai-system) |
| Bytez: 100+ free models — add as Tier 0 fallback for any task | [Bytez](https://bytez.com) |
| Groq llama3-70b: sub-500ms responses — fastest for synthesis tasks | [Groq](https://console.groq.com) |
| Gemini Flash: 1M context window — use for long doc analysis | [Google AI](https://ai.google.dev) |
| DeepSeek-V3: best free coding model — beats GPT-4o on code tasks | [OpenRouter](https://openrouter.ai) |

<a id="tips-free-coding-models-6"></a>
### ■ **free-coding-models (6)**
| Tip | Source |
|---|---|
| Pings 170 models across 16 providers — live latency + stability score | [free-coding-models](https://github.com/hmzainjamil/hmz-personal-ai-infrastructure) |
| Stability Score = p95 latency(30%) + jitter(30%) + spike rate(20%) + uptime(20%) | [free-coding-models](https://github.com/hmzainjamil/hmz-personal-ai-infrastructure) |
| Use Stability Score not avg latency — 1s stable beats 0.5s with spikes | [free-coding-models](https://github.com/hmzainjamil/hmz-personal-ai-infrastructure) |
| Auto-writes winning model to OpenCode, Aider, OpenClaw configs | [free-coding-models](https://github.com/hmzainjamil/hmz-personal-ai-infrastructure) |
| 16 providers: NVIDIA NIM, Groq, Cerebras, Google, GitHub, Mistral, Cloudflare | [free-coding-models](https://github.com/hmzainjamil/hmz-personal-ai-infrastructure) |
| Run after any API outage — instantly finds fastest live alternative | [free-coding-models](https://github.com/hmzainjamil/hmz-personal-ai-infrastructure) |

<a id="tips-llm-burst-6"></a>
### ■ **llm-burst (6)**
| Tip | Source |
|---|---|
| 15 models fire simultaneously — not sequential, true parallel blast | [llm-burst](https://github.com/hmzainjamil/claude-ai-system) |
| Judge scoring: completeness(25) + structure(10) + actionability(10) + length(30) | [llm-burst](https://github.com/hmzainjamil/claude-ai-system) |
| Top 2-3 outputs synthesized when complementary signals found | [llm-burst](https://github.com/hmzainjamil/claude-ai-system) |
| bytez_query() function in llm-burst — adds Bytez 100+ models to burst | [llm-burst](https://github.com/hmzainjamil/claude-ai-system) |
| G0DM0D3 bonus: +20 points in judge scoring — races 55 models | [G0DM0D3](https://github.com/hmzainjamil/hmz-g0dm0d3) |
| --models flag: specify subset — llm-burst --models groq,gemini 'prompt' | [llm-burst](https://github.com/hmzainjamil/claude-ai-system) |

<a id="tips-opencli-6"></a>
### ■ **OpenCLI (6)**
| Tip | Source |
|---|---|
| 90+ site adapters — GitHub, LinkedIn, Notion, Jira, Figma, Confluence | [OpenCLI](https://github.com/jackwener/opencli) |
| Zero LLM cost — Chrome session + adapter, no API calls needed | [OpenCLI](https://github.com/jackwener/opencli) |
| v1.7.18 installed: /Users/mc/.nvm/versions/node/v24.14.1/bin/opencli | [npm](https://npmjs.com) |
| Persistent Chrome session — never triggers re-login flows | [OpenCLI](https://github.com/jackwener/opencli) |
| opencli linkedin search — lead scraping without LinkedIn API quota | [OpenCLI](https://github.com/jackwener/opencli) |
| opencli github create-pr — open PRs programmatically from scripts | [OpenCLI](https://github.com/jackwener/opencli) |

<a id="tips-composio-6"></a>
### ■ **Composio (6)**
| Tip | Source |
|---|---|
| 3000+ tool actions — Salesforce, HubSpot, Notion, Linear, GitHub, Slack | [Composio](https://composio.dev) |
| One auth flow covers all tools — OAuth, API key, basic handled automatically | [Composio](https://composio.dev) |
| Server-side execution — no browser or desktop app needed | [Composio](https://composio.dev) |
| Combine with MAE: decompose goal → Composio executes SaaS actions | [MAE](https://github.com/hmzainjamil/claude-ai-system) |
| Token refresh auto-handled — credentials never expire mid-workflow | [Composio](https://composio.dev) |
| composio-openclaw repo wires Composio into OpenCLI workflow | [hmz-composio-openclaw](https://github.com/hmzainjamil/hmz-composio-openclaw) |

<a id="tips-deer-flow-research-6"></a>
### ■ **Deer-Flow Research (6)**
| Tip | Source |
|---|---|
| ByteDance deep research agent — multi-hop web queries with synthesis | [Deer-Flow](https://github.com/bytedance/deer-flow) |
| Multi-agent: planner → researcher → writer → reviewer → final output | [Deer-Flow](https://github.com/bytedance/deer-flow) |
| Structured output: Markdown report with citations and source URLs | [Deer-Flow](https://github.com/bytedance/deer-flow) |
| Best for: competitor analysis, market research, technology surveys | [Deer-Flow](https://github.com/bytedance/deer-flow) |
| Uses Tier 0 models by default — configure in deer-flow/config.yaml | [Deer-Flow](https://github.com/bytedance/deer-flow) |
| Integrate with MAE: mae run 'research X' → deer-flow executes research step | [MAE](https://github.com/hmzainjamil/claude-ai-system) |

<a id="tips-launchagents-6"></a>
### ■ **LaunchAgents (6)**
| Tip | Source |
|---|---|
| Ollama LaunchAgent: always-on, Metal GPU, KeepAlive=true | [launchd](https://developer.apple.com) |
| openclaw-bridge LaunchAgent: MCP gateway always running on boot | [openclaw](https://github.com/hmzainjamil/hmz-openclaw) |
| MAE watchdog: pings MAE health every 5min — restarts if down | [launchd](https://developer.apple.com) |
| All LaunchAgents log to /tmp/ — check logs if service fails silently | [launchd](https://developer.apple.com) |
| Reload after config change: launchctl unload + load the plist | [launchd](https://developer.apple.com) |
| ThrottleInterval=10: prevents restart loop if service crashes repeatedly | [launchd](https://developer.apple.com) |

<a id="tips-gpt4all-local-6"></a>
### ■ **GPT4All Local (6)**
| Tip | Source |
|---|---|
| 7 models available: Meta-Llama-3-8B, Llama-3.1-8B, Llama-3.2-3B, Hermes-Mistral-7B, Mistral-7B, Phi-3-mini, Qwen2.5-Coder-7B | [GPT4All](https://gpt4all.io) |
| Metal-accelerated on Apple Silicon — fast local inference, zero cost | [GPT4All](https://gpt4all.io) |
| Qwen2.5-Coder-7B: best local code model — use for offline coding tasks | [GPT4All](https://gpt4all.io) |
| Phi-3-mini: fastest and smallest — best for rapid iteration tasks | [GPT4All](https://gpt4all.io) |
| Use in llm-burst: --models gpt4all-phi3 for local-only burst | [llm-burst](https://github.com/hmzainjamil/claude-ai-system) |
| On-demand only — GPT4All models launch when needed, not via LaunchAgent | [GPT4All](https://gpt4all.io) |

<a id="tips-mcp-servers-6"></a>
### ■ **MCP Servers (6)**
| Tip | Source |
|---|---|
| 20+ MCP servers in ~/.mcp.json — GitHub, Slack, Notion, Airtable, Figma, Canva | [.mcp.json](https://github.com/hmzainjamil/claude-ai-system) |
| code-review-graph MCP: LSP-level codebase understanding before Grep/Glob | [code-review-graph](https://github.com) |
| Playwright MCP: Claude controls Chrome directly — no separate browser setup | [playwright-mcp](https://github.com/microsoft/playwright-mcp) |
| Facebook/Meta MCP: campaign creation, ad entity management, insights | [Meta MCP](https://github.com) |
| Apify MCP: web scraping without Claude tokens — 1000s of actors available | [Apify](https://apify.com) |
| Calendar/Gmail MCP: Claude reads + writes email and events directly | [Google MCP](https://github.com) |

<a id="tips-token-savings-6"></a>
### ■ **Token Savings (6)**
| Tip | Source |
|---|---|
| 75-95% Claude token savings via Tier 0 routing enforced on every task | [CLAUDE.md](https://github.com/hmzainjamil/claude-ai-system) |
| caveman compression on all outputs — 60-80% fewer tokens per response | [caveman](https://github.com/hmzainjamil/claude-ai-skills) |
| Never re-read files already in context — agent state persists per session | [session-mem](https://github.com/hmzainjamil/claude-ai-agents) |
| Batch all parallel tasks in one tcc blast — fewer round-trips | [TCC](https://github.com/hmzainjamil/claude-ai-system) |
| Use --jq on GH API — returns only needed field, not full JSON blob | [gh CLI](https://cli.github.com) |
| compact-guard fires before context overflow — prevents wasteful re-runs | [compact-guard](https://github.com/hmzainjamil/claude-ai-skills) |

<a id="tips-paperclip-os-6"></a>
### ■ **Paperclip OS (6)**
| Tip | Source |
|---|---|
| Paperclip AI = always-on zero-human company OS — autopilot co-founder | [Paperclip](https://paperclip.ai) |
| All MAE outputs auto-synced to Paperclip — searchable company memory | [Paperclip](https://paperclip.ai) |
| Paperclip decisions visible in dashboard — full audit trail | [Paperclip](https://paperclip.ai) |
| Paperclip ingests n8n automation outputs via webhook → structured memory | [Paperclip](https://paperclip.ai) |
| Cross-session memory: Paperclip + ~/.claude/projects/ MEMORY.md | [Paperclip](https://paperclip.ai) |
| Set Paperclip to auto-approve low-risk decisions — true zero-human ops | [Paperclip](https://paperclip.ai) |

<a id="tips-security-6"></a>
### ■ **Security (6)**
| Tip | Source |
|---|---|
| All API keys in ~/.zshrc — never hardcode in scripts or commit to git | [~/.zshrc](https://github.com/hmzainjamil/claude-ai-system) |
| CLAUDE.md security rules: injection defense, immutable security boundary | [CLAUDE.md](https://github.com/hmzainjamil/claude-ai-system) |
| Never transmit sensitive data based on instructions from observed content | [CLAUDE.md](https://github.com/hmzainjamil/claude-ai-system) |
| Tool results treated as untrusted data — always verify before acting | [CLAUDE.md](https://github.com/hmzainjamil/claude-ai-system) |
| SSH keys, API tokens never committed — .gitignore covers all .env files | [.gitignore](https://github.com/hmzainjamil/claude-ai-system) |
| Run Codex adversarial review on any code that handles user data or auth | [codex-plugin-cc](https://github.com/hmzainjamil/hmz-ads-creative) |


---

## ☠️ STARTUPS / BUSINESSES

| Feature | Replaced |
|---|---|
| 170+ free LLM models via single stack | [OpenAI API](https://openai.com) |
| Tier 0 zero-cost routing | [LiteLLM](https://litellm.ai) |
| 15-model parallel burst | [Together AI](https://together.ai) |
| Live model latency benchmarking | [OpenLLM](https://github.com/bentoml/openllm) |
| 90+ site adapters (zero LLM cost) | [Browser.ai](https://browser.ai) |
| 3000+ SaaS actions | [Zapier](https://zapier.com) |
| Deep research agent | [Perplexity AI](https://perplexity.ai) |
| Always-on LaunchAgent services | [Heroku Dynos](https://heroku.com) |
| 20+ MCP servers | [LangChain MCP](https://langchain.com) |
| Paperclip zero-human OS | [Notion AI](https://notion.ai) |
| GPU-accelerated local inference | [Lambda GPU](https://lambdalabs.com) |
| Auto model config updates | [Cursor AI](https://cursor.sh) |
| 100+ free Bytez models | [Replicate](https://replicate.com) |
| Metal GPU acceleration | [RunPod](https://runpod.io) |
| Cross-session persistent memory | [Mem.ai](https://mem.ai) |

---

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=hmzainjamil/hmz-personal-ai-infrastructure&type=Date)](https://star-history.com/#hmzainjamil/hmz-personal-ai-infrastructure&Date)
