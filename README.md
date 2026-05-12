# hmz-personal-ai-infrastructure
Complete personal AI stack — local + cloud models, MCP servers, automation OS, and zero-cost routing.

![models](https://img.shields.io/badge/models-15%2B-blue?style=flat&labelColor=555)
![mcp](https://img.shields.io/badge/MCP_servers-10%2B-orange?style=flat&labelColor=555)
![cost](https://img.shields.io/badge/monthly_cost-%240_local-brightgreen?style=flat&labelColor=555)
![platform](https://img.shields.io/badge/platform-macOS-lightgrey?style=flat&labelColor=555)
![license](https://img.shields.io/badge/license-MIT-blue?style=flat&labelColor=555)

[Concepts](#-concepts) · [Architecture](#️-architecture) · [Tips](#-tips-and-tricks-22) · [Kills](#️-startups--businesses) · [Stars](#star-history)

## 🧠 CONCEPTS

| Feature | Location | Description |
|---------|----------|-------------|
| [**G0DM0D3 Router**](g0dm0d3/) | `g0dm0d3/` | Sovereign AI routing — 15 models, Tier 0 always first, Claude only for final output [![core](https://img.shields.io/badge/role-core-orange?style=flat&labelColor=555)] |
| [**Ollama Local Stack**](ollama/) | `ollama/` | 7 local models on Metal GPU — Llama 3, Mistral, Qwen Coder, Phi-3 |
| [**Claude Code Harness**](claude-system/) | `claude-system/` | 45+ bin scripts, 200+ skills, hooks — full automation OS |
| [**MCP Server Fleet**](mcp/) | `mcp/` | 10+ MCP servers — Gmail, Notion, Airtable, Slack, Google Drive, code-review-graph |
| [**LaunchAgent Daemons**](launchagents/) | `launchagents/` | 12+ always-on daemons — Ollama, CEO loop, portfolio sync, health checks |
| [**n8n Workflows**](n8n/) | `n8n/` | 30+ automation workflows — BDM, content, intel, reporting |
| [**Paperclip CEO**](paperclip/) | `paperclip/` | AI company co-founder — 127.0.0.1:3100, company c5066522 |
| [**Memory System**](memory/) | `memory/` | ~/.claude/projects/memory/ — 4 types: user, feedback, project, reference |
| [**Skill Archive**](skills-archive/) | `skills-archive/` | 200+ domain skills — dormant until needed, gated by skill-router |
| [**GitHub API Layer**](github-api/) | `github-api/` | Contents API for all pushes — no git clone, no symlink conflicts |

### 🔥 Hot

| Feature | Location | Description |
|---------|----------|-------------|
| [**Tier 0 Health Dashboard**](monitoring/tier0-health.sh) | `monitoring/tier0-health.sh` | Shows live status of all 15 models — available/unavailable matrix |
| [**Session Continuity**](continuity/) | `continuity/` | session-queue.jsonl → auto-learn Stop hook → memory files → next session |
| [**OpenClaw Integration**](openclaw/) | `openclaw/` | Open Design MCP at 127.0.0.1:51827 — creative design in Claude Code |

## ⚙️ ARCHITECTURE

```
Personal AI Infrastructure Stack:

  Layer 1: Local Models (zero cost)
    Ollama → Llama3, Mistral, Qwen2.5-Coder, Phi-3

  Layer 2: Cloud Burst (Tier 0)
    Groq → DeepSeek → Gemini → OpenRouter → GLM → Kimi

  Layer 3: Orchestration
    Claude Code + 45 bin scripts + 200+ skills + 12 LaunchAgents

  Layer 4: Automation
    n8n (30+ workflows) + Paperclip CEO + MCP servers

  Layer 5: Memory
    ~/.claude/projects/memory/ + session-queue.jsonl + GitHub repos

  Layer 6: Output (Claude only here)
    Claude Sonnet/Opus — final synthesis, user-facing responses only
```

| Component | Count | Always-On | Cost |
|-----------|-------|-----------|------|
| Local models | 7 | Llama3 + Mistral | $0 |
| Cloud providers | 8 | — (on-demand) | ~$5/mo |
| LaunchAgents | 12+ | Ollama, CEO, OClaw | $0 |
| MCP servers | 10+ | All loaded | $0 |
| n8n workflows | 30+ | Scheduled | $0 (self-hosted) |
| Skills | 200+ | 12 core always-on | $0 |

## 💡 TIPS AND TRICKS (22)

[stack](#tips-stack) · [mcp](#tips-mcp) · [memory](#tips-memory) · [cost](#tips-cost)

<a id="tips-stack"></a>■ **Stack Management (6)**

| Tip | Source |
|-----|--------|
| `auto-troubleshoot` runs on SessionStart — catches broken LaunchAgents before you start | [HMZ](https://github.com/hmzainjamil) |
| `tier0-health` check at session start — shows which models are up before routing | [HMZ](https://github.com/hmzainjamil) |
| All repos use GitHub Contents API — no git clone, no symlink macOS conflicts | [HMZ](https://github.com/hmzainjamil) |
| skill-auto-activate fires on every prompt — zero manual skill management needed | [HMZ](https://github.com/hmzainjamil) |
| `~/.claude/logs/` — centralized logging for all hooks, daemons, scripts | [HMZ](https://github.com/hmzainjamil) |
| `compact-guard` at 70% context — auto-compresses before overflow, never crashes | [HMZ](https://github.com/hmzainjamil) |

<a id="tips-mcp"></a>■ **MCP Server Fleet (5)**

| Tip | Source |
|-----|--------|
| code-review-graph MCP before Grep/Glob — semantic search beats text search for code | [HMZ](https://github.com/hmzainjamil) |
| OpenClaw at 127.0.0.1:51827 — creative design tasks via LaunchAgent KeepAlive | [HMZ](https://github.com/hmzainjamil) |
| Gmail MCP for email sequences — draft without sending, confirm before dispatch | [HMZ](https://github.com/hmzainjamil) |
| Notion MCP for knowledge base — append learnings, never overwrite existing pages | [HMZ](https://github.com/hmzainjamil) |
| Airtable MCP for structured data — client pipeline, KPI tracking, content calendar | [HMZ](https://github.com/hmzainjamil) |

<a id="tips-memory"></a>■ **Memory System (6)**

| Tip | Source |
|-----|--------|
| 4 memory types: user (profile), feedback (corrections), project (status), reference (pointers) | [HMZ](https://github.com/hmzainjamil) |
| MEMORY.md index — 200 line limit, each entry ≤150 chars with file pointer | [HMZ](https://github.com/hmzainjamil) |
| session-queue.jsonl: write learnings during session → auto-learn Stop hook processes | [HMZ](https://github.com/hmzainjamil) |
| Memory files: never save git history, code patterns, debugging solutions — only non-obvious facts | [HMZ](https://github.com/hmzainjamil) |
| Verify memory before acting — files move, functions get renamed, check current state | [HMZ](https://github.com/hmzainjamil) |
| Update stale memories immediately — wrong memory worse than no memory | [HMZ](https://github.com/hmzainjamil) |

<a id="tips-cost"></a>■ **Cost Optimization (5)**

| Tip | Source |
|-----|--------|
| Caveman compression on all sub-task outputs — 60-80% token reduction | [HMZ](https://github.com/hmzainjamil) |
| Tier 0 for 100% of sub-tasks — Claude token consumption near-zero | [HMZ](https://github.com/hmzainjamil) |
| Batch 5+ parallel tool calls in one message — fewer Claude round-trips | [HMZ](https://github.com/hmzainjamil) |
| Ollama local = $0 for 80%+ of tasks — only burst to cloud for capability gaps | [HMZ](https://github.com/hmzainjamil) |
| Target <$10/month total AI spend — track with finance/revenue.js dashboard | [HMZ](https://github.com/hmzainjamil) |

## ☠️ STARTUPS / BUSINESSES

| Feature | Replaced |
|-|-|
| **Full AI Infrastructure** | [OpenAI Platform](https://platform.openai.com), [Anthropic Console](https://console.anthropic.com) — partial dependency only |
| **Local Model Stack** | [Jan.ai](https://jan.ai), [LM Studio](https://lmstudio.ai), [GPT4All](https://nomic.ai/gpt4all) |
| **MCP Server Fleet** | [Zapier](https://zapier.com), [Make.com](https://make.com), [n8n Cloud](https://n8n.io) |
| **Memory System** | [Mem.ai](https://mem.ai), [Rewind AI](https://rewind.ai), [Notion AI](https://notion.so/ai) |
| **Automation OS** | [Superhuman](https://superhuman.com), [Magical](https://magical.com), [TextBlaze](https://blaze.today) |

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=hmzainjamil/hmz-personal-ai-infrastructure&type=Date)](https://star-history.com/#hmzainjamil/hmz-personal-ai-infrastructure&Date)
