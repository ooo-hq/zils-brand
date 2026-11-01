# Zils brand: instructions for agents

This repository is the source of truth for how Zils looks: logos, colors, type and the interface system. Read it before building or restyling anything Zils-branded: a page, dashboard, deck, diagram, email or social image.

## Read first

1. [`SYSTEM.md`](SYSTEM.md): surfaces, color roles, type, the quiet hierarchy, components and motion.
2. [`tokens/tokens.css`](tokens/tokens.css): copy these variables instead of retyping hex values. [`tokens/tokens.json`](tokens/tokens.json) has the same values for non-CSS tools.
3. [`README.md`](README.md): logo files and usage, for people outside Zils.

## Rules

- **Name:** write "Zils". Never "ZILS" or "zils", including in page titles, alt text and labels. Mono uppercase labels may uppercase other words, never the wordmark.
- **Logo:** use the SVGs in `logo/` (periwinkle on dark, purple on light, white on photos). Don't retype the name in a gothic font, recolor, stretch or add effects.
- **Type:** Inter Tight for headings (Light 300, tight tracking) and body (400). IBM Plex Mono, uppercase with wide tracking, for labels, nav, buttons, table headers and data. Don't substitute Plex Sans, Inter or a system font for Inter Tight.
- **Color:** use the tokens. Dark is the default. Support light with the `[data-theme="light"]` values. Orange is for the one primary action, focus, LIVE and corner markers, not for decoration.
- **Spectrum:** only for blocks, bars, icon tiles and large numerals. Never as a page or section background.
- **Structure:** gutters and a lighter column between 1 px rails. Each section opens with a numbered section row (see `SYSTEM.md`). Divide cells with lines, not drop shadows.
- **Hierarchy:** one headline and at most one short line per block; the rest goes in collapsed rows. Body text is text-2, never as bright as the headline.
- **Data:** anything labeled live must be live. Don't present sample numbers as real.
- **Motion:** respect `prefers-reduced-motion`; pause continuous animation off-screen.

## Before you finish

- Screenshot dark and light at desktop and 390 px width. Check that nothing scrolls sideways.
- Check text contrast: text-3 and accent text must reach WCAG AA on their surface.
- Search your output for "zils" and "ZILS" outside code identifiers and URLs.

## Keeping this repository current

zils.ai is the live implementation (`ooo-hq/zils-web`, `app/global.css`, `.zs` tokens). When the site's palette, type or components change, update `tokens/`, `SYSTEM.md` and the README tables in the same change, and note the date in the commit message.
