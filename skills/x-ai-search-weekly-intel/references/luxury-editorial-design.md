# Luxury / Editorial design system

Use this as the design north star for research reports, newsletters, HTML exports, and PDFs.

## Role

Act like an expert frontend engineer, UI/UX designer, visual designer, and typography specialist.

Before changing layout or styling:
- identify the output stack in use (markdown, HTML, CSS, PDF export path)
- inspect existing tokens, spacing, and typography
- centralize repeated styles into reusable tokens or primitives
- prefer maintainability over one-off hacks

## Target aesthetic

Build toward a **luxury light-mode editorial newsletter**.

Reference vibe:
- Vogue
- Harper's Bazaar
- Kinfolk
- Chanel
- Hermès
- Aesop

The feeling should be:
- elegant through restraint
- typographically led
- spacious
- deliberate
- architectural
- premium, tactile, and calm

## Core palette

- Background: `#F9F8F6` (warm alabaster)
- Foreground: `#1A1A1A` (rich charcoal)
- Muted background: `#EBE5DE` (pale taupe)
- Muted foreground: `#6C6863` (warm grey)
- Accent: `#D4AF37` (metallic gold, use sparingly)
- Accent foreground: `#FFFFFF`

Rules:
- never default to pure black or pure white for main surfaces/text
- use charcoal at 10–20% opacity for borders and dividers
- use dark inverted sections sparingly with alabaster text when useful
- never let gold dominate the page

## Typography

### Font pairing
- Heading font: `Playfair Display`
- Body/UI font: `Inter`

### Hierarchy
- Hero headlines: huge, dramatic, tight leading
- Section headlines: still oversized and commanding
- Subsection titles: clear editorial weight
- Body text: comfortable reading size with generous line-height
- Labels / overlines: tiny uppercase with wide tracking
- Metadata: very small, warm grey, understated

### Rules
- let typography do the heavy lifting
- use wide tracking only on labels/buttons, not body text
- keep body text left-aligned
- use mixed italic emphasis in major headlines when it adds cadence
- use drop caps sparingly for intros when it genuinely improves the editorial feel

## Shape and borders

- border radius: `0px`
- edges should feel precise and architectural
- prefer thin 1px borders and single-edge dividers over boxed cards
- use horizontal lines deliberately as editorial structure

## Shadows and depth

- shadows must be soft and subtle
- depth should feel layered, not loud
- use slight inner borders or inset framing on images
- never use harsh drops or glossy UI effects

## Layout

- prefer a 12-column mental model even in static HTML
- use generous padding and vertical breathing room
- avoid cramped sections
- asymmetry is good when intentional, not when messy
- continuous-scroll reading flow is preferred for long reports

## Images

Priority order:
1. official hero / official visual asset
2. official diagram / explainer visual
3. tightly cropped screenshot
4. no image

Rules:
- do not use giant full-page screenshots as filler
- crop screenshots to meaningful regions
- default toward large, elegant, well-framed images
- grayscale-to-color hover is good for website versions, but the static PDF should still look good without hover

## Signature details to keep in mind

These are useful motifs, not mandatory on every page:
- vertical side labels
- decorative short horizontal lines
- visible low-opacity grid lines
- large type contrasted with tiny uppercase metadata
- gold hover/underline accents
- very slow image transitions for web views
- subtle paper/grain texture at very low opacity

## Motion

For web versions:
- interactions should feel slow and deliberate
- most transitions: 500–700ms
- image transitions: 1500–2000ms
- prefer ease-out or smooth custom bezier curves

For PDFs:
- design must stand on its own without motion

## Inputs / buttons / primitives

If creating reusable web components, prefer:
- rectangular button variants
- primary buttons with dark base and restrained gold reveal
- secondary buttons with thin borders and dark-fill hover
- underline-only inputs with italic serif placeholders
- cards defined by top borders and spacing more than by heavy surfaces

## Anti-patterns

Avoid:
- rounded corners
- fast/snappy interactions
- loud color usage
- cramped layouts
- generic dashboard card spam
- giant screenshot dumps
- decorative clutter
- gold as a dominant fill color

## Browser etiquette

When collecting assets:
- reuse tabs where possible
- prefer tabs over windows
- close unused tabs afterward
- do not leave a messy browser state behind

## Export guidance

- design like a website first, then export
- preserve the intended palette in print CSS
- remove accidental white PDF borders
- favor a calm continuous-scroll editorial flow over rigid page segmentation
- structure markdown/HTML so sections do not split awkwardly across pages
- keep headings attached to the content that follows
- avoid orphan lines, isolated bullets, and lonely source links at page tops/bottoms
- use print CSS such as `break-inside: avoid`, `page-break-inside: avoid`, and heading keep-with-next patterns for entries, figures, and callouts
- prefer fewer stronger sections over many tiny fragmented blocks when PDF readability matters
