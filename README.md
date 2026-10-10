# Skryvo for AI agents

Write posts in your brand's voice, schedule them to your connected social accounts and blogs, and read how
they performed, from the AI tool you already use. You need a Skryvo account (https://app.skryvo.ai) and, to
publish, accounts connected under Settings › Connected Accounts.

**MCP server:** `https://api.skryvo.ai/mcp` — one link for every user and client, not a secret. Clients
that support OAuth open Skryvo's sign-in and consent page; no key needed.
**API key:** for agents without OAuth, create one at https://app.skryvo.ai/settings/agents and keep it as
the secret `SKRYVO_API_KEY` (or send it as `Authorization: Bearer <key>`).

## Sign in with OAuth (paste the link)

| Agent | Setup |
|---|---|
| Claude (web, desktop, mobile) | Directory: search **Skryvo** in Connectors, or Settings › Connectors › Add custom connector › paste the link |
| Claude Cowork | Cowork › Customize › Connectors › + Add custom connector › paste the link |
| Claude Code | `/plugin marketplace add Skryvo/agent` then `/plugin install skryvo@skryvo` (adds the skill), or `claude mcp add --transport http skryvo https://api.skryvo.ai/mcp` |
| ChatGPT (and OpenAI dots, which share ChatGPT's plugins) | Plugins › Add › **Add custom MCP server** › paste the link |
| Codex | `codex mcp add skryvo --url https://api.skryvo.ai/mcp` |
| Cursor (desktop app) | Cursor Settings › Tools & MCP › New MCP server, or add `mcp.json` from this repo to `.cursor/mcp.json` |
| VS Code (Copilot) | Command Palette › **MCP: Add Server** › HTTP › paste the link |
| Gemini CLI | `gemini extensions install https://github.com/Skryvo/agent` (or `gemini mcp add --transport http skryvo https://api.skryvo.ai/mcp`) |
| Gemini web app | Settings › Connected apps › add a custom app with the link |
| Grok Build | `grok plugin marketplace add Skryvo/agent` then `grok plugin install skryvo --trust` |
| Perplexity Computer | Settings › Connectors › + Custom connector › Remote › paste the link, OAuth |
| Kimi Code | Ask Kimi to add the link to `~/.kimi-code/mcp.json`, then `/mcp-config login skryvo` |
| Muse | Message Muse: "Add my Skryvo connector: https://api.skryvo.ai/mcp — MCP over HTTP with OAuth, send me the sign-in link." |
| Windsurf, Zed, any MCP client | Add the link as a remote (Streamable HTTP) MCP server |

## Connect with an API key

| Agent | Setup |
|---|---|
| Manus, Cue | Add a custom MCP connector: server `https://api.skryvo.ai/mcp`, API key field `Bearer <your key>` |
| OpenClaw, Hermes Agent, NanoClaw, Paperclip, Grok Bot | `npx skills add Skryvo/agent`, then save `SKRYVO_API_KEY` as the agent's secret |
| Scripts, n8n, Make | REST at `https://api.skryvo.ai/api/v1/agent` with `Authorization: Bearer <key>` — see `skills/skryvo-api/SKILL.md` |

## What it can do

List brands and channels, write a post for up to four platforms (uses your plan's generations), schedule
and cancel posts, list what is scheduled, and read results. Details: https://skryvo.ai/agents

## Privacy

Skryvo receives only the requests your agent makes, never the rest of your conversation. Full policy:
https://skryvo.ai/privacy. Disconnect apps or revoke keys any time in Skryvo under Settings › API & agents.

Support: support@skryvo.ai
