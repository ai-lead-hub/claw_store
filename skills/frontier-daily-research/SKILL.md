---
name: frontier-daily-research
description: Daily frontier and ecosystem intelligence collection for an AI filmmaking startup. Use when asked to run daily AI research, collect frontier lab/tool/research/community updates, maintain the intel knowledge base, populate `intel/daily/` notes, triage importance, or prepare inputs for every-other-day / weekly reports. Also use for recurring daily research jobs and for promoting important findings into urgent, workflow, paper, entity, or experiment notes.
---

# Frontier Daily Research

Run a disciplined daily intake pass for the AI filmmaking research OS.

## Core workflow

1. Read `references/watch-scope.md` for coverage and ranking.
2. Read `references/luxury-editorial-design.md` if the output will become a designed report or PDF.
3. For each entity in the watch scope, conduct **exhaustive multi-source passes** before marking it "done." Minimum three distinct source types per entity:
   - **Official channels** — blog, product page, release notes, GitHub, arXiv
   - **Video coverage** — YouTube (official channel + major creators/analysts who cover this entity), BiliBili if Chinese
   - **Community discussion** — Reddit (relevant subs), X/Twitter search, Hacker News, Discord
   - **News outlets** — at least one general tech/news publication (TechCrunch, The Verge, VentureBeat, Ars Technica, SCMP, etc.) plus any vertical publications relevant to that entity
   - **Third-party trackers** — any independent benchmarks, aggregator sites, or comparison threads
4. Do not mark an entity as "no news found" until all four source tiers have been checked.
5. Dedupe against recent intake when possible.
6. Tag and rank items by AI filmmaking relevance, not generic hype.
7. Write the daily intake into `intel/daily/YYYY-MM-DD.md` using the established schema.
8. Promote strong items into durable folders when they are worth revisiting later.

**Hard rule: research until you are confident you have found everything, not until you have found something.** One official page is not sufficient. One Reddit thread is not sufficient. Exhaust the source tiers before moving on.

## Browser automation (mandatory for this skill)

This skill MUST use the OpenClaw browser for all tier-2 (video) and tier-3 (community/X/Twitter) research. The `user` profile attaches to your real logged-in Chrome session — this is required for accessing Reddit, YouTube, Bilibili, X/Twitter, and any site with JS-rendered content.

### How to use browser in subagent tasks

When spawning subagents for this skill, include this instruction block:

```
## Browser setup
- Use browser with profile="user" for ALL tier-2 (YouTube/Bilibili) and tier-3 (Reddit/X/Twitter/community) research
- The user profile reuses your existing Chrome login session — no extra auth needed
- Use web_search/web_fetch for tier-1 (official) and tier-4 (news) only
- Browser is for: YouTube creator videos, Bilibili demos, Reddit threads, X/Twitter posts, dynamic pages that load via JS

## Browser commands available
- openclaw browser --browser-profile user status  # check if browser is live
- openclaw browser --browser-profile user navigate <url>  # open a URL
- openclaw browser --browser-profile user snapshot  # get page content with element refs
- openclaw browser --browser-profile user screenshot  # screenshot
- openclaw browser --browser-profile user tabs  # list open tabs
- openclaw browser --browser-profile user open <url>  # open URL in new tab

## YouTube scraping workflow
1. Navigate to YouTube search: https://www.youtube.com/results?search_query=<entity>+AI+2026
2. Snapshot to see video titles, channels, dates
3. Click into relevant videos to get descriptions and comment context
4. Screenshot thumbnails if visual evidence is needed

## Reddit scraping workflow  
1. Navigate to Reddit search: https://www.reddit.com/search/?q=<entity>+AI+video
2. Snapshot to see post titles, scores, comment counts
3. Click into relevant posts for full content

## X/Twitter scraping workflow
1. Navigate to: https://twitter.com/search?q=<entity>+AI+video&src=typed_query
2. Snapshot to see post text, handles, engagement counts
3. Click into relevant posts for full context and replies
4. If logged in, check trending topics for AI filmmaking related terms

## Browser etiquette
- Prefer opening tabs over new windows
- Close tabs when done
- Keep browser state tidy between searches
- Reuse tabs where logical (search, click, back, click next result)
```

## Intake rules

Capture breadth, but spend summary effort selectively.

Each captured item should include:
- title
- source
- date
- link
- category
- tags
- quick note
- rough importance
- summary status
- promotion target
- status

## Prioritization

Prefer:
- direct creative utility
- controllability and consistency improvements
- workflow leverage
- startup/product implications
- shipped proof over demos and rumors

## Output discipline

The daily file is a research inbox, not a polished essay.
Keep entries compact and useful.

When generating a user-facing report from ongoing research:
- compare against the previous report when available
- omit items already meaningfully covered unless there is a real new development
- bias toward net-new updates rather than repeating background context
- add a final sanity-check section listing the sources checked

## Promotion discipline

Only promote when an item is likely to matter again:
- urgent strategic change
- workflow opportunity
- important paper
- recurring entity update
- experiment candidate

## Browser etiquette

When browsing sources:
- prefer reusing tabs
- open a new tab rather than a new window
- close unused tabs afterward
- keep the browser state tidy

## Design note

If turning research into a polished report:
- think like designing a website first
- prefer restrained, luxury light-mode editorial aesthetics
- use images only when they add real value
- avoid giant screenshots and noisy layout gimmicks
