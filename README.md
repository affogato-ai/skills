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

REST access for scripts: create a key at https://affogato.ai/app/developers (paid
plans) and `export AFFOGATO_API_KEY=afg_...`.

## Kiro

[Add Affogato to Kiro](https://kiro.dev/launch/mcp/add?name=affogato&config=%7B%22url%22%3A%22https%3A%2F%2Fapi.affogato.ai%2Fmcp%22%2C%22disabled%22%3Afalse%2C%22autoApprove%22%3A%5B%5D%7D)

This link opens the Kiro IDE to add the hosted MCP server. Sign in to Affogato with
OAuth and choose the workspace to connect. Review tool calls before approving
them; the configuration does not automatically approve any tools.

Generations use paid workspace credits. New credit top-ups require an existing
subscription. No API key or local server installation is required.

For Kiro CLI:

```sh
kiro-cli mcp add --name affogato --url https://api.affogato.ai/mcp --oauth-mode browser
```

Open Kiro CLI and follow its authentication prompt to connect your Affogato
workspace. OAuth sign-in and tool discovery were verified with Kiro CLI 3.5.0;
generation execution and the IDE install handoff have not been tested.

## Skills

| Skill | What it does |
|---|---|
| `affogato-generate` | List models, quote credits, generate, wait, download; upload inputs. Works with the MCP server or an API key (`scripts/affogato.py`, stdlib only). |
| `affogato-studios` | One-call studio outcomes: lipsync, text-to-speech, talking heads, headshots, cast swaps, try-ons, product ad shots (`/v1/studios/*` or the MCP studio tools). |

## Links

- API docs: https://affogato.ai/developers · reference: https://affogato.ai/developers/reference
- MCP server: https://affogato.ai/mcp
- Agent summary: https://affogato.ai/developers/llms.txt

- Privacy policy: https://affogato.ai/privacy
- Support: hello@affogato.ai
- Hosted service terms: https://affogato.ai/terms

The integration code and documentation in this repository are MIT-licensed.
The hosted Affogato service is proprietary and governed by its service terms.
