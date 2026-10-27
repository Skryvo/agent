# Installing Skryvo's MCP server

Skryvo is a hosted MCP server. There is nothing to clone, build or run locally.

1. The person needs a Skryvo account (free at https://app.skryvo.ai). Ask them to open
   https://app.skryvo.ai/settings/agents, create an API key and paste it to you. It starts with `sk_skryvo_`.
2. Add this server to the client's MCP settings, with the key in place of `<key>`:

```json
{
  "mcpServers": {
    "skryvo": {
      "type": "streamableHttp",
      "url": "https://api.skryvo.ai/mcp",
      "headers": { "Authorization": "Bearer <key>" }
    }
  }
}
```

   A client that supports OAuth can leave out `headers`; it opens Skryvo's sign-in and consent page instead.
3. Check the connection by calling `list_brands`. It returns the person's brands.

To publish, the person connects their social accounts once in Skryvo under Settings › Connected Accounts;
`list_channels` shows which ones are ready. Always show a draft from `write_post` and get the person's
go-ahead before `schedule_post`.
