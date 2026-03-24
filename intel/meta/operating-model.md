# Operating Model

## Goal
Build a continuous intelligence system for an AI filmmaking startup.

This system should:
1. track the market
2. support product and workflow decisions
3. store durable knowledge in a searchable structure

## Pipeline states

### 1. Capture
Collect raw items with minimal friction.

Required fields:
- date
- title
- source
- link
- language
- primary category
- rough relevance
- quick note
- status

Output:
- `intel/daily/YYYY-MM-DD.md`

### 2. Triage
Dedupe, tag, and rank items.

Decide:
- summarize now
- keep as link-only
- monitor
- ignore for now

### 3. Evaluate
For stronger items, add:
- short summary
- why it matters
- filmmaking relevance
- scoring
- decision relevance
- promotion targets

### 4. Promote
Move durable items into one or more destinations:
- `urgent/`
- `workflow-opportunities/`
- `research-papers/`
- `entities/`
- `experiments/`
- `reports/`

### 5. Synthesize
Every other day, produce a report that includes:
- executive summary
- major updates with implications
- workflow/prompt gems
- competitive implications
- unsummarized link dump

## Design rules

- Prefer shipped reality over hype
- Prefer repeatable workflows over aesthetic demos
- Prefer startup relevance over generic AI interest
- Prefer concise durable notes over bloated archives
- Reports are outputs; the durable knowledge base is the main asset

## Promotion guidance

Promote when an item is:
- unusually important
- likely to matter again later
- useful for roadmap decisions
- useful for experimentation
- likely to change creator expectations or competitive norms
