---
name: skryvo-api
description: Write, schedule, list, cancel and measure social media posts through Skryvo's API with a Skryvo API key. Use in agents that run shell commands but have no Skryvo MCP connection (OpenClaw, Hermes, NanoClaw, Paperclip, Grok Bot, scripts) when the person asks to post or schedule for their brand, check what is scheduled, or see how posts performed.
---

# Skryvo through its API

Skryvo writes in the person's brand voice and publishes through the accounts they connected in Skryvo.
Every call needs the person's key in `SKRYVO_API_KEY` (created at
https://app.skryvo.ai/settings/agents → API keys). Never print, log or paste the key.

```bash
API=https://api.skryvo.ai/api/v1/agent
AUTH="Authorization: Bearer $SKRYVO_API_KEY"
```

If `SKRYVO_API_KEY` is empty, ask the person to create a key in Skryvo and save it as a secret or
environment variable named `SKRYVO_API_KEY`. Don't ask them to paste it into the chat.

## Read the setup first

```bash
curl -s -H "$AUTH" "$API/brands"     # {"brands":[{"id","name","is_default"}]}
curl -s -H "$AUTH" "$API/channels"   # {"channels":[{"id","platform","name","brand_ids","kind","needs_reconnect"}]}
```

Use only channels that serve the chosen brand (`brand_ids` empty means every brand). `kind: "blog"`
takes articles, not posts. `needs_reconnect: true` can't post: tell the person to reconnect it in Skryvo
under Settings › Connected Accounts.

## Write (uses one of the person's generations per platform; schedules nothing)

```bash
curl -s -X POST -H "$AUTH" -H "Content-Type: application/json" "$API/drafts" \
  -d '{"topic":"Launch week recap","platforms":["linkedin","bluesky"],"brand_id":"BRAND_ID"}'
# {"topic":..., "posts":[{"platform","text","hashtags","generation_id"} or {"platform","error"}]}
```

Platforms: twitter, linkedin, instagram, facebook, tiktok, bluesky, threads, pinterest, mastodon,
telegram, discord, slack (up to four per call). Show every draft before scheduling.

## Schedule (only after the person approves the exact text, channels and time)

```bash
curl -s -X POST -H "$AUTH" -H "Content-Type: application/json" "$API/posts" \
  -d '{"text":"...","channel_ids":["CHANNEL_ID"],"at":"2026-10-14T09:00:00-04:00","brand_id":"BRAND_ID"}'
```

`at` is ISO 8601 with the person's offset and moves to the next quarter hour; leave it out to post in about
five minutes. Optional `image_url`. TikTok needs
`"tiktok":{"privacy":"SELF_ONLY|MUTUAL_FOLLOW_FRIENDS|FOLLOWER_OF_CREATOR|PUBLIC_TO_EVERYONE"}`, chosen by
the person.

## Check, cancel, measure

```bash
curl -s -H "$AUTH" "$API/posts?days=7"              # scheduled and recent posts; written=false is a planned topic
curl -s -X DELETE -H "$AUTH" "$API/posts/POST_ID"   # cancel before it goes out (confirm first)
curl -s -H "$AUTH" "$API/results?days=30"           # reach, engagement, best times, top posts (7, 30 or 90)
```

Errors come back as `{"detail": "..."}` in plain words; pass them on as they are.
