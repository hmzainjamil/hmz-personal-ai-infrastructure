# hmz-personal-ai-infrastructure — Full Personal AI Infrastructure Stack

> **One person. Apple Silicon. 4 always-on services. 10+ MCP servers. $92-174/month. Operates like a 50-person team.**

---

## Overview

`hmz-personal-ai-infrastructure` documents the complete AI infrastructure stack running on a single MacBook with Apple Silicon. This is not a cloud setup or an enterprise deployment — it's a personal machine running permanent AI services that power a full digital agency operation.

**Monthly cost: $92-174** (vs. $3,000-5,000+ to hire equivalent human capacity)

---

## Hardware Foundation

### MacBook Apple Silicon

| Component | Spec | AI Relevance |
|-----------|------|-------------|
| CPU | Apple M-series | Unified memory architecture for fast inference |
| GPU | Apple Metal GPU | Runs 7 GPT4All models simultaneously |
| RAM | 16-32GB unified | Shared CPU/GPU memory enables local LLMs |
| Storage | 512GB-1TB SSD | Holds all local model weights (100GB+) |
| Network | WiFi 6 + Ethernet | Groq/Gemini latency <500ms |

### Why Apple Silicon for AI

The unified memory architecture means the Metal GPU can access all system RAM. A 16GB MacBook can run Llama 3 70B via Ollama with full Metal GPU acceleration — something impossible on a similarly-priced x86 laptop.

GPT4All specifically optimizes for Metal GPU and runs 7 models simultaneously at 20-50 tokens/second, making local inference genuinely fast enough for production use.

---

## Always-On Services (4 LaunchAgents)

All four services run permanently with `KeepAlive=true`. They start at login, restart if they crash, and never require manual intervention.

### LaunchAgent 1: OpenClaw (AI Gateway)

```
Service: OpenClaw AI routing gateway
Port: 8765
Config: ~/.openclaw/config.json
Log: /tmp/openclaw.log

Function: Routes every AI call to optimal provider.
         Never lets Claude receive a sub-task call.
         Handles fallback when providers are down.
         Caches repeated queries.
         Logs cost per call.

Status check: curl http://localhost:8765/health
```

### LaunchAgent 2: Ollama (Local LLM Server)

```
Service: Ollama local LLM inference server
Port: 11434
Config: ~/.ollama/
Log: /tmp/ollama.log

Function: Serves local language models via OpenAI-compatible API.
         Models: llama3, mistral, codellama, phi3, gemma, deepseek-coder
         All inference is local — no internet required.
         Metal GPU acceleration enabled automatically.

Status check: curl http://localhost:11434/api/tags
```

### LaunchAgent 3: Paperclip (Memory Sync)

```
Service: Paperclip persistent memory manager
Port: 8766
Config: ~/.claude/projects/
Log: /tmp/paperclip.log

Function: Syncs Claude Code memory files to GitHub every 10 minutes.
         Processes session-queue.jsonl from Stop hook.
         Routes each learning to correct memory file.
         Updates MEMORY.md index automatically.
         Backs up to Google Drive daily.

Status check: curl http://localhost:8766/status
```

### LaunchAgent 4: GitHub Sync (Auto-Backup)

```
Service: Git auto-sync for all repos
Schedule: Every 10 minutes
Config: ~/.claude/bin/github-sync
Log: /tmp/github-sync.log

Function: Auto-commits and pushes all local repo changes to GitHub.
         Includes: memory files, skills, config, workflows.
         Never loses work due to machine failure.
         Creates dated snapshot commits.

Status check: cat /tmp/github-sync.log | tail -5
```

---

## Hook System

Claude Code hooks intercept key moments in every session and trigger automated actions.

### Hook 1: UserPromptSubmit

**Fires:** Every time user sends a message

```bash
# ~/.claude/hooks/user-prompt-submit.sh
#!/bin/bash

# 1. Run skill auto-activator
~/.claude/bin/skill-auto-activate "$PROMPT"

# 2. Classify task type for OpenClaw routing
~/.claude/bin/task-classifier "$PROMPT" > /tmp/current-task-type.txt

# 3. Check if G0DM0D3 race should be triggered
~/.claude/bin/godmode-check "$PROMPT"

# 4. Update session cost tracker
~/.claude/bin/cost-tracker start
```

### Hook 2: SessionStart

**Fires:** When a new Claude Code session begins

```bash
# ~/.claude/hooks/session-start.sh
#!/bin/bash

# 1. Load MEMORY.md index into context
cat ~/.claude/projects/-Users-mc/memory/MEMORY.md

# 2. Load critical behavioral rules
~/.claude/bin/load-priority-memory

# 3. Check all LaunchAgents are running
~/.claude/bin/health-check

# 4. Set today's date in context
echo "Today: $(date +%Y-%m-%d)"

# 5. Log session start
echo "$(date -u +%Y-%m-%dT%H:%M:%SZ) session_start" >> ~/.claude/logs/sessions.log
```

### Hook 3: Stop

**Fires:** When a Claude Code session ends

```bash
# ~/.claude/hooks/stop.sh
#!/bin/bash

# 1. Process auto-learn queue
~/.claude/bin/auto-learn-processor ~/.claude/session-queue.jsonl

# 2. Update MEMORY.md index
~/.claude/bin/update-memory-index

# 3. Deactivate all non-core skills
~/.claude/bin/skill-off-all-non-core

# 4. Commit memory changes to GitHub
cd ~/.claude && git add -A && git commit -m "session memory update $(date +%Y%m%d-%H%M)"

# 5. Log session cost
~/.claude/bin/cost-tracker stop
echo "Session cost logged to ~/.openclaw/logs/"
```

---

## MCP Server Stack (10+ Active)

Model Context Protocol servers give Claude Code access to external tools and services.

| MCP Server | Purpose | Always Active |
|-----------|---------|--------------|
| Playwright MCP | Browser automation and control | Yes |
| Composio MCP | 250+ tool integrations | Yes |
| Airtable MCP | Database operations | Yes |
| Notion MCP | Knowledge base access | Yes |
| Google Drive MCP | File storage | Yes |
| Gmail MCP | Email sending and reading | Yes |
| Google Calendar MCP | Scheduling | Yes |
| Slack MCP | Team communication | Yes |
| GitHub MCP | Repo operations | Yes |
| Apify MCP | Web scraping actors | Yes |
| Meta Ads MCP | Facebook/Instagram ad management | On demand |
| Google Ads MCP | Campaign management | On demand |
| code-review-graph | Codebase analysis | On demand |

### MCP Configuration (`~/.claude/mcp.json`)

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@playwright/mcp", "--browser", "chromium"]
    },
    "composio": {
      "command": "composio",
      "args": ["mcp", "serve"]
    },
    "airtable": {
      "command": "npx",
      "args": ["@airtable/mcp-server"],
      "env": {"AIRTABLE_API_KEY": "${AIRTABLE_API_KEY}"}
    },
    "notion": {
      "command": "npx",
      "args": ["@notionhq/notion-mcp-server"],
      "env": {"NOTION_API_KEY": "${NOTION_API_KEY}"}
    },
    "github": {
      "command": "npx",
      "args": ["@github/mcp-server"],
      "env": {"GITHUB_TOKEN": "${GITHUB_TOKEN}"}
    },
    "apify": {
      "command": "npx",
      "args": ["@apify/mcp-server"],
      "env": {"APIFY_TOKEN": "${APIFY_TOKEN}"}
    }
  }
}
```

---

## API Key Stack

Active API integrations and their purpose:

| Service | Key Variable | Tier | Monthly Cost |
|---------|-------------|------|-------------|
| Groq | GROQ_API_KEY | Free | $0 |
| Google Gemini | GOOGLE_API_KEY | Free + paid | $0-20 |
| OpenRouter | OPENROUTER_API_KEY | Pay-per-use | $5-20 |
| DeepSeek | DEEPSEEK_API_KEY | Pay-per-use | $2-10 |
| Dashscope (Qwen) | DASHSCOPE_API_KEY | Pay-per-use | $2-8 |
| Moonshot (Kimi) | MOONSHOT_API_KEY | Pay-per-use | $2-8 |
| OpenAI | OPENAI_API_KEY | Pay-per-use | $5-20 |
| Anthropic | ANTHROPIC_API_KEY | Pay-per-use | $10-40 |
| Luma AI | LUMA_API_KEY | Pay-per-use | $10-30 |
| Airtable | AIRTABLE_API_KEY | Paid plan | $20 |
| Apollo.io | APOLLO_API_KEY | Paid plan | $49-99 |
| GitHub | GITHUB_TOKEN | Free | $0 |
| Apify | APIFY_TOKEN | Pay-per-use | $5-20 |

**Total monthly API spend: ~$92-174**

---

## File System Layout

```
~/
  .claude/
    hooks/                    <- SessionStart, UserPromptSubmit, Stop
    bin/                      <- skill-on, skill-off, skill-search, etc
    projects/
      -Users-mc/
        memory/               <- All persistent memory files
          MEMORY.md           <- Master index
          user/               <- User profiles
          feedback/           <- Behavioral rules (50+ files)
          project/            <- Project contexts (20+ files)
          reference/          <- Reference docs (10+ files)
    skills-archive/           <- 1,000+ skill files by category
    skills/                   <- Currently active skills (symlinked)
    session-queue.jsonl       <- Auto-learn queue (processed by Stop hook)
    logs/                     <- Session logs, cost logs
    
  .openclaw/
    config.json               <- OpenClaw routing configuration
    cache/                    <- Query cache (10,000 entries)
    logs/                     <- Cost logs, routing logs
    skills/                   <- OpenClaw skill routing files
    
  .ollama/
    models/                   <- Local model weights (50-100GB)
    
  installed-repos/
    microsoft/                <- 10 Microsoft repos
    apify/                    <- 25 Apify repos
    n8n-workflows/            <- 8,159 workflow JSONs
    ai-tools/                 <- 20+ AI tool repos
    
  Downloads/                  <- ALL generated files land here
```

---

## Infrastructure Costs vs. Hiring Equivalent

| Capability | Hire | Monthly Cost | AI Infrastructure | Monthly Cost |
|------------|------|-------------|------------------|-------------|
| Performance marketer | $3,000-8,000 | — | OpenClaw + Claude | ~$40 |
| Copywriter | $2,000-5,000 | — | GPT-4o-mini + Groq | ~$10 |
| Web developer | $3,000-8,000 | — | Claude Code + Blink | ~$30 |
| Data analyst | $3,000-6,000 | — | Gemini 1.5 Pro + Sheets | ~$5 |
| BDM / sales | $3,000-8,000 | — | n8n + Claude | ~$20 |
| Project manager | $2,000-5,000 | — | Notion + automation | ~$20 |
| **Team total** | **$16K-40K/mo** | | **AI total** | **$92-174/mo** |
| **Savings** | | | **99%+** | |

---

## Monitoring & Health Checks

```bash
# Check all LaunchAgents
launchctl list | grep hmz

# Check OpenClaw
curl http://localhost:8765/health

# Check Ollama
curl http://localhost:11434/api/tags | jq '.models[].name'

# Check today's cost
openclaw cost --today

# Check memory file count
ls ~/.claude/projects/-Users-mc/memory/**/*.md | wc -l

# Check active skills
~/.claude/bin/skill-list --active

# Full system health report
~/.claude/bin/health-check --full
```

---

## Related Repos

| Repo | Purpose |
|------|---------|
| hmz-ai | Core model routing hierarchy |
| hmz-openclaw | Always-on AI gateway |
| hmz-claude-mem-main | Persistent memory system |
| hmz-composio | 250+ tool integrations |
| hmz-n8n-workflows | 8,159 automation workflows |

---

## License

MIT

---

*One person. One MacBook. One AI infrastructure stack that runs like a 50-person agency.*
