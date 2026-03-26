# Daily workflow

## 1. Multi-source research per entity

For every entity in the watch scope, complete all of the following before marking it researched:

### Tier 1 — Official
- Blog posts, product pages, press releases
- GitHub / arXiv / official documentation
- Official social media accounts (X, YouTube channel)

### Tier 2 — Video coverage
- YouTube: search by entity name, check the official channel AND search for recent videos from 3+ independent creators/analysts who cover this space
- For Chinese labs: also check Bilibili
- Look for: reviews, demonstrations, comparisons, tutorials, news coverage

### Tier 3 — Community & social
- Reddit: search the entity name across relevant subs (r/StableDiffusion, r/LocalLLaMA, r/GenerativeAI, r/MachineLearning, etc.)
- X/Twitter: search by entity name and relevant hashtags
- Hacker News, Discord servers if applicable

### Tier 4 — News & analysis
- At least 2 news outlets per high-priority entity: TechCrunch, The Verge, VentureBeat, Ars Technica, SCMP,Reuters, Bloomberg AI, etc.
- Any vertical publications that cover this entity specifically
- Independent benchmarks or comparison posts

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
