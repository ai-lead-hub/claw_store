# Cron Plan

## Goal
Run a daily collection pass and an every-other-day synthesis pass.

## Proposed cadence

### Daily collection
- Frequency: once per day
- Suggested time: morning UTC, after global sources have updated
- Output: `intel/daily/YYYY-MM-DD.md`

### Every-other-day report
- Frequency: every 2 days
- Suggested time: after daily collection
- Input window: last 2 days of daily intake + promoted notes
- Output: `intel/reports/YYYY-MM-DD.md`

## Daily collection responsibilities

- gather links from watchlists
- include foreign-language sources when relevant
- dedupe against recent days
- tag each item
- assign rough importance
- choose shortlist for deeper evaluation
- mark possible promotion targets

## Every-other-day synthesis responsibilities

- read last 2 days of intake
- select top items for summary
- produce executive summary
- generate strategic implications
- include workflow/prompt gems
- append unsummarized link dump
- promote durable items into urgent / workflow / papers / entities / experiments

## Implementation note

Initial version can be prompt-driven and file-based.

Later version can add:
- lightweight structured JSONL sidecar files
- source-specific collection helpers
- scoring automation
- dedupe assistance

## Safety / quality note

Do not optimize for maximum volume.
Optimize for:
- relevance
- repeatability
- durability
- strategic usefulness
