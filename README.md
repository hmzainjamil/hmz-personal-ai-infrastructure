# hmz-personal-ai-infrastructure
Full personal AI stack — local models, cloud burst, LaunchAgent daemons, and Paperclip CEO all running on a single MacBook Pro with intelligent RAM management.

![local](https://img.shields.io/badge/local_models-GPT4All%2BOllama-blue?style=flat&labelColor=555) ![cloud](https://img.shields.io/badge/cloud_burst-8_providers-green?style=flat&labelColor=555) ![daemons](https://img.shields.io/badge/daemons-8_always_on-orange?style=flat&labelColor=555) ![cost](https://img.shields.io/badge/monthly_cost-near_zero-brightgreen?style=flat&labelColor=555)

[Concepts](#-concepts) · [Hot](#-hot) · [Stack](#️-full-stack) · [Tips](#-tips-and-tricks-22) · [Replaced](#️-startups--businesses) · [Stars](#star-history)

---

## 🧠 CONCEPTS

| Feature | Location | Description |
|---------|----------|-------------|
| [**Ollama (local)**](https://github.com/hmzainjamil/hmz-ollama) | `localhost:11434` | Always-on via LaunchAgent — llama3:latest on GPU, 40-60 tok/sec |
| [**GPT4All (local)**](https://gpt4all.io) | Desktop app | 7 models: Meta-Llama-3-8B · Qwen2.5-Coder-7B · Phi-3-mini · Mistral-7B — fully offline |
| [**Groq (cloud burst)**](https://console.groq.com) | API | llama3-70b fastest cloud — free tier, 6K tok/min |
| [**Gemini Flash (cloud)**](https://ai.google.dev) | API | 1,500 free calls/day — primary analysis + summarization model |
| [**DeepSeek-V3 (cloud)**](https://api.deepseek.com) | API | Best reasoning + code — $0.27/1M tokens |
| [**GLM (cloud)**](https://open.bigmodel.cn) | API | glm-4.5, glm-4.5-air, glm-5-turbo — multilingual, cheap |
| [**Gemma4-31B (cloud)**](https://ai.google.dev) | API | gemma-4-31b-it via Google AI and OpenRouter free |
| [**Paperclip CEO**](https://github.com/hmzainjamil/hmz-digiminds-ceo) | `localhost:3100` | Autonomous CEO daemon — 50 agents, 20 goals, 28 KPIs |
| [**G0DM0D3 Routing**](https://github.com/hmzainjamil/hmz-g0dm0d3) | `CLAUDE.md` | Automatic model selection — Tier 0 first, Claude only for final output |

### 🔥 Hot

| Feature | Location | Description |
|---------|----------|-------------|
| [**RAM manager**](~/.claude/bin/auto-troubleshoot) | `auto-troubleshoot` | Checks RAM at session start — skips Ollama burst if <2GB free, warns on pressure |
| [**Dashscope/Wan**](https://dashscope.console.aliyun.com) | API | `wan2.7-image`, `wan2.7-image-pro`, `Qwen3.6` — image gen + Alibaba models now in Tier 0 |
| [**llm-burst parallel**](~/.claude/bin/llm-burst) | `llm-burst` | 8 models simultaneously — total wall-clock time = slowest model (~3s), not sum |

---

## ⚙️ FULL STACK

```
MacBook Pro (M-series, 32GB RAM recommended)
├── LOCAL MODELS (always-on, LaunchAgent)
│   ├── Ollama → llama3:latest (GPU, 40-60 tok/sec)
│   └── GPT4All → 7 models (on-demand, CPU/GPU)
│
├── CLOUD BURST (on demand, Tier 0)
│   ├── Groq (fastest, free tier)
│   ├── Gemini Flash (1,500/day free)
│   ├── DeepSeek-V3 (best quality, cheap)
│   ├── GLM (multilingual, cheap)
│   ├── Gemma4-31B (OpenRouter free)
│   ├── GPT-4o-mini (reliable fallback)
│   └── Kimi/Moonshot (262K context)
│
├── DAEMONS (8 always-on LaunchAgents)
│   ├── Paperclip CEO (port 3100)
│   ├── OpenClaw Gateway
│   ├── Ollama
│   ├── GitHub Portfolio Sync (6:30 AM)
│   └── 4 Paperclip engines (lead/content/kpi/trends)
│
└── CLAUDE CODE (session-based)
    ├── 45 bin scripts
    ├── 13 core skills
    └── G0DM0D3 routing → Tier 0 first
```

| Resource | Allocation | Notes |
|----------|-----------|-------|
| RAM: Ollama | 4-8GB | GPU memory, shared with system |
| RAM: GPT4All | 4-6GB | On-demand only |
| RAM: Paperclip | 200-500MB | Lightweight Node.js server |
| RAM: System | 8-16GB | macOS + Claude Code session |
| Storage: Models | 15-40GB | Ollama model library |
| Monthly cost | ~$5-15 | Cloud API usage only |

---

## 💡 TIPS AND TRICKS (22)

[RAM](#tips-ram) · [Models](#tips-models) · [Daemons](#tips-daemons) · [Cost](#tips-cost) · [Privacy](#tips-priv)

<a id="tips-ram"></a>■ **RAM Management (5)**

| Tip | Source |
|-----|--------|
| `OLLAMA_KEEP_ALIVE=24h` keeps models in GPU memory — eliminates cold start | [Ollama config](../hmz-ollama/) |
| Skip Ollama in llm-burst when RAM < 2GB — `auto-troubleshoot` does this automatically | [RAM rule](CLAUDE.md) |
| GPT4All and Ollama can run simultaneously — different memory pools, no conflict | [Architecture](~/.claude/bin/) |
| Activity Monitor → GPU History shows if Ollama is using GPU or CPU | [macOS monitoring](launchagents/) |
| Quit Chrome/Slack before running heavy local model tasks — they eat RAM fast | [Ops rule](CLAUDE.md) |

<a id="tips-models"></a>■ **Model Selection (5)**

| Tip | Source |
|-----|--------|
| Default routing: general → llama3 · code → CodeLlama · fast → Groq · analysis → Gemini | [G0DM0D3](../hmz-g0dm0d3/) |
| Long docs (>50K tokens) → Kimi k2.5 (262K) or Gemini 1.5 Pro (1M) | [Context routing](../hmz-g0dm0d3/) |
| Private/sensitive data → GPT4All or Ollama only — no network calls | [Privacy rule](CLAUDE.md) |
| `ollama pull deepseek-coder:6.7b` for code tasks when DeepSeek API is down | [Fallback](../hmz-ollama/) |
| Gemma4-31B on OpenRouter is currently free — use before it gets rate-limited | [Cost tip](../hmz-g0dm0d3/) |

<a id="tips-daemons"></a>■ **Daemons (5)**

| Tip | Source |
|-----|--------|
| All 8 daemons verified at session start by `auto-troubleshoot` hook | [auto-troubleshoot](../claude-ai-system/automations/bin/auto-troubleshoot) |
| Daemon logs: `~/Library/Logs/ai.hmz.*.log` — one file per daemon | [Log location](launchagents/) |
| `launchctl list \| grep ai.hmz` — green column = PID (running), `-` = stopped | [Status check](launchagents/) |
| Never `killall` a daemon — use `launchctl stop ai.hmz.<name>` to graceful-stop | [Safe stop](launchagents/) |
| After macOS update: reload all plists with `launchctl unload` then `load` | [Update SOP](launchagents/) |

<a id="tips-cost"></a>■ **Cost (4)**

| Tip | Source |
|-----|--------|
| Full stack monthly cost: ~$5-15 (API overage above free tiers only) | [Cost model](CLAUDE.md) |
| Free tiers: Groq 6K tok/min · Gemini 1,500 calls/day · Gemma4 via OpenRouter | [Free quotas](../hmz-g0dm0d3/) |
| Claude Sonnet at $3/1M tokens — only for final output, not sub-tasks | [Claude pricing](https://anthropic.com) |
| `llm-burst` 8 parallel at $0.01/task vs Claude Sonnet $0.30/task = 30x savings | [Benchmark](../claude-ai-system/automations/bin/llm-burst) |

<a id="tips-priv"></a>■ **Privacy (3)**

| Tip | Source |
|-----|--------|
| Client data always through Ollama or GPT4All — never cloud APIs | [Privacy policy](CLAUDE.md) |
| API keys in LaunchAgent plists, never in code — `EnvironmentVariables` key | [OPSEC](launchagents/) |
| `github-sync` scrubs all tokens before pushing plists to GitHub | [OPSEC](../claude-ai-system/automations/bin/github-sync) |

---

## ☠️ STARTUPS / BUSINESSES

| Feature | Replaced |
|-|-|
| **Local + cloud hybrid routing** | [LangChain](https://langchain.com), [LlamaIndex](https://llamaindex.ai) — cloud-only default |
| **8-model parallel burst** | Single model API integration — one provider's quality ceiling |
| **Zero-cost local inference** | [Replicate](https://replicate.com), [Together AI](https://together.ai) — charge per inference |
| **Always-on daemons** | [RunPod](https://runpod.io), [Lambda Labs](https://lambdalabs.com) — $0.50-2/hr GPU rental |
| **Automatic RAM management** | Manual model loading/unloading |
| **G0DM0D3 automatic routing** | Manually choosing model per task |

---

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=hmzainjamil/hmz-personal-ai-infrastructure&type=Date)](https://star-history.com/#hmzainjamil/hmz-personal-ai-infrastructure&Date)