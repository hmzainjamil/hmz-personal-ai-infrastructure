<div align="center">

# 🧠 Personal AI Infrastructure — HMZ System

**Built & maintained by [Hafiz Muhammad Zulqarnain](https://github.com/hmzainjamil)**  
*Senior PPC & Paid Media Specialist | AI Automation Engineer*

[![System](https://img.shields.io/badge/Part_of-claude--ai--system-blue?style=flat-square)](https://github.com/hmzainjamil/claude-ai-system)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

</div>

---

## Overview

Personal AI infrastructure stack — the core configuration, tooling, and orchestration layer that powers the HMZ Claude AI automation system. This repository contains the foundational components used across all 27 repos in the portfolio.

## What's Inside

| Component | Purpose |
|---|---|
| LaunchAgents | macOS background automation daemons (daily sweeps, sync) |
| Shell configs | Optimized `.zshrc`, PATH routing, API key management |
| MCP server configs | Model Context Protocol integrations (Apollo, Vibe, Gmail, etc.) |
| Claude settings | `settings.json` — hooks, permissions, MCP bindings |
| Bin scripts | Core automation scripts (github-sync, skill-on/off, llm-burst) |
| Model routing | Tier-0 model config (Ollama, Groq, DeepSeek, Gemini, GPT4All) |

## Architecture

```
Personal AI Infrastructure
├── LaunchAgents (6 active)
│   ├── ai.hmz.github-portfolio-sync   → 6:30 AM daily GitHub sync
│   ├── ai.hmz.daily-leads             → 7:00 AM elite B2B lead sweep
│   ├── ai.hmz.bdm-morning             → 9:00 AM job board sweep
│   ├── ai.hmz.bdm-evening             → 9:00 PM job board + Reddit
│   ├── ai.hmz.indeed-morning          → Indeed MCP sweep
│   └── ai.hmz.indeed-evening          → Indeed MCP evening sweep
├── MCP Servers (12 integrated)
│   ├── Vibe Prospecting, Apollo, Gmail
│   ├── Airtable, Notion, Slack, Calendar
│   ├── Facebook Ads, Indeed, Apify
│   └── code-review-graph, computer-use
└── Model Tier System
    ├── Tier 0: Ollama + Groq + Gemini + DeepSeek (free/cheap)
    └── Tier 1: Claude Sonnet/Haiku (final synthesis only)
```

## Setup (for cloning to a new machine)

```bash
# 1. Clone all repos
git clone https://github.com/hmzainjamil/claude-ai-system

# 2. Set your API keys in ~/.zshrc
export GITHUB_TOKEN="your_classic_pat"
export GITHUB_USERNAME="your_username"
export GROQ_API_KEY="your_key"
export OPENROUTER_API_KEY="your_key"
export GOOGLE_API_KEY="your_key"
# ... see SECURITY.md for full list

# 3. Restore LaunchAgents
cp automations/launchagents/*.plist ~/Library/LaunchAgents/
launchctl load ~/Library/LaunchAgents/ai.hmz.*.plist

# 4. Install Claude Code
npm install -g @anthropic-ai/claude-code
```

## Daily Automation Schedule

| Time (PKT) | Agent | Output |
|---|---|---|
| 6:30 AM | github-portfolio-sync | All 27 repos auto-committed & pushed |
| 7:00 AM | hmz-daily-leads | 10 elite B2B leads → Excel |
| 9:00 AM | hmz-bdm-morning-sweep | Job board HTML report |
| 9:00 PM | hmz-bdm-evening-sweep | Evening job report + Reddit drafts |

---

**Part of [claude-ai-system](https://github.com/hmzainjamil/claude-ai-system) — auto-updated daily**
