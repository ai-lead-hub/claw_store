# Daily workflow

## 1. Multi-source research per entity

For every entity in the watch scope, complete all of the following before marking it researched:

### Tier 1 — Official
- Blog posts, product pages, press releases
- GitHub / arXiv / official documentation
- Official social media accounts (X, YouTube channel)

### Tier 2 — Video coverage
**→ Use browser (profile=user) for all tier-2 research**
- YouTube: navigate to YouTube search, snapshot results, click into relevant videos
  - Search template: `https://www.youtube.com/results?search_query=<entity>+AI+video+2026`
  - Check official channel + 3+ independent creators/analysts
  - Capture: video titles, channel names, upload dates, view counts, descriptions
- For Chinese labs (DeepSeek, MiniMax, Kling, Z.ai, Moonshot, Qwen, Baidu): also check Bilibili
  - Bilibili search: `https://search.bilibili.com/all?keyword=<entity>+AI+video`
- Look for: reviews, demonstrations, comparisons, tutorials, news breakdowns

### Tier 3 — Community & social
**→ Use browser (profile=user) for Reddit and dynamic community pages**
- Reddit: navigate to Reddit search, snapshot post lists, click into relevant threads
  - Search template: `https://www.reddit.com/search/?q=<entity>+AI+video+generation`
  - Check: r/StableDiffusion, r/LocalLLaMA, r/GenerativeAI, r/MachineLearning, r/ComfyUI
  - Capture: post titles, scores, comment counts, top comment context
- X/Twitter: use web_search with entity-specific queries
- Hacker News, Discord if applicable

- X/Twitter: use BROWSER with profile="user" — X loads content dynamically via JS and requires a real browser session with your login
  - Navigate to: https://twitter.com/search?q=<entity>+AI+video&src=typed_query
  - Snapshot results, click into relevant posts
  - If logged in, you can also check your home feed for trending posts about entities
  - X Premium+ can be checked for trending topics

### Tier 4 — News & analysis
- web_search and web_fetch for news articles
- At least 2 news outlets per high-priority entity: TechCrunch, The Verge, VentureBeat, Ars Technica, SCMP, Reuters, Bloomberg AI, etc.

**Browser is mandatory for tiers 2 and 3. web_search/web_fetch alone are not sufficient for those tiers.**

**Rule: three good source tiers are the minimum. Four are preferred. One is never enough.**

## 2. Triage

For each item, decide:
- summarize now
- keep as link-only
- monitor
- ignore for now

## 3. Rank

Rank by:
- creative utility
- startup relevance
- workflow leverage
- proof quality

## 4. Write intake

Write the day’s findings into `intel/daily/YYYY-MM-DD.md`.

Keep notes concise.
Use compact bullets unless an item clearly deserves a fuller summary.

When the intake is likely to be turned into a PDF later:
- keep each item as a coherent block
- avoid one-line orphan bullets under a heading
- avoid separating links far away from the item they belong to
- prefer clean subsection structure that can survive print export without awkward page breaks

## 5. Promote

Promote only strong items into durable folders.

## 6. Prepare for synthesis

Before drafting a user-facing report:
- inspect the previous report if one exists
- remove items that were already covered unless there is a fresh material update
- keep the final report focused on deltas, not repeated landscape context

In the final report:
- include only net-new updates or clearly changed statuses
- end with a sanity-check source list showing what sources were checked
- keep that source list on the last page/last section where possible

Leave enough structure that a later report generator can read the daily file and assemble a more polished summary.
