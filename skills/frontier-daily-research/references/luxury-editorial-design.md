# Luxury Editorial Report Design

Use this design direction for research reports, newsletters, and PDF exports.

## Role

Be an expert frontend engineer, UI/UX designer, visual design specialist, and typography expert. Integrate the design system into the existing report workflow in a way that is visually consistent, maintainable, and idiomatic to the stack.

Before changing layout or styling:
- identify the current output stack (markdown, HTML, CSS, PDF export path)
- inspect existing typography, spacing, color choices, and layout patterns
- respect maintainability over one-off styling hacks
- prefer reusable layout and typography tokens

## Design target

Build toward a **luxury light-mode editorial newsletter** aesthetic.

Reference vibe:
- Vogue
- Harper's Bazaar
- Kinfolk
- Chanel
- Hermès
- Aesop

Core traits:
- elegance through restraint
- strong typography hierarchy
- generous whitespace
- precise spacing
- subtle depth
- intentional asymmetry only when it improves the composition
- slow, deliberate feeling rather than loud UI

## Non-negotiables

- Keep the reading flow primary.
- Remove anything decorative that does not improve comprehension.
- Preserve or improve accessibility.
- Make layouts responsive and export-friendly.
- Make the report feel like a high-end website printed to PDF, not a markdown dump.

## Color direction

Primary light-mode palette:
- Background: `#F9F8F6` (warm alabaster)
- Foreground: `#1A1A1A` (rich charcoal)
- Muted background: `#EBE5DE` (pale taupe)

Use dark text on warm light backgrounds by default.
Avoid burnt-out pure white where possible.

## Typography direction

- let typography do the heavy lifting
- create obvious hierarchy between title, section heads, item heads, body, captions, and metadata
- keep line lengths comfortable
- use stronger editorial spacing between sections
- avoid dense dashboard-like card grids unless the content truly needs them

## Image policy

Image priority order:
1. official hero / official visual asset
2. official diagram / explainer image
3. tightly cropped screenshot of the meaningful area
4. no image

Never use giant full-page screenshots as filler.
If using screenshots:
- crop tightly
- prefer fixed aspect ratios like 16:9, 4:3, or square
- show the part that matters, not the entire scroll

## PDF / export policy

- prefer continuous-scroll HTML structure
- keep page segmentation visually soft
- remove accidental white export borders
- use print CSS that preserves the intended palette and spacing

## Browser etiquette for research capture

- prefer reusing existing tabs
- open a new tab rather than a new window
- close unused tabs after capture is complete
- do not leave tab clutter behind

## Working style

Think like designing a website first, then exporting it.
Aim for a premium newsletter or editorial brief, not a generic report template.
