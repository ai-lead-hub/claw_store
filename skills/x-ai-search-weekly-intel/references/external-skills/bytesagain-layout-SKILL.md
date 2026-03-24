Saved reference from community skills archive.
Original source: https://github.com/openclaw/skills/tree/main/skills/bytesagain/layout
Relevance to x-ai-search-weekly-intel: HIGH
Use for: HTML scaffolding, CSS grid/flex layout, spacing systems, responsive structure for visual reports.

---
name: layout
description: "Generate CSS layouts. Use when building grid or flexbox layouts, creating responsive breakpoints, or scaffolding HTML pages."
version: "3.4.0"
author: BytesAgain
homepage: https://bytesagain.com
source: https://github.com/bytesagain/ai-skills
tags:
  - layout
  - css
  - grid
  - flexbox
  - responsive
---

# Layout

Generate CSS Grid layouts, Flexbox containers, responsive breakpoint media queries, page scaffold HTML, and spacing utility classes — all from a single shell script. Analyze existing CSS files for layout property usage.

## Commands

### `grid`
Generate a CSS Grid layout with configurable columns, rows, gap, named areas, and custom templates.

### `flex`
Generate a Flexbox layout with direction, wrapping, alignment, and per-item grow factor.

### `responsive`
Generate mobile-first (`min-width`) and desktop-first (`max-width`) media query breakpoints.

### `scaffold`
Generate a complete HTML page skeleton with semantic sections. Supports four layout types:
- basic
- holy-grail
- dashboard
- landing

### `spacing`
Generate a spacing scale system with CSS custom properties and margin/padding utility classes.

### `analyze`
Analyze an existing CSS file and report layout property usage.

## Why we saved this
For our research PDF workflow, the useful pattern is not the shell script itself — it is the underlying design approach:
- scaffold HTML first
- use semantic sections
- design with grid/flex instead of markdown print styles
- create an explicit spacing system
- treat report layout like a small editorial web page
