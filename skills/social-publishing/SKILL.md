---
name: social-publishing
description: Plan, write, schedule and review social media posts with Skryvo. Use when the person asks to write or schedule posts for their brand, post to LinkedIn, X, Bluesky, Threads, Mastodon, Pinterest, Telegram, Discord, Slack or other connected accounts, see what is scheduled, cancel a post, or learn which posts, channels and times perform best.
---

# Social publishing with Skryvo

Skryvo writes in the person's own brand voice and publishes through the accounts they connected in
Skryvo. Its tools come from the `skryvo` MCP server. The first call asks the person to sign in to
Skryvo and approve access.

## Start every task by reading the setup

1. Call `list_brands`. With several brands, ask which one the post is for unless the request names it.
   Use the brand marked default when the person says it doesn't matter.
2. Call `list_channels`. Use only channels that serve the chosen brand (`brand_ids` empty means every
   brand). A channel with `needs_reconnect: true` can't post: tell the person to reconnect it in Skryvo
   under Settings › Connected Accounts. A channel of kind `blog` takes articles, not posts.
3. If the platform they want has no channel, say so and point them to Settings › Connected Accounts in
   Skryvo, which connects it in a minute. Don't schedule to another platform instead.

## Write

- Call `write_post` with the topic and the platforms (up to four per call). Each platform uses one of the
  person's Skryvo generations, so write only for the platforms they asked for.
- Show every draft in full, labelled by platform, before anything is scheduled. Edit on request; small
  wording changes don't need a new `write_post` call.
- If a platform comes back with an `error` (for example, the monthly limit), report it as it is and carry
  on with the others.

## Schedule

- Never schedule without the person's clear go-ahead on the exact text, channels and time.
- Pass times as ISO 8601 with the person's time zone offset, e.g. `2026-10-14T09:00:00-04:00`. Without
  `at`, the post goes out in about five minutes. Skryvo moves a time to its next quarter hour.
- One `schedule_post` call takes one text for several channels. Different text per platform means one
  call per platform.
- TikTok needs the audience the person chooses (`tiktok_privacy`); always ask, never pick one.
- Confirm afterwards with the returned date and time of each post.

## Check and change

- `list_scheduled_posts` shows what is coming up and anything that failed to publish, with the reason.
- `cancel_post` removes a scheduled post. Confirm which post first; it can't be undone.

## Learn what works

- `post_results` (7, 30 or 90 days, optionally one brand) gives reach, engagement and clicks per channel,
  the best posting times and the top posts. Use it to suggest when to post and which angles to repeat,
  and say how many days the numbers cover.
- Results arrive about an hour after a post goes live, so a brand-new post shows no numbers yet.
