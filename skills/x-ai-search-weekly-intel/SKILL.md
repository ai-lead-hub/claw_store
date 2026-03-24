---
name: x-ai-search-weekly-intel
description: Build a weekly AI tools/model intelligence report from AI Search posts on X. Use when asked to check @aisearchio, find a recent post that lists multiple tools or models, research those items across official .io/.ai/product pages, GitHub, and arXiv, cluster them by similar use case, write a user-friendly summary report, and export a PDF for delivery. Also use when setting up or running a recurring Sunday-evening workflow for this report.
---

# X AI Search Weekly Intel

Use this skill to turn a recent multi-tool AI Search post into a structured research brief.

## Core workflow

1. Read `references/workflow.md` and follow it in order.
2. Read `references/design-direction.md` and `references/luxury-editorial-design.md` before designing the report.
3. Use visible browser mode only if login/session issues require it; otherwise prefer headless.
4. Maintain browser etiquette: reuse tabs when possible, open tabs rather than new windows, and close unused tabs after capture.
5. Treat the X post as the discovery seed, not the final source of truth.
6. Research each named tool/model on:
   - official product/company pages
   - GitHub, if relevant
   - arXiv, if relevant
7. Cover the full named roundup unless the user explicitly asks for a subset.
8. Group items by similar user problem or workflow role, not by hype.
9. Write a report that is readable by a non-terminal human.
10. Prefer a continuous-scroll, editorial HTML/CSS report that reads like a premium newsletter or website.
11. Use images sparingly and intelligently: prefer official visuals or diagrams, otherwise use tightly cropped screenshots, otherwise omit the image.
12. Render the final report to PDF with `scripts/render_report_pdf.py`.

## Output requirements

The report must include:
- report title and date
- seed X post link
- short executive summary
- grouped sections by similar use case
- per-item summary with links
- notes on why each item matters
- a short "what to watch" section
- source links throughout

Prefer concise summaries over bloated coverage.

## Use-case grouping guidance

Group by practical role such as:
- video generation
- image generation
- editing / post-production
- control / consistency
- audio / voice
- 3D / world / scene tools
- developer / workflow infrastructure
- research models / papers

If a better grouping emerges from the actual batch, use that instead.

## PDF generation

Use `scripts/render_report_pdf.py` after the markdown report is complete.

Example:

```bash
python3 scripts/render_report_pdf.py input.md output.pdf
```

The script converts markdown to HTML and prints it to PDF using local Chrome.

## Scheduling

For recurring runs, also read `references/cron-setup.md`.

Prefer:
- isolated cron session
- explicit delivery target
- Sunday evening in the user's timezone
- headless browser mode once login/session state is stable
