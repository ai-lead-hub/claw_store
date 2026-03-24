# Design direction for x-ai-search-weekly-intel

These external skill references are now the marked design direction for this workflow:

## Primary references

1. `external-skills/bytesagain-layout-SKILL.md`
2. `external-skills/bytesagain-html-builder-SKILL.md`

These should guide:
- HTML-first report generation
- card/grid section layout
- spacing and visual hierarchy
- palette and typography choices
- responsive structure before PDF export

## Secondary reference

3. `external-skills/agent-friendly-design-SKILL.md`

This should guide:
- semantic HTML
- heading structure
- robust document markup
- accessibility-friendly report scaffolding

## Marked usage for this skill

For future runs of `x-ai-search-weekly-intel`:
- do not treat markdown as the final design surface
- create a proper HTML report with styled sections and images
- use screenshots / scraped visuals from source pages where useful
- render PDF from the designed HTML
- aim for an editorial / briefing-doc feel, not plain export output
