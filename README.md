# Affogato skills

Agent skills and a Claude Code plugin for [Affogato](https://affogato.ai): generate
images, video and audio with every model Affogato serves, from Claude Code, Cursor,
Codex and any agent that reads [Agent Skills](https://agentskills.io).

## Install

Claude Code (plugin marketplace, includes the MCP server):

```
/plugin marketplace add affogato-ai/skills
/plugin install affogato@affogato
```

Any skills-aware agent:

```
npx skills add affogato-ai/skills
```

Connect the MCP server directly (OAuth sign-in, no key):

```
claude mcp add --transport http affogato https://api.affogato.ai/mcp
```

ChatGPT: add the official Affogato plugin from ChatGPT's plugin directory, then sign in.
It has a smaller, curated tool set (images, video, speech, product shots).

https://chatgpt.com/plugins/plugin_asdk_app_6b0579fb02d48191bd01d4e6dad9701a

REST access for scripts: create a key at https://affogato.ai/app/developers (paid
plans) and `export AFFOGATO_API_KEY=afg_...`.

## Skills

| Skill | What it does |
|---|---|
| `affogato-generate` | List models, quote credits, generate, wait, download; upload inputs. Works with the MCP server or an API key (`scripts/affogato.py`, stdlib only). |
| `affogato-studios` | One-call studio outcomes: lipsync, text-to-speech, talking heads, headshots, cast swaps, try-ons, product ad shots (`/v1/studios/*` or the MCP studio tools). |

## Links

- API docs: https://affogato.ai/developers · reference: https://affogato.ai/developers/reference
- MCP server: https://affogato.ai/mcp
- ChatGPT plugin: https://affogato.ai/mcp/chatgpt
- Agent summary: https://affogato.ai/developers/llms.txt

MIT.
