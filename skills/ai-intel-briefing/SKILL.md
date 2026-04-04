---
name: ai-intel-briefing
description: >
  AI intelligence briefing: frontier lab updates, LLM releases, arXiv papers, benchmark news, plus AI creator tips/prompts/workflows from Western creators (X, YouTube, Reddit) and Chinese creators (Bilibili, Weibo — T8starAIX, dx5182 etc). Covers OpenAI, Anthropic, Google DeepMind, Meta, xAI, Mistral, DeepSeek, Qwen, Baidu, ByteDance, Tencent, Meituan and all major Chinese/Western labs. Output: luxury editorial PDF → GitHub archive → Telegram delivery. USE for: AI news, briefing, digest, creator tips, prompt tricks, workflow discoveries, what's new in AI, Chinese AI update, open-source AI roundup.
---

# AI Intelligence Briefing Skill

## ⚠️ READ THIS BEFORE STARTING — MANDATORY PREFLIGHT

**Browser MCP is NON-NEGOTIABLE.** Open a test tab first. If it fails → STOP immediately and tell the user. Do not silently fall back to web_search.

**Every source in the TODO list below MUST be visited. No skipping. No shortcuts.**

---

## BROWSER MCP — HOW TO USE IT CORRECTLY

This skill runs on Browser MCP (chrome-devtools). These are the exact tool calls you make.
Internalize this before touching a single URL.

### ACTUAL Tool Names (chrome-devtools MCP via mcporter)

| Action | Tool | Key Params |
|--------|------|-----------|
| Open new tab | `new_page` | `url` |
| Navigate | `navigate_page` | `type: "url"`, `url` |
| Wait for text | `wait_for` | `text: ["..."]`, `timeout` |
| Read page | `take_snapshot` | `verbose: false` |
| Close tab | `close_page` | `pageId: N` |
| List tabs | `list_pages` | — |
| Select tab | `select_page` | `pageId: N` |

### How to call chrome-devtools via exec:
```
mcporter call chrome-devtools.new_page --url "https://example.com"
mcporter call chrome-devtools.take_snapshot
```

### Standard Page Visit Sequence (memorize this)

```
1. mcporter call chrome-devtools.new_page --url TARGET_URL
2. mcporter call chrome-devtools.wait_for --text "[unique page text]" --timeout 5000
3. mcporter call chrome-devtools.take_snapshot  ← read ALL visible content
4. [extract items → write to scratchpad]
5. mcporter call chrome-devtools.close_page --pageId N
6. repeat for next URL
```

**Always wait for page content to load.** JS-rendered pages look empty without waiting. Use `list_pages` to check tab count — should never have >1 open.

### Scroll-to-Bottom Protocol (for feed pages)

For any page that is a feed (arXiv list, Reddit, HuggingFace trending, X search):
Use `evaluate_script` to scroll the page, then `take_snapshot` to read:
```
# Use evaluate_script to scroll:
mcporter call chrome-devtools.evaluate_script --function "() => window.scrollBy(0, 5000)"
# Then take snapshot:
mcporter call chrome-devtools.take_snapshot
# Repeat until content stops changing
```

### Search on X/Twitter

X search requires typing, not just navigating to a URL:
```
1. browser_navigate(url="https://x.com/search?q=QUERY&f=live")
2. browser_wait_for(time=3000)
3. [scroll-to-bottom protocol above]
4. browser_snapshot()
```
If login wall appears: try `https://nitter.poast.org/search?q=QUERY` as fallback.

### Handling Paywalls / Login Walls

| Site | Strategy |
|------|----------|
| X/Twitter | Try nitter: `nitter.poast.org/USER` or `nitter.poast.org/search?q=QUERY` |
| Reddit "verify" | Try `old.reddit.com/r/SUBREDDIT` |
| Bloomberg / FT / The Information | Check homepage only (free headlines), note [PAYWALLED] |
| Bilibili | Try YouTube as fallback for same creator |
| Any 403/404 | Google search `site:DOMAIN keyword` → update skill URL |

### Tab Hygiene Rules

- **ONE tab open at a time** — non-negotiable
- After every `take_snapshot()`, close the tab before opening the next
- Run `list_pages` periodically — if >1 tab is open, close extras immediately
- If browser crashes: restart, read scratchpad (it survived), continue from last checkpoint

---

## ⚠️ CRITICAL RULES — LEARNED THE HARD WAY

### 1. Always Check Previous Session's Briefing First
Before starting a new research session:
- Read `memory/briefing-YYYY-MM-DD.md` for the previous edition's content
- Read `memory/briefing-research-YYYY-MM-DD.md` for what was gathered today
- Identify **ongoing stories** that need follow-up
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
- Visit the actual X/Twitter accounts, YouTube channels, and Bilibili channels listed below using Browser MCP
- Generic "ComfyUI workflow tutorial" from search = immediately obvious filler, do not include it

### 4. Gemini/web_search Rate Limits Are a Real Constraint
- Gemini free tier: 5 requests/minute, 60 requests/day
- After ~8 web_search calls: rate limited for ~50 seconds
- **Prefer Browser MCP over web_search for all research** — browser has no quota
- web_search is only a last resort if browser MCP is unavailable for a specific source
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

### 8. Browser MCP Is This Skill's Primary Tool
- MCP server name: `chrome-devtools` (run `mcporter list-servers` to confirm)
- Claude Code's `--browser` flag is NOT the same — do not confuse them
- If Browser MCP disconnects mid-session: STOP, report exactly what was collected so far, wait for user

### 9. Research Is a Scratchpad, Not an Afterthought
- Write items to `briefing-research-YYYY-MM-DD.md` AS you find them, not at the end
- Include: title, source, URL, timestamp, priority tag, 1-line summary
- If session crashes, the scratchpad survives — this is your safety net

### 10. If You Can't Find a Source by URL, Search on Google First
- Dead URL → `browser_navigate("https://google.com/search?q=site:DOMAIN+keyword")`
- Once found, UPDATE THIS SKILL FILE with the working URL so future runs don't re-hit the dead link
- Always try Google search before marking a source as blocked

### 11. YouTube Requires "Last 7 Days" Filter — Always
YouTube is a primary source. Use this URL pattern to filter by recency:
`https://www.youtube.com/@CHANNEL/videos?view=0&sort=dd&shelf_id=0`
Or navigate to the channel, click Videos, then use the filter dropdown → "Last 7 days".
High views + recent date + specific technique = high signal item.

### 12. Snapshot Size Warning
If `browser_snapshot()` returns >50KB of text, the page is dense. Extract only:
- Headlines with dates
- Author names
- Key numbers/benchmarks
- URLs of individual items worth deeper reading
Do NOT try to read every paragraph — you'll hit context limits.

---

## TODO LIST — Complete This Every Single Run

### HOW TO USE THIS SECTION

**Every briefing run, without exception:**
1. Read the CONDENSED CHECKLIST below — this is what you work from during research
2. Open a NEW scratchpad: `memory/briefing-research-YYYY-MM-DD.md`
3. After completing each PHASE, update the TRACKER at the bottom of the scratchpad
4. If you get interrupted or stop early: the tracker shows exactly where you are
5. Do NOT start synthesis until PHASE 1.10 is complete or you hit a genuine blocker

---

```
============================================================
CONDENSED CHECKLIST — Work from this during research
============================================================
After each phase: UPDATE TRACKER in scratchpad (see bottom)

PREFLIGHT
  □ Browser MCP works (open google.com → snapshot test)
  □ Credentials confirmed (check memory files)
  □ Previous briefing read (ongoing stories noted)
  □ Today's scratchpad exists (create if not)

PHASE 1.1 — Western Labs [8 sources]
  □ OpenAI   □ Anthropic   □ DeepMind   □ Meta AI
  □ xAI      □ Mistral    □ Cohere     □ Perplexity

PHASE 1.2 — Chinese/Asian Labs [8 sources]
  □ DeepSeek □ Qwen/Alibaba □ Baidu □ ByteDance
  □ Tencent  □ Moonshot    □ 01.AI  □ South Korea

PHASE 1.3 — arXiv [7 sources]
  □ cs.AI □ cs.LG □ cs.CL □ cs.CV □ cs.RO
  □ Papers With Code □ HuggingFace Papers

PHASE 1.4 — Reddit [7 communities]
  □ r/ML □ r/LocalLLaMA □ r/singularity □ r/artificial
  □ r/StableDiffusion □ r/ClaudeAI □ r/ChatGPT

PHASE 1.5 — X/Twitter [4 searches + 6 accounts]
  □ AI search  □ LLM search  □ prompt tip  □ ComfyUI
  □ @sama □ @karpathy □ @ylecun □ @AnthropicAI
  □ @MistralAI □ @GoogleDeepMind

PHASE 1.6 — Tech News [8 sites]
  □ TechCrunch □ VentureBeat □ The Verge □ Ars Technica
  □ MIT Tech Review □ Wired □ Bloomberg □ The Information

PHASE 1.7 — Academic Labs [6 labs]
  □ Stanford HAI □ Berkeley BAIR □ MIT CSAIL □ AI2 □ EleutherAI □ Mila

PHASE 1.8 — HF + GitHub [4 sections]
  □ HF Models □ HF Papers □ GitHub Trending □ HF Orgs

PHASE 1.9 — Western Creators [6 accounts + 8 YouTube + 2 subreddits]
  □ @kavanthekid □ @simonmeyer □ @PJaccetturo □ @fofrAI
  □ @karenxcheng □ @nickfloats
  □ YouTube: Kilcher □ 2MP □ AI Explained □ Berman □ Fireship □ Sam Witteveen
  □ r/PromptEngineering □ r/comfyui

PHASE 1.10 — Eastern Creators [6 YouTube searches + 4 Bilibili + 1 WeChat]
  □ YT: AI绘画 □ ComfyUI □ 提示词 □ Flux □ AI视频 □ Kling
  □ Bilibili: AI绘画 □ ComfyUI □ 提示词 □ 大模型 □ T8starAIX □ dx5182
  □ WeChat: 量子位 □ 机器之心 □ 新智元

DONE phases: Write to TRACKER → Synthesize → PDF → GitHub → Telegram
============================================================
```

---

## RESEARCH TRACKER — Update After Every Phase

After completing each phase, update this block at the TOP of your scratchpad (above all items):

```
## TRACKER — Updated [HH:MM]
PREFLIGHT: [✅/⬜] | 1.1: [✅/⬜/🔶] | 1.2: [✅/⬜/🔶] | 1.3: [✅/⬜/🔶] | 1.4: [✅/⬜/🔶] | 1.5: [✅/⬜/🔶] | 1.6: [✅/⬜/🔶] | 1.7: [✅/⬜/🔶] | 1.8: [✅/⬜/🔶] | 1.9: [✅/⬜/🔶] | 1.10: [✅/⬜/🔶]
BLOCKED: [list any blocked/skipped sources]
PARTIAL: [any phase that was partially completed - e.g. 1.1 🔶 = 5 of 8 sources]
ITEMS: [running count of items in scratchpad so far]
```

**Status key:** ✅ complete | ⬜ not started | 🔶 partial

**Rules:**
1. Tracker goes at the TOP of scratchpad, not the bottom
2. Update after EVERY phase — not at the end
3. If interrupted, tracker tells you exactly where to resume
4. ITEMS count tells you if you have enough to synthesize
5. Do NOT start synthesis while any phase is ⬜ unless the source genuinely cannot be accessed
6. If a phase is BLOCKED, note it and continue — do not stop the entire run for one source

**When to synthesize vs continue researching:**
- Tracker shows 1.1-1.6 ✅, 1.7-1.10 ⬜: You have enough. Synthesize.
- Tracker shows 1.1 still 🔶 (partial): Finish Phase 1.1 first — minimum baseline.
- Tracker shows <15 items total: Continue researching before synthesizing.
- Tracker shows 1.1-1.10 all ✅ or 🔶: Full run. Synthesize.

---

## PDF Generation — Page-by-Page Layout Guidelines

**Read `references/pdf-style.md` for the full HTML template, CSS, ReportLab fallback, and code.** This section covers the rules and decisions. That file covers the implementation.

### Mandatory Page Order

```
Page 1:   COVER — edition #, date, tagline, stats bar
Page 2:   TABLE OF CONTENTS — 12 sections with page numbers
Page 3:   THE WEEK'S THESIS — full page, pull-quote treatment
Pages 4+: CONTENT SECTIONS — one section-header per page-group
Last:     APPENDIX — source roster, URLs, item counts
```

**NEVER** flow all 12 sections as a single unbroken scroll. Every section must start on a new page (`page-break-before: always` on `.section-start`).

### Pipeline: WeasyPrint (primary) → ReportLab (fallback)

**WeasyPrint install + run:**
```bash
pip install weasyprint --break-system-packages
# Windows — always wrap with:
chcp 65001 >nul && set PYTHONIOENCODING=utf-8 && python generate_pdf.py
```
```python
import weasyprint
weasyprint.HTML(filename="report.html").write_pdf("report.pdf")
```

### Non-Negotiable Rules

| Rule | Why |
|------|-----|
| No emoji in HTML/Python strings | Crashes on Windows CP1252; use CSS text labels instead |
| `print-color-adjust: exact` on body | Dark background disappears without it |
| `page-break-inside: avoid` on every item card | Cards must never split across pages |
| `break-inside: avoid` on two-column items | Prevents orphaned items in columns |
| Use `target-counter(attr(href url), page)` for TOC | Only way to get correct auto page numbers in WeasyPrint |
| Chinese font: Noto Sans SC via Google Fonts import | Missing font = boxes for all CJK characters |

### Item Card Structure (all sections)

Every news item, paper, and creator tip uses this HTML shape:

```html
<div class="item no-break">
  <div class="item-priority tag-high">HIGH</div>
  <div class="item-title">Item headline here</div>
  <div class="item-meta">source.com · April 3, 2026</div>
  <div class="item-body">One-paragraph summary.</div>
</div>
```

Priority tag classes: `tag-critical` / `tag-high` / `tag-medium` / `tag-signal`  
These map to colors — **never use emoji** 🔴🟠🟡🟢 — use the CSS classes only.

### Two-Column Layout for Creator Sections

Sections 8 and 9 (Creator Dispatch) have many short items — use two columns:
```css
.two-col { column-count: 2; column-gap: 16mm; }
.two-col .item { break-inside: avoid; }
```

### PDF Quality Checklist (run before delivery)

```
□ Cover page: edition number, date, stats bar present
□ TOC on page 2 with correct page numbers
□ Each of 12 sections starts on a new page
□ No item card split across a page break
□ Priority tags are CSS text labels, not emoji
□ Dark background renders (not white) — print-color-adjust set
□ Page number footer on every page
□ Chinese characters render correctly (Noto Sans SC loaded)
□ File size < 5MB
□ Body text >= 9pt, titles >= 11pt at 100% zoom
□ Windows: ran with chcp 65001 + PYTHONIOENCODING=utf-8
```

-> Full CSS variables, @page rules, section HTML templates, typography table, and ReportLab fallback code: **`references/pdf-style.md`**

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

| Situation | Browser MCP Action | Report As |
|-----------|-------------------|-----------|
| Page 404/DNS | `browser_navigate` to Google, search for the content, update skill URL | `[DEAD LINK → FOUND AT: new_url]` |
| Page blank after 2s wait | `browser_scroll` down + `browser_wait_for(3000)` + `browser_snapshot` again | `[BLANK]` if still empty |
| Tab hangs >30s | `browser_tab_close` current, open new tab | `[TIMEOUT]` |
| Login wall (X) | Try nitter.poast.org fallback | `[NITTER FALLBACK]` |
| Login wall (Reddit) | Try old.reddit.com | `[OLD REDDIT FALLBACK]` |
| Bilibili region block | YouTube Chinese search fallback | `[BILIBILI BLOCKED → YT FALLBACK]` |
| Paywall (Bloomberg etc) | Headlines only from homepage | `[PAYWALLED: headlines only]` |
| 429 rate limit | `browser_wait_for(15000)`, retry once | `[RATE LIMITED]` if still blocked |
| MCP disconnects | STOP all research. Report last completed phase. Wait for user. | IMMEDIATE STOP |
| >1 tab open | `browser_tab_list` → close extras | Internal hygiene, don't report |

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
12. **Appendix** — full source roster with item counts and URLs

---

## Ongoing Stories Protocol

1. Before synthesizing, check the previous edition's `briefing-YYYY-MM-DD.md`
2. For each story flagged as "to watch" or in development, search for updates
3. In the report, explicitly note: "This story from Edition #N had a development this week"
4. Continuity is what distinguishes a good briefing from a news dump

---

## Key Creator Accounts (Western) — CHECK EVERY RUN

### AI Filmmakers
| Creator | X Handle | YouTube |
|---------|----------|---------|
| Kavan the Kid | @kavanthekid | search "Kavan the Kid AI" |
| Simon Meyer | @simonmeyer_director | search "Simon Meyer AI director" |
| PJ Ace | @PJaccetturo | search "PJ Ace AI" |

### ComfyUI / Flux Workflow Creators
| Creator | X Handle | Focus |
|---------|----------|-------|
| fofrAI | @fofrAI | Latent Vision, Flux/ComfyUI |
| Karen X Cheng | @karenxcheng | AI art workflows |
| Nick Floats | @nickfloats | Creative AI, model comparisons |

### YouTube Channels (use "Last 7 Days" filter)
| Channel | Focus |
|---------|-------|
| Yannic Kilcher | Paper deep-dives |
| Two Minute Papers | Research highlights |
| AI Explained | AI news analysis |
| Matthew Berman | Model reviews/demos |
| Fireship | Tech news (AI heavy) |
| Sam Witteveen | LLM engineering |
| Scott Detweiler | ComfyUI workflows |
| Nerdy Rodent | ComfyUI node tutorials |
| Latent Vision / fofrAI | Advanced ComfyUI pipelines |

---

## Key Creator Accounts (Eastern/Chinese) — CHECK EVERY RUN

### YouTube Chinese Search Queries (filter: last 7 days)
- `AI绘画教程` — AI painting tutorial
- `ComfyUI工作流` — ComfyUI workflow
- `提示词技巧` — prompt tips
- `Flux工作流` — Flux workflow
- `AI视频生成` — AI video generation
- `Kling AI教程` / `可灵教程` — Kling tutorial
- `万相工作流` — Wan workflow

### Bilibili Key Creators
| Creator | Bilibili ID | Focus |
|---------|------------|-------|
| T8starAIX | T8star/T8星 | ComfyUI workflows, image gen |
| dx5182 | dx5182 | Open-source tools, practical workflows |
| 秋葉aaaki | Search by name | SD/ComfyUI educator |

### WeChat via Sogou (sogou.com/weixin)
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
