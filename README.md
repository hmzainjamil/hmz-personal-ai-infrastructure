# hmz-personal-ai-infrastructure
> Complete personal AI stack — Tier 0 LLMs, agents, tools, LaunchAgents, repos — running on one Mac.

[![repos](https://img.shields.io/badge/repos-149-blue?style=flat&labelColor=555)](~/installed-repos/)
[![llms](https://img.shields.io/badge/LLMs-11--tier0-green?style=flat&labelColor=555)](tier0/)
[![agents](https://img.shields.io/badge/agents-210-orange?style=flat&labelColor=555)](agents/)
[![launchagents](https://img.shields.io/badge/launchagents-12-purple?style=flat&labelColor=555)](launchagents/)
[![license](https://img.shields.io/badge/license-MIT-lightgrey?style=flat&labelColor=555)](LICENSE)

[concepts](#concepts) · [architecture](#architecture) · [tips](#tips) · [startups](#startups) · [star](#star)

---

## 🧠 CONCEPTS <a id="concepts"></a>

| Feature | Location | Description |
|---|---|---|
| [**Tier 0 LLM Stack**](tier0/) | `tier0/` | 11 free/near-free models: Groq, Gemini, DeepSeek, Kimi, GLM, Bytez, Ollama, GPT4All |
| [**149 Installed Repos**](repos/) | `~/installed-repos/` | Cloned repos: Microsoft, Apify, LLM bundles, n8n workflows, ads-creative |
| [**MAE Orchestration**](mae/) | `~/.claude/bin/mae` | 12-agent swarm engine with wave batching and RAM guard |
| [**Free Coding Models**](tools/free-coding-models/) | `tools/` | Real-time pings 170 models across 16 providers — finds fastest free model |
| [**OpenCLI**](tools/opencli/) | `tools/opencli/` | 90+ site adapters: Twitter, Reddit, Bilibili, HackerNews — zero token cost |
| [**Deer Flow**](tools/deer-flow/) | `tools/deer-flow/` | ByteDance deep research pipeline — web search + multi-step synthesis |
| [**Paperclip**](tools/paperclip/) | `tools/paperclip/` | Open-source company OS — agents like employees, org chart, budgets |
| [**Semantic Kernel**](tools/semantic-kernel/) | `~/installed-repos/microsoft/semantic-kernel/` | Microsoft AI orchestration — plugins, memory, planners |

### 🔥 Hot

| Feature | Location | Description |
|---|---|---|
| [**Bytez Integration**](tier0/bytez.md) | `tier0/` | 100+ free models via bytez.com — API key: integrated in llm-burst |
| [**LTX-Video**](tools/ltx-video/) | `tools/ltx-video/` | Lightricks LTX-Video generation model |
| [**Claw Code**](tools/claw-code/) | `tools/claw-code/` | Ultraworkers claw-code agent framework |

---

## ⚙️ ARCHITECTURE <a id="architecture"></a>

```
Personal AI Infrastructure Stack
             │
┌────────────┴──────────────────────────────────┐
│                  TIER 0 LLMs                   │
│  Ollama  Groq  Gemini  DeepSeek  Kimi          │
│  GLM     Bytez GPT4All OpenRouter Dashscope    │
└────────────────────────┬──────────────────────┘
             │
┌────────────┴──────────────────────────────────┐
│               TOOLS & FRAMEWORKS               │
│  MAE · TCC · llm-burst · free-coding-models   │
│  OpenCLI · Paperclip · Semantic Kernel        │
│  Crawlee · Playwright · Apify                  │
└────────────────────────┬──────────────────────┘
             │
┌────────────┴──────────────────────────────────┐
│                149 REPOS                       │
│  ads-creative · microsoft · apify-org          │
│  n8nworkflows · llm-agents-bundle             │
│  openclaw · website-builder · ui-ux-pro-max   │
└───────────────────────────────────────────────┘
```

| Layer | Components | Cost |
|---|---|---|
| LLMs | Ollama + GPT4All (local) + Groq + Gemini + Bytez | $0 |
| LLMs (paid) | Kimi K2.6, DeepSeek-V3, GLM-4.5 | ~$0.001/1k tokens |
| Tools | MAE, TCC, llm-burst, OpenCLI | $0 |
| Infrastructure | LaunchAgents, hooks, plist | $0 |

---

## 💡 TIPS AND TRICKS (16) <a id="tips"></a>

[llm-setup](#tips-llm) · [repo-management](#tips-repo) · [tools](#tips-tools) · [cost](#tips-cost)

<a id="tips-llm"></a>
■ **LLM Setup (4)**

| Tip | Source |
|---|---|
| `source ~/.claude/tier0.env` loads all API keys — run once at session start | [hmzainjamil](https://github.com/hmzainjamil) |
| `~/.claude/bin/tier0-check` verifies all 11 Tier 0 models are responding | [hmzainjamil](https://github.com/hmzainjamil) |
| Bytez: `curl -H "Authorization: Bearer KEY" https://api.bytez.com/models/v2/chat` | [Bytez](https://bytez.com) |
| Groq free tier: 30 req/min, 14,400/day — enough for all sub-tasks without any cost | [Groq](https://groq.com/pricing) |

<a id="tips-repo"></a>
■ **Repo Management (4)**

| Tip | Source |
|---|---|
| 149 repos in `~/installed-repos/` — `ls ~/installed-repos/ | wc -l` shows current count | [hmzainjamil](https://github.com/hmzainjamil) |
| `git clone --depth=1 URL` — depth=1 saves 70-80% disk space vs full clone | [git docs](https://git-scm.com) |
| `auto-github-push` hook auto-uploads new scripts to GitHub on Write — zero manual push | [hmzainjamil](https://github.com/hmzainjamil) |
| Never `git push` to symlink-heavy repos — use GitHub Contents API exclusively | [hmzainjamil](https://github.com/hmzainjamil) |

<a id="tips-tools"></a>
■ **Tools (4)**

| Tip | Source |
|---|---|
| `opencli doctor` verifies browser bridge extension is running before any adapter calls | [jackwener/opencli](https://github.com/jackwener/opencli) |
| `free-coding-models` TUI pings 170 models live — use Stability Score not avg latency | [hmzainjamil](https://github.com/hmzainjamil) |
| Deer Flow: `python3 ~/installed-repos/deer-flow/main.py "research question"` | [ByteDance](https://github.com/bytedance/deer-flow) |
| Crawlee Python: `pip install crawlee` then use `BeautifulSoupCrawler` for AI-ready scraping | [Apify](https://crawlee.dev) |

<a id="tips-cost"></a>
■ **Cost Optimization (4)**

| Tip | Source |
|---|---|
| Bytez + Groq + Gemini Free = 3 high-quality models at $0 — use for 95% of all tasks | [hmzainjamil](https://github.com/hmzainjamil) |
| Claude Sonnet/Opus only for final synthesis of complex multi-step tasks | [Anthropic](https://anthropic.com/pricing) |
| GPT4All on Metal GPU = $0 forever — 7 local models, no internet required | [GPT4All](https://gpt4all.io) |
| `llm-burst` automatically routes to cheapest/fastest model per task via judge scoring | [hmzainjamil](https://github.com/hmzainjamil) |

---

## ☠️ STARTUPS / BUSINESSES <a id="startups"></a>

| Feature | Replaced |
|---|---|
| **Complete AI infrastructure** | [AWS AI Stack](https://aws.amazon.com/machine-learning/), [Azure AI](https://azure.microsoft.com/ai) |
| **11-model Tier 0 LLM routing** | [AWS Bedrock](https://aws.amazon.com/bedrock/), [Azure OpenAI](https://azure.microsoft.com/openai) |
| **149-repo installed library** | [GitHub Copilot workspace](https://github.com/copilot), [Replit](https://replit.com) |
| **Zero-cost LLM inference** | [Replicate](https://replicate.com), [Modal](https://modal.com), [Runpod](https://runpod.io) |
| **OpenCLI 90+ site adapters** | [Browserbase](https://browserbase.com), [Playwright Cloud](https://playwright.dev/), [Apify](https://apify.com) |

---

## Star History <a id="star"></a>

[![Star History Chart](https://api.star-history.com/svg?repos=hmzainjamil/hmz-personal-ai-infrastructure&type=Date)](https://star-history.com/#hmzainjamil/hmz-personal-ai-infrastructure&Date)
