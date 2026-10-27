# Skryvo for AI agents

[![Listed on mcpservers.org](https://mcpservers.org/badge.svg)](https://mcpservers.org/servers/skryvo/agent)
[![Skryvo MCP connector](https://glama.ai/mcp/connectors/ai.skryvo/mcp/badges/score.svg)](https://glama.ai/mcp/connectors/ai.skryvo/mcp)
[![Skryvo on ClaudePluginHub](https://www.claudepluginhub.com/badge/skryvo-skryvo)](https://www.claudepluginhub.com/plugins/skryvo-skryvo)

[Skryvo](https://skryvo.ai) writes social posts and articles in your brand's voice, plans them on one calendar
and publishes them to your channels. This repo connects it to the AI tool you already use: ask Claude, ChatGPT,
Cursor or another agent to write a week of posts, check each one, and schedule it. Skryvo shows every post and
waits for your go-ahead before anything is published.

You need a Skryvo account (free plan: https://app.skryvo.ai) and, to publish, accounts connected under
Settings › Connected Accounts. Step-by-step setup for each agent: https://skryvo.ai/agents/

**MCP server:** `https://api.skryvo.ai/mcp` — one link for every user and client, not a secret. Clients
that support OAuth open Skryvo's sign-in and consent page; no key needed.
**API key:** for agents without OAuth, create one at https://app.skryvo.ai/settings/agents and keep it as
the secret `SKRYVO_API_KEY` (or send it as `Authorization: Bearer <key>`).

## Sign in with OAuth (paste the link)

| Agent | Setup |
|---|---|
| [Claude](https://skryvo.ai/agents/claude/) (web, desktop, mobile) | Directory: search **Skryvo** in Connectors, or Settings › Connectors › Add custom connector › paste the link |
| [Claude Cowork](https://skryvo.ai/agents/claude-cowork/) | Cowork › Customize › Connectors › + Add custom connector › paste the link |
| [Claude Code](https://skryvo.ai/agents/claude-code/) | `/plugin marketplace add Skryvo/agent` then `/plugin install skryvo@skryvo` (adds the skill), or `claude mcp add --transport http skryvo https://api.skryvo.ai/mcp` |
| [ChatGPT](https://skryvo.ai/agents/chatgpt/) (and OpenAI dots, which share ChatGPT's plugins) | Plugins › Add › **Add custom MCP server** › paste the link |
| [Codex](https://skryvo.ai/agents/codex/) | `codex mcp add skryvo --url https://api.skryvo.ai/mcp`, then `codex mcp login skryvo`. [Guide](https://skryvo.ai/blog/codex-mcp/) |
| [Cursor](https://skryvo.ai/agents/cursor/) (desktop app) | Add `mcp.json` from this repo to `~/.cursor/mcp.json` (or a project's `.cursor/mcp.json`), then switch Skryvo on under Customize. [Guide](https://skryvo.ai/blog/cursor-mcp/) |
| [VS Code](https://skryvo.ai/agents/vscode/) (Copilot) | Command Palette › **MCP: Add Server** › HTTP › paste the link, save to the global config (`~/.copilot/mcp-config.json`); or `code --add-mcp '{"name":"skryvo","type":"http","url":"https://api.skryvo.ai/mcp"}'`. [Guide](https://skryvo.ai/blog/vscode-mcp/) |
| [Antigravity CLI](https://skryvo.ai/agents/gemini/) (`agy`, replaced Gemini CLI for individual plans on 2026-06-18) | Add `"skryvo": { "serverUrl": "https://api.skryvo.ai/mcp" }` under `mcpServers` in `~/.gemini/config/mcp_config.json`, then `/mcp` to sign in. [Guide](https://skryvo.ai/blog/gemini-cli-mcp/) |
| [Gemini CLI](https://skryvo.ai/agents/gemini/) (Code Assist Standard/Enterprise, paid API keys) | `gemini extensions install https://github.com/Skryvo/agent` (or `gemini mcp add --transport http skryvo https://api.skryvo.ai/mcp`) |
| Gemini web app | Settings › Connected apps › add a custom app with the link |
| Grok Build | `grok plugin marketplace add Skryvo/agent` then `grok plugin install skryvo --trust` |
| [Perplexity Computer](https://skryvo.ai/agents/perplexity/) | Plugins › Add custom › Connector › Add MCP connector › Remote › paste the link, OAuth. [Guide](https://skryvo.ai/blog/perplexity-mcp/) |
| Kimi Code | Ask Kimi to add the link to `~/.kimi-code/mcp.json`, then `/mcp-config login skryvo` |
| Muse | Message Muse: "Add my Skryvo connector: https://api.skryvo.ai/mcp — MCP over HTTP with OAuth, send me the sign-in link." |
| [Windsurf](https://skryvo.ai/agents/windsurf/), Zed, any MCP client | Add the link as a remote (Streamable HTTP) MCP server |

## Connect with an API key

| Agent | Setup |
|---|---|
| Manus, Cue | Add a custom MCP connector: server `https://api.skryvo.ai/mcp`, API key field `Bearer <your key>` |
| OpenClaw, Hermes Agent, NanoClaw, Paperclip, Grok Bot | `npx skills add Skryvo/agent`, then save `SKRYVO_API_KEY` as the agent's secret |
| [Scripts, n8n, Make](https://skryvo.ai/agents/api/) | REST at `https://api.skryvo.ai/api/v1/agent` with `Authorization: Bearer <key>` — see `skills/skryvo-api/SKILL.md` |

## What it can do

List brands and channels, write a post for up to four platforms (uses your plan's generations), schedule
and cancel posts, list what is scheduled, and read results. Details: https://skryvo.ai/agents/

## Where it publishes

Live: LinkedIn, X, Bluesky, Mastodon, Pinterest, Telegram, Discord, Slack, WordPress, WordPress.com and Dev.to.
Built and waiting for platform review: LinkedIn Pages, Facebook Pages, Instagram, Threads and TikTok (photo
posts). What each channel supports and its limits: https://skryvo.ai/channels/

Channel guides for agents: [LinkedIn MCP](https://skryvo.ai/mcp/linkedin/), [X MCP](https://skryvo.ai/mcp/x/),
[WordPress MCP](https://skryvo.ai/mcp/wordpress/), [Discord MCP](https://skryvo.ai/mcp/discord/),
[Telegram MCP](https://skryvo.ai/mcp/telegram/).

## Plans

Free, Hobby, Pro and Enterprise; scheduling starts on Hobby. Limits and prices: https://skryvo.ai/pricing/

## Privacy

Skryvo receives only the requests your agent makes, never the rest of your conversation. Full policy:
https://skryvo.ai/privacy/. Disconnect apps or revoke keys any time in Skryvo under Settings › API & agents.

Support: support@skryvo.ai
