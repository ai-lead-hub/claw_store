# AI Filmmaking Research OS

This repo area is for continuous intelligence gathering and synthesis for an AI filmmaking startup.

## Purpose

This system should help answer:
- What changed?
- What matters?
- What should we test?
- What should we build?
- What should we ignore for now?

## Core flow

1. **Capture** → raw daily intake in `intel/daily/`
2. **Evaluate** → score, tag, summarize, and assess relevance
3. **Promote** → move durable items into `urgent/`, `workflow-opportunities/`, `research-papers/`, and `entities/`
4. **Synthesize** → publish every-other-day reports in `intel/reports/`

## Main folders

- `daily/` — raw daily intake and quick triage
- `reports/` — polished every-other-day intelligence reports
- `urgent/` — small set of high-priority items to read now
- `workflow-opportunities/` — items that could influence product/workflow decisions
- `research-papers/` — paper notes with implementation implications
- `entities/` — persistent notes on labs, tools, creators, repos, competitors
- `experiments/` — hypotheses and concrete tests to run
- `sources/` — watchlists and source maps
- `meta/` — taxonomy, scoring, operating rules
- `templates/` — reusable note/report templates

## Current priorities

- Build a reliable daily collection loop
- Generate useful every-other-day synthesis
- Promote important items into durable notes
- Bias toward actionable signal for AI filmmaking workflows and startup strategy

## Hot files

- `meta/taxonomy.md`
- `meta/scoring.md`
- `meta/operating-model.md`
- `sources/watchlists.md`
- `templates/daily-intake-template.md`
- `templates/report-template.md`
- `meta/cron-plan.md`

## Status model

An item should move through these states:
- `captured`
- `triaged`
- `summarized`
- `evaluated`
- `promoted`
- `archived`

## Decision principle

This is not a generic AI news archive.

Prioritize:
- direct creative utility
- startup/product implications
- workflow leverage
- high proof over hype
- repeatable techniques over flashy one-offs
