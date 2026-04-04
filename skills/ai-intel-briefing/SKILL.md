---
name: ai-intel-briefing
description: >
  AI intelligence briefing: frontier lab updates, arXiv papers, benchmark news, AI creator
  tips/prompts/workflows from Western and Chinese creators. Covers OpenAI, Anthropic,
  Google DeepMind, Meta, xAI, Mistral, DeepSeek, Qwen, Baidu, ByteDance, and all major
  labs. Output: luxury editorial PDF → GitHub archive → Telegram delivery.
  USE for: AI news briefing, digest, creator tips, what's new in AI.
---

# AI Intelligence Briefing Skill

## ⚠️ READ THIS BEFORE STARTING — MANDATORY PREFLIGHT

**Browser MCP is NON-NEGOTIABLE.** Open a test tab first. If it fails → STOP immediately
and tell the user. Do not silently fall back to web_search.

**Every source in the TODO list below MUST be visited. No skipping. No shortcuts.**

---

## ⚠️ CRITICAL RULES — LEARNED THE HARD WAY

### 1. ALWAYS Check Previous Session's Briefing First
Before starting a new research session:
- Read `memory/briefing-YYYY-MM-DD.md` for the **previous edition's** content
- Read `memory/briefing-research-YYYY-MM-DD.md` for what was gathered today
- Identify **ongoing stories** that need follow-up (developments from last edition)
- Identify **what was already researched today** so you don't repeat it
- Do NOT treat each briefing as a fresh start — the best briefings are sequels

### 2. Creds Are in the Workspace, Not Env Vars
Shell env vars are often empty when spawned. Credentials are stored in:
- `memory/YYYY-MM-DD.md` of any previous session
- GitHub: `ai-lead-hub/claw_store` repo (check any briefing folder's metadata.json)
- Telegram bot: `Hephaeustus_bot` / `TELEGRAM_BOT_REDACTED_U4VU-JCZUTM4vJg0`
- Telegram chat: `7739622002`
- GitHub token: `GH_TOKEN_REDACTED`

Set creds in Python via direct assignment in the script, NOT `os.environ`.

### 3. Creator Tips Must Come From Actual Account Visits
- web_search is NOT acceptable for creator tips
- If web_search/Gemini fails (rate limits, 429), do NOT substitute with generic content
- Visit the actual X/Twitter accounts, YouTube channels, and Bilibili channels listed below
- Generic "ComfyUI workflow tutorial" from search = immediately obvious filler

### 4. Gemini/web_search Rate Limits Are a Real Constraint
- Gemini free tier: 5 requests/minute, 60 requests/day
- After ~8 web_search calls: rate limited for ~50 seconds
- When rate limited mid-research: switch to web_fetch (more reliable, no quota)
- web_fetch works on most sites but gives raw content — extract manually
- If both are blocked: report the gap to user, don't fake the content

### 5. Windows Python Execution
- Never pipe Python scripts through `&&` — use a `.bat` wrapper or direct `python "path"`
- Always set `chcp 65001 >nul` (UTF-8) before Python in batch files
- Always set `PYTHONIOENCODING=utf-8` before running
- Emoji in print() causes `UnicodeEncodeError: 'charmap' codec can't encode` on Windows CP1252
- Use `cmd /c "chcp 65001 >nul && python script.py"` or a `.bat` file

### 6. GitHub API Version
- Use `X-GitHub-Api-Version: 2022-11-28` in all GitHub API calls
- Without this, some endpoints return 422 or wrong response shapes

### 7. GitHub b64 Content Is Bytes
- `base64.b64decode(data["content"])` returns `bytes`, not `str`
- Decode with `.decode("utf-8")` before `json.loads()`
- Wrong: `json.loads(base64.b64decode(data["content"]))`
- Right: `json.loads(base64.b64decode(data["content"]).decode("utf-8"))`

### 8. Browser MCP Is This Skill's MCP — Use It
- The skill's chrome-devtools MCP is the primary research tool
- Claude Code's `--browser` flag is NOT the same — do not confuse them
- If the skill's browser MCP fails: stop and tell the user
- MCP server name: `chrome-devtools` (use `mcporter list-servers` to confirm)

### 9. Research Is a Scratchpad, Not an Afterthought
- Write items to `briefing-research-YYYY-MM-DD.md` as you find them, not at the end
- If session crashes, the scratchpad survives
- Include: title, source, URL, timestamp, priority tag, 1-line summary
- Append items throughout — don't batch at the end

### 10. Browser Hygiene — ONE TAB AT A TIME, ALWAYS
This is non-negotiable for any research session:
1. Open a new tab
2. Navigate to the URL
3. Scroll to the very BOTTOM of the page (all lazy-loaded content must load first)
4. Read all visible content
5. Extract relevant items → write to scratchpad immediately
6. Close the tab
7. THEN open the next URL
8. Repeat

**Why it matters:** Open tabs accumulate memory, cause browser crashes, and lost tabs = lost work.
A crashed browser mid-research = hours of work gone.
If the browser crashes: restart it, read the scratchpad (it survived), continue.

### 11. If You Can't Find a Source by URL, Search on Google First
- If a URL in this skill is dead or you can't find the page → search on Google
- Search query format: `site:[domain] [lab name] [content type]` e.g. `site:deepmind.google.com blog`
- Once found, UPDATE THE SKILL with the working URL so future runs don't hit the dead link
- Always try Google search before marking a source as blocked

### 12. YouTube Is Critical — Check Every Run
YouTube is a primary source for AI creator content, including:
- Chinese AI creators who publish tutorials in Chinese on YouTube
- AI filmmaker workflow breakdowns
- ComfyUI/Flux workflow walkthroughs
- LLM engineering deep dives
- New tool tutorials (often appear on YouTube before official docs)
- Check the "Last 7 days" filter on channel uploads, not just search
- If a YouTube channel/video has high views + recent date + specific technique → it's high signal

---

## BROWSER RESEARCH PROTOCOL (ONE TAB AT A TIME)

**For every single URL you visit, without exception:**

```
LOOP:
  1. open new tab
  2. navigate to [URL]
  3. wait for page to fully load (watch for spinners, lazy content)
  4. scroll to BOTTOM of page (keep scrolling until content stops loading)
  5. read ALL visible content (headlines, summaries, timestamps, authors)
  6. extract relevant items:
     - title
     - source name
     - URL
     - timestamp/date
     - 1-line summary
     - priority tag (🔴🟠🟡🟢)
  7. write ALL extracted items to scratchpad (briefing-research-YYYY-MM-DD.md)
  8. close tab
  9. if more URLs → go to LOOP step 1
```

**Tab discipline rules:**
- NEVER have more than 1 tab open at a time
- If you find a link within a page you want to read → note the URL first, close current tab, open new tab with that URL
- If browser has 3+ tabs open → this is a warning sign, close extras immediately
- If browser crashes → restart, resume from scratchpad (it survived)

---

## TODO LIST — Complete This Every Single Run

Copy this checklist at the start of each run. Mark each item DONE as you complete it.
Every item must be checked. Report any BLOCKED or SKIPPED items to the user.

```
□ PREFLIGHT — Browser MCP test (open a tab, confirm it loads)
□ PREFLIGHT — Note time window (default: last 7 days)
□ PREFLIGHT — Confirm GitHub/Telegram credentials (check workspace memory files)
□ PREFLIGHT — Read previous briefing (memory/briefing-YYYY-MM-DD.md) for ongoing stories
□ PREFLIGHT — Read today's scratchpad (briefing-research-YYYY-MM-DD.md) to avoid re-researching

□ PHASE 1.1 — WESTERN FRONTIER LABS (official blogs + X accounts)
  □ OpenAI — openai.com/blog + @OpenAI X page
  □ Anthropic — anthropic.com/news + @AnthropicAI X page
  □ Google DeepMind — deepmind.google/blog + @GoogleDeepMind X page
  □ Meta AI — ai.meta.com + @MetaAI X page
  □ xAI — x.ai/blog + @xaboratory x.ai X page
  □ Mistral — mistral.ai/news + @MistralAI X page
  □ Cohere — cohere.com/research + @CohereAI X page
  □ Perplexity — perplexity.ai/blog + @AlessandroIZ X page

□ PHASE 1.2 — CHINESE/ASIAN FRONTIER LABS
  □ DeepSeek — deepseek.com (check for new model releases, V3.2 etc.)
  □ Qwen/Alibaba — qwenlm.github.io + HuggingFace org qwen
  □ Baidu — baidu.com (ERNIE, Qianfan-OCR)
  □ ByteDance — huggingface.co/bytedance (deer-flow)
  □ Tencent — tencent.com (Hunyuan updates)
  □ Moonshot AI — moonshot.cn (Kimi updates)
  □ 01.AI — 01.ai (Yi models)
  □ South Korea — Rebellions, Naver Clova updates

□ PHASE 1.3 — ARXIV (last 7 days, all relevant categories)
  □ arXiv cs.AI — arxiv.org/list/cs.AI/recent
  □ arXiv cs.LG — arxiv.org/list/cs.LG/recent
  □ arXiv cs.CL — arxiv.org/list/cs.CL/recent
  □ arXiv cs.CV (multimodal relevant) — arxiv.org/list/cs.CV/recent
  □ arXiv cs.RO (robotics relevant) — arxiv.org/list/cs.RO/recent
  □ Semantic Scholar — semanticscholar.org (trending papers)
  □ Papers With Code — paperswithcode.com/latest

□ PHASE 1.4 — REDDIT COMMUNITIES (last 72h)
  □ r/MachineLearning — reddit.com/r/MachineLearning (top week)
  □ r/LocalLLaMA — reddit.com/r/LocalLLaMA (top week)
  □ r/singularity — reddit.com/r/singularity (top week)
  □ r/artificial — reddit.com/r/artificial (top week)
  □ r/StableDiffusion — reddit.com/r/StableDiffusion
  □ r/ClaudeAI — reddit.com/r/ClaudeAI
  □ r/ChatGPT — reddit.com/r/ChatGPT
  NOTE: Reddit frequently shows "Please wait for verification" — skip if blocked, note in report

□ PHASE 1.5 — KEY X/TWITTER ACCOUNTS
  □ @sama (Sam Altman) — OpenAI announcements
  □ @karpathy — AI/DL insights + supply chain warnings
  □ @ylecun (Yann LeCun) — Meta AI, research
  □ @demishassabis — DeepMind CEO
  □ @GoogleDeepMind — Gemma 4, Gemini updates
  □ @AnthropicAI — Claude releases, research
  □ @MistralAI — Voxtral, Mistral updates
  □ @emostaque — Meta AI chief
  □ @AndrewYNg — AI education, landing AI
  □ Search: "AI since:7d min_faves:300" on X
  □ Search: "LLM since:7d min_faves:200" on X

□ PHASE 1.6 — TECH NEWS SITES (last 7 days)
  □ TechCrunch AI — techcrunch.com/category/artificial-intelligence
  □ VentureBeat AI — venturebeat.com/category/ai
  □ The Verge AI — theverge.com/ai-artificial-intelligence
  □ Ars Technica AI — arstechnica.com/ai
  □ MIT Tech Review — technologyreview.com/topic/artificial-intelligence
  □ Wired AI — wired.com/tag/artificial-intelligence
  □ The Information AI — theinformation.com (check homepage)
  □ Financial Times Technology — ft.com/technology
  □ Bloomberg Technology — bloomberg.com/technology

□ PHASE 1.7 — ACADEMIC LABS + UNIVERSITY AI (last 30 days)
  □ Stanford HAI News — hai.stanford.edu/news
  □ Berkeley BAIR Blog — bair.berkeley.edu/blog
  □ MIT CSAIL — csail.mit.edu (news)
  □ CMU ML — ml.cmu.edu (news)
  □ Allen Institute (AI2) — allenai.org (blog)
  □ EleutherAI — eleuther.ai (check for releases)
  □ Mila — mila.quebec (news)
  □ Oxford Future of Humanity — fhi.ox.ac.uk (publications)
  □ Cambridge MLMI — ci.cl.cam.ac.uk (publications)

□ PHASE 1.8 — HUGGINGFACE + GITHUB
  □ HF Trending Models — huggingface.co/models?sort=trending
  □ HF Trending Papers — huggingface.co/papers/trending
  □ HF Papers Daily — huggingface.co/papers (daily)
  □ GitHub Trending AI — github.com/trending (last week)
  □ HF Organizations: google (Gemma), microsoft (Phi, VibeVoice),
    facebook (SAM), Cohere, NousResearch, meta-llm

□ PHASE 1.9 — WESTERN CREATOR TIPS (X + YouTube + Reddit) — CRITICAL
  □ @kavanthekid — AI filmmaker, Phantom X, SAG-approved, Kling/Higgsfield workflows
  □ @simonmeyer_director — Higgsfield $150k winner, Kling/Seedance prompts
  □ @PJaccetturo — Genre.ai CEO, 300M+ views, Veo 3/Kling/Grok prompts
  □ @fofrAI — Latent Vision, Flux/ComfyUI workflows
  □ @karenxcheng — AI art workflows, Midjourney/Flux
  □ @nickfloats — Creative AI, new model comparisons
  □ X search: "prompt tip since:3d min_faves:300"
  □ X search: "ComfyUI workflow since:3d min_faves:200"
  □ X search: "AI system prompt tip since:3d min_faves:500"
  □ YouTube: Yannic Kilcher (last 7 days uploads)
  □ YouTube: Two Minute Papers (last 7 days)
  □ YouTube: AI Explained (last 7 days)
  □ YouTube: Matthew Berman (last 7 days)
  □ YouTube: Fireship (last 7 days)
  □ YouTube: Sam Witteveen (last 7 days)
  □ r/PromptEngineering — top posts week
  □ r/ChatGPTPro — power user tricks week
  □ r/comfyui — workflows week
  NOTE: Visit actual accounts — do NOT substitute with generic web_search content
  NOTE: Use "Last 7 days" filter on YouTube channels

□ PHASE 1.10 — CREATOR TIPS: EASTERN + CHINESE (YouTube + Bilibili + Weibo) — CRITICAL
  Many Chinese AI creators publish on YouTube in Chinese — check BOTH platforms
  Many Chinese creators also publish on Bilibili, Weibo, Xiaohongshu
  If Bilibili/Weibo blocked → prioritize YouTube Chinese creators as fallback

  □ YouTube: Search "AI绘画教程" (AI painting tutorial) — last 7 days
  □ YouTube: Search "ComfyUI工作流" (ComfyUI workflow) — last 7 days
  □ YouTube: Search "提示词技巧" (prompt tips) — last 7 days
  □ YouTube: Search "Flux工作流" (Flux workflow) — last 7 days
  □ YouTube: Search "AI视频生成" (AI video generation) — last 7 days
  □ YouTube: Search "Kling AI教程" — last 7 days
  □ YouTube: Search "万相/可灵工作流" (Wan/Kling workflow) — last 7 days

  □ Bilibili search: "AI绘画教程" (AI painting tutorial), last 7 days
  □ Bilibili search: "ComfyUI工作流" (ComfyUI workflow), last 7 days
  □ Bilibili search: "提示词技巧" (prompt tips), last 7 days
  □ Bilibili search: "大模型教程" (LLM tutorial), last 7 days
  □ Bilibili search: "Flux工作流" (Flux workflow), last 7 days
  □ Bilibili search: "AI视频生成" (AI video generation), last 7 days
  □ Bilibili: T8starAIX (ComfyUI workflows)
  □ Bilibili: dx5182 (open-source workflows)
  □ Weibo search: "AI工作流", "提示词", "ComfyUI"
  □ WeChat: 量子位 (Quantum Bits) AI news
  □ WeChat: 机器之心 (Machine Intelligence) AI news
  □ WeChat: 新智元 (AI Era) AI news
  □ GitHub: search repos with Chinese README (topic:comfyui stars:>100)
  NOTE: If Bilibili/Weibo blocked → search harder on YouTube, report gap

□ PHASE 2 — WRITE RESEARCH LOG (memory/briefing-research-YYYY-MM-DD.md)
  □ All items from 1.1–1.10 written to scratchpad AS YOU FIND THEM
  □ Priority tags assigned (🔴🟠🟡🟢)
  □ URLs recorded for every item
  □ BLOCKED/SKIPPED sources noted at top with reason
  □ ONGOING STORY FLAGS: mark items that are follow-ups from previous editions

□ PHASE 3 — DEDUPLICATE against seen_items.json
  □ New items identified
  □ Duplicate items noted (with original report date)

□ PHASE 4 — SYNTHESIZE into 12-section report
  □ Section 1: The Week's Thesis (narrative arc — tie events together)
  □ Section 2: Frontier Dispatches — Western Labs
  □ Section 3: Eastern Front — Asian/Chinese Labs
  □ Section 4: The Research Layer — arXiv/Academic
  □ Section 5: Infrastructure & Tooling
  □ Section 6: Community Pulse
  □ Section 7: The Numbers — Benchmarks & Evals
  □ Section 8: Creator Dispatch — Western
  □ Section 9: Creator Dispatch — Eastern
  □ Section 10: What to Watch
  □ Section 11: Curator's Note
  □ Appendix: Source Roster (full list of sources visited + item counts)
  □ ONGOING STORIES: explicitly note developments in stories from previous editions

□ PHASE 5 — GENERATE PDF
  □ HTML template from references/pdf-style.md
  □ WeasyPrint conversion (Windows: set chcp 65001, PYTHONIOENCODING=utf-8)
  □ Fallback: HTML file if WeasyPrint not available

□ PHASE 6 — STORE TO GITHUB
  □ Push report.pdf + items.json + metadata.json to reports/YYYY-MM-DD_HH-MM/
  □ Update seen_items.json with new items
  □ GitHub API version header: X-GitHub-Api-Version: 2022-11-28

□ PHASE 7 — TELEGRAM DELIVERY
  □ Send PDF with rich caption
  □ Include: edition number, item count, critical count, source count
  □ Include GitHub archive link

□ FINAL REPORT — Post completion summary to user
  □ Total sources visited vs planned
  □ All BLOCKED/SKIPPED sources listed
  □ Any [PARTIAL] categories noted
  □ Quality floor checklist: ≥25 items ✅/❌, ≥6 source types ✅/❌,
    ≥5 arXiv ✅/❌, ≥3 Chinese lab ✅/❌, ≥5 Western creator tips ✅/❌,
    ≥3 Chinese creator items ✅/❌
  □ ONGOING STORIES: list which stories from last edition had developments this week
```

---

## Quality Standards — Minimums

Every report MUST meet all of these before delivery:

| Floor | Required | Check |
|-------|----------|-------|
| Total items | ≥ 25 | __ |
| Source types | ≥ 6 different categories | __ |
| arXiv papers | ≥ 5 with citations | __ |
| Chinese lab updates | ≥ 3 | __ |
| Western creator tips | ≥ 5 actionable | __ |
| Chinese creator items | ≥ 3 | __ |
| Critical items | ≥ 1 | __ |

If any floor is not met → expand research on that category before synthesizing.

---

## Priority Tags

- 🔴 **CRITICAL** — Major release, breakthrough, security event, AGI signal
- 🟠 **HIGH** — Notable update, competitive move, benchmark result
- 🟡 **MEDIUM** — Product update, community development, interesting paper
- 🟢 **SIGNAL** — Trend, rumor, early indicator

---

## Error Handling

**Every error MUST be reported. Never silently absorb failures.**

| Situation | Action |
|-----------|--------|
| Page 404/DNS | Note `[DEAD LINK]`, try alternative URL, try Google search, UPDATE SKILL with working URL |
| Paywall | Note `[PAYWALLED]`, try homepage, report |
| Blank/JS error | Wait 5s, refresh once. Still blank → `[BLANK]`, skip, report |
| Browser tab hangs >30s | Close, note `[TIMEOUT]`, skip that source, report |
| X/Twitter login wall | Try mobile version or nitter instance, report if blocked |
| Bilibili region block | Try YouTube search for same content (many creators cross-post), report if blocked |
| Rate limited (429) | Wait 15s, retry once. Still blocked → skip, report |
| Reddit "Please wait for verification" | Skip Reddit for that run, note in report |
| web_search/Gemini rate limited | Switch to web_fetch, report if both blocked |
| MCP disconnects | STOP research. Report exactly what was lost. Wait for user. |
| Can't find source URL | Google search for the content, update skill with working URL |

**End-of-run report MUST include:**
- Sources attempted vs successful
- Full list of BLOCKED/SKIPPED/TIMEOUT sources
- Any [PARTIAL] category (fewer than 3 sources read)
- Quality floor checklist results

---

## Report Structure (12 Sections)

1. **The Week's Thesis** — single most important narrative, 1 paragraph
2. **Frontier Dispatches — Western Labs** — per-lab updates
3. **Eastern Front** — Chinese/Asian lab updates
4. **The Research Layer** — arXiv/academic highlights
5. **Infrastructure & Tooling** — frameworks, hardware, APIs, deployment
6. **Community Pulse** — Reddit, X, YouTube signals
7. **The Numbers** — benchmarks, evals, rankings
8. **Creator Dispatch: Western** — X/YouTube/Reddit tips
9. **Creator Dispatch: Eastern** — Bilibili/YouTube/Weibo/WeChat tips
10. **What to Watch** — forward-looking signals
11. **Curator's Note** — editorial take
12. **Appendix** — full source roster with item counts

---

## Ongoing Stories Protocol

At the end of every briefing, flag stories that are **ongoing developments**:

1. Before synthesizing, check the previous edition's `briefing-YYYY-MM-DD.md`
2. For each story that was "to watch" or in development, search for new updates
3. In the report, explicitly note: "This story from Edition #N had a development this week"
4. This is what distinguishes a good briefing from a news dump — continuity

---

## Key Creator Accounts (Western) — CHECK EVERY RUN

### AI Filmmakers (highest signal for creative AI workflows)
| Creator | Platform | Focus |
|---------|----------|-------|
| **Kavan the Kid** | @kavanthekid (X), YouTube | AI narrative film, Kling/Higgsfield, Phantom X |
| **Simon Meyer** | @simonmeyer_director (X), YouTube | AI commercials, Kling/Seedance, Higgsfield winner |
| **PJ Ace** | @PJaccetturo (X), YouTube | AI ads, Genre.ai, Veo 3/Kling, viral production |

### ComfyUI / Flux Workflow Creators
| Creator | Platform | Focus |
|---------|----------|-------|
| **@fofrAI** | X, YouTube | Latent Vision, Flux/ComfyUI workflows |
| **@karenxcheng** | X, YouTube | AI art workflows, Midjourney/Flux |
| **@nickfloats** | X, YouTube | Creative AI, model comparisons |

### YouTube Channels — CHECK EVERY RUN (use Last 7 Days filter)
| Channel | Focus |
|---------|-------|
| **Yannic Kilcher** | Paper deep-dives |
| **Two Minute Papers** | Research highlights |
| **AI Explained** | AI news analysis |
| **Matthew Berman** | Model reviews/demos |
| **Fireship** | Tech news (AI heavy) |
| **Sam Witteveen** | LLM engineering |
| **Scott Detweiler** | ComfyUI workflows |
| **Nerdy Rodent** | ComfyUI node tutorials |
| **Latent Vision** | Advanced ComfyUI pipelines |

---

## Key Creator Accounts (Eastern/Chinese) — CHECK EVERY RUN

Many Chinese AI creators publish on YouTube in Chinese. Check YouTube AND Bilibili.

### YouTube Chinese Creators (search in Chinese, check every run)
- Search: "AI绘画教程" → filter last 7 days
- Search: "ComfyUI工作流" → filter last 7 days
- Search: "Flux工作流" → filter last 7 days
- Search: "Kling教程" / "可灵教程" → filter last 7 days

### Bilibili Key Creators
| Creator | Bilibili ID | Focus |
|---------|------------|-------|
| T8starAIX | T8star/T8星 | ComfyUI workflows, image gen |
| dx5182 | dx5182 | Open-source tools, practical AI workflows |
| 秋葉aaaki | Search by name | Popular SD/ComfyUI educator |

### Weibo Key Accounts (search: AI绘画, ComfyUI, 提示词)
Filter by: 热度 (popularity), last 7 days

### WeChat (search via sogou.com/weixin)
| Account | Focus |
|---------|-------|
| 量子位 | AI news, tools, tutorials |
| 机器之心 | Deep ML/AI coverage |
| 新智元 | AI industry + tutorials |

---

## Reference Files

- `references/sources.md` — Master URL list (backup if you can't find a source)
- `references/pdf-style.md` — Luxury HTML/CSS template + WeasyPrint code
- `references/prompts.md` — Synthesis prompts for writing each section
- `references/github-storage.md` — GitHub API code for push + dedup
- `references/creator-sources.md` — Full creator account list + translation tips

## Known Working Credentials (check memory files for latest)
- GitHub token: `GH_TOKEN_REDACTED`
- GitHub repo: `ai-lead-hub/claw_store`
- Telegram bot: `Hephaeustus_bot` (`TELEGRAM_BOT_REDACTED_U4VU-JCZUTM4vJg0`)
- Telegram chat: `7739622002`
