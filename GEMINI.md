# Social publishing with Skryvo

Skryvo writes in the person's own brand voice and publishes through the accounts they connected in
Skryvo. Its tools come from the `skryvo` MCP server. The first call asks the person to sign in to
Skryvo and approve access.

## Start every task by reading the setup

1. Call `list_brands`. With several brands, ask which one the post is for unless the request names it.
   Use the brand marked default when the person says it doesn't matter.
2. Call `list_channels`. Use only channels that serve the chosen brand (`brand_ids` empty means every
   brand). A channel with `needs_reconnect: true` can't post: tell the person to reconnect it in Skryvo
   under Settings › Connected Accounts. A channel of kind `blog` takes articles, not posts. Each channel's
   `can` says what it takes.
3. If the platform they want has no channel, call `list_platforms` and point them to Settings › Connected
   Accounts in Skryvo. Don't schedule to another platform instead.

## Write

- Call `write_post` with the topic and the platforms (up to four per call). The call uses one of the
  person's Skryvo generations for all of them. Left without platforms or pictures, it first returns
  `status: "confirm"` with the settings and the cost; show that, then call again with `confirmed: true`.
- Show every draft in full, labelled by platform, before anything is scheduled.
- If a platform comes back with an `error` (for example, the monthly limit), report it as it is and carry
  on with the others.

## Picture

- `design_picture` designs one picture in the brand's kept look, with a copy sized for each platform, and
  follows the person's own design for that format where they added one. It takes about a minute and uses
  Image Studio credits. Show every picture before scheduling.
- `headline` sets other words on it, `direction` carries what the person wants, and `photo_id` builds it
  around one of the brand's own photos. Reference images are chosen in Skryvo under For this piece.

## Schedule

- Never schedule without the person's clear go-ahead on the exact text, channels and time.
- Pass times as ISO 8601 with the person's time zone offset. Without `at`, the post goes out in about five
  minutes. Skryvo moves a time to its next quarter hour.
- One `schedule_post` call covers every channel. `images`, `{channel_id: image_url}`, gives each channel its
  copy of the picture, and `by_channel` gives a channel its own words, thread, poll, comments or video.
- Whatever `must_choose` names is the person's answer, never yours, such as a TikTok audience
  (`tiktok_privacy`).
- Confirm afterwards with the returned date and time of each post.

## Check and change

- `list_scheduled_posts` shows what is coming up and anything that failed to publish, with the reason.
- `change_post` moves a post or changes its words. `cancel_post` removes one; confirm first, it can't be
  undone. `review_post` records the person's own decision on a team post.

## Articles

- `plan_article` is free; show the plan and its questions, then `write_article` writes it in the background
  and `article_status` reports it. `article_seo` and `improve_article` check and fix it.
- `import_article` brings the person's own article in from text or a public address, free within the plan's
  monthly limit, once they say it is theirs to publish. Every article tool then works on it.
- `publish_article` schedules an article to a `blog` channel or sends it as a draft. An article read from a
  live address goes only as a draft or as an update of that post. `repurpose_article` turns it into posts.

## Learn what works

- `post_results` (7, 30 or 90 days, optionally one brand) gives reach, engagement and clicks per channel,
  the best posting times and the top posts. Say how many days the numbers cover.
- Results arrive about an hour after a post goes live, so a brand-new post shows no numbers yet.
