# hmz-personal-ai-infrastructure
HMZ's complete personal AI stack — local models, cloud routing, MCP servers, always-on services

![Infrastructure](https://img.shields.io/badge/AI_Stack-Production-6C3EE8?style=flat&labelColor=000) ![Ollama](https://img.shields.io/badge/Ollama-llama3-blue?style=flat&labelColor=555) ![Models](https://img.shields.io/badge/models-GPT4All%7CGemini%7CGroq%7CDeepSeek-orange?style=flat&labelColor=555)

The infrastructure layer powering DigiMinds agency operations.

---

## 🧠 AI MODEL STACK

| Tier | Models | Use Case | Cost |
|------|--------|----------|------|
| Local | Ollama (llama3, mistral), GPT4All (7 models) | Sub-tasks, research, analysis | Free |
| Cloud Tier 0 | Groq, Gemini, DeepSeek-V3, GPT-4o-mini | Fast inference, code gen | Near-zero |
| Cloud Tier 1 | OpenRouter (100+ models) | Dynamic routing | Low |
| Final Layer | Claude Sonnet/Opus | Output synthesis only | Premium |

## ⚙️ ALWAYS-ON SERVICES

| Service | Port | LaunchAgent | Description |
|---------|------|-------------|-------------|
| Paperclip AI | 3100 | `ai.hmz.paperclip` | Agency CEO — task orchestration |
| Ollama | 11434 | permanent | Local LLM inference on GPU |
| OpenClaw Gateway | varies | `ai.openclaw.gateway` | MCP gateway |
| Open Design | 51827 | varies | UI design tools |

## 💡 MCP SERVER ECOSYSTEM

■ **Connected Platforms (always available)**

| MCP Server | Tools | Purpose |
|-----------|-------|---------|
| Gmail | search_threads, create_draft, get_thread | Email management |
| Notion | search, create_pages, update_page | Knowledge base |
| Airtable | list_records, create_records, update | CRM data |
| Apollo | prospect, enrich_lead, sequence_load | Sales intelligence |
| Slack | read_channel, send_message, search | Team communication |
| Apify | call_actor, get_actor_run | Web scraping |
| Google Calendar | list_events, create_event | Scheduling |
| Facebook Ads | get_ad_entities, ads_insights | Campaign management |

## ☠️ WHAT THIS INFRASTRUCTURE REPLACES

| Old Approach | New Stack |
|-------------|-----------|
| Manual research | Groq + Gemini parallel search |
| Expensive Claude calls for sub-tasks | Ollama local inference |
| Fragmented tools | Unified MCP server layer |
| Manual reporting | Paperclip CEO + scheduled agents |

---
Built by [HMZ](https://github.com/hmzainjamil) · [DigiMinds](https://digiminds.org)
