# Workflow

## Goal
Turn one recent AI Search X post that lists multiple tools/models into a compact weekly research report.

## Step 1 — Find the seed post

Go to `@aisearchio` on X.

Look at the most recent few posts and choose the one that:
- mentions multiple tools and/or models
- looks like a roundup, comparison, or notable batch
- is recent enough for a weekly report

Capture:
- post URL
- post date
- short note on why this post was chosen

## Step 2 — Extract the research set

Pull out the named items.

For each item, capture at minimum:
- name
- rough type: tool / model / company / paper / repo
- rough category

Ignore obvious filler unless it is useful.

## Step 3 — Research each item

Unless the user asks for a partial sample, cover the full named roundup from the chosen seed post.

For each extracted item, prioritize these sources in order:

1. Official page
- company page
- product page
- launch post
- docs page

2. GitHub
- official repo if it exists
- key signals: stars, recent activity, installability, demo assets, README clarity

3. arXiv
- only when the item is a research model/paper or clearly paper-backed

Capture only high-value facts:
- what it does
- target use case
- core capability
- whether it looks shipped, research-only, or ecosystem tooling
- why it matters

Do not waste report space on boilerplate marketing language.

## Step 4 — Cluster by use case

Group items by similarity of job-to-be-done.

Good grouping examples:
- video generation
- image generation
- editing / enhancement
- controllability / consistency
- audio / voice
- workflow / infrastructure
- research / frontier models

Do not force a category if the batch suggests a better grouping.

## Step 5 — Write the report

Before writing, compare against the previous relevant report if available.
If an item was already meaningfully covered, omit it unless there is a real new development worth reporting.

Use this structure:

1. Title
2. Seed post
3. Executive summary
4. Grouped findings (net-new / changed items only)
5. What matters most
6. Watch list / follow-ups
7. Source links appendix / sanity-check list of sources checked

Per item include:
- name
- one-line description
- group/category
- short summary
- why it matters
- links: official / GitHub / arXiv as available

## Step 6 — Style and layout

Write for a smart operator, not a researcher.

Use:
- plain language
- short paragraphs
- bullets where helpful
- direct judgments
- continuous-scroll editorial flow
- premium newsletter / website reading feel

Avoid:
- vague hype
- repeating the same claims from official sites
- giant unsorted dumps
- giant full-page screenshots
- over-designed layouts that are harder to read than the content

Image policy:
1. official hero / official visual asset
2. official diagram / explainer image
3. tightly cropped screenshot
4. no image

## Step 7 — Render PDF

Save the report as markdown, then render it:

```bash
python3 scripts/render_report_pdf.py <input.md> <output.pdf>
```

## Step 8 — Delivery

Deliver the PDF and a short summary message.

The message should say:
- what seed post was used
- how many items were researched
- the main clusters found
- what stood out most
