# Zils design system

How Zils interfaces look and read. The values come from zils.ai (zils-web `app/global.css`, the `.zs` tokens) and the 18 October 2026 rebrand spec. Use [`tokens/tokens.css`](tokens/tokens.css) or [`tokens/tokens.json`](tokens/tokens.json) for the exact values.

## Feel

A dark, calm instrument panel with a warm-to-cool spectrum: 80s science fiction made quiet. Pages show what Zils does rather than telling a story about it.

Avoid:

- Busy pages: background text, long explanations, or body text as bright as the headline.
- Synthwave clichés: sunsets over grid floors, amber CRT headers, LED-dot horizons, full-page gradient washes.
- Fake data presented as live. Anything labeled live must be live.

## Surfaces and structure

Two surfaces: dark **gutters** at the sides and a slightly lighter **column** between them, separated by 1 px rails. Together they read as one panel instead of text floating on black.

- Gutters are 56 px on desktop. Below 900 px they collapse to 0 and the column keeps a 16 px inner margin.
- Inside the column, cells are divided by 1 px lines (`--zils-line`). Notices use a dashed rule.
- Consoles, cards and hovered rows use the raised surface (`--zils-raised`).

**Section row.** Each section starts with a 40 px row: the section number in the left gutter (`01`, `02`, …), a mono uppercase label, an optional right-aligned note, and a small orange corner triangle at the column's top-left edge.

```css
.section-row { position: relative; display: flex; align-items: center; height: 40px; border-bottom: 1px solid var(--zils-line); font-family: var(--zils-font-mono); text-transform: uppercase; }
.section-row .n { width: 56px; margin-left: -56px; text-align: center; font-size: 10px; color: var(--zils-text-3); }
.section-row .label { padding-left: 24px; font-size: 10.5px; letter-spacing: .14em; color: var(--zils-text-2); }
.section-row .note { margin-left: auto; padding-right: 20px; font-size: 10px; letter-spacing: .12em; color: var(--zils-text-3); }
.section-row .corner { position: absolute; left: 0; top: 0; border-style: solid; border-width: 7px 7px 0 0; border-color: var(--zils-orange) transparent transparent transparent; }
@media (max-width: 899px) { .section-row .n { margin-left: 0; width: 28px; } .section-row .label { padding-left: 8px; } .section-row .note { display: none; } }
```

## Color

| Token | Dark | Light | Use |
|---|---|---|---|
| gutter | `#0f0f13` | `#ecebf1` | page sides, footer, nav (92% opacity with blur) |
| panel | `#18191e` | `#faf9fc` | content column |
| raised | `#1d1e24` | `#f1eff6` | consoles, cards, hover rows |
| line | white 7% | `#1c1a26` 10% | rails, rows, cell borders |
| text-1 | `#e8e6ef` | `#1c1a26` | headings, key numbers |
| text-2 | text-1 at 58% | text-1 at 70% | body |
| text-3 | text-1 at 54% | text-1 at 64% | labels, captions |
| logo | `#8f88ff` | `#4b44c8` | the wordmark |
| orange | `#ff7a2f` | `#ab4d25` | the one primary button, LIVE, corner markers, focus and active accents |
| peri | `#a9b5f2` | `#4a5fc4` | cool accents in text |
| bad | `#ff8f6b` | `#b4452a` | errors and failed states |

Light mode uses deeper accents so text in those colors stays readable (WCAG AA).

**The spectrum** is one gradient, warm to cool: `#ef8d5a` → `#d9a08c` → `#cfa2e4` → `#c3b4f6` → `#a9b5f2` → `#8ea6ff`. Orange is its warm end, so orange belongs to the gradient rather than standing apart. Use it for blocks, bars, icon tiles and large numerals, optionally with a fractal-noise grain at about 35% in overlay blend. Never use it as a page background. For gradient text in light mode use `--zils-spectrum-text`, a deepened version that reaches 3:1.

**Lane colors are fixed.** An answer has the same color wherever it appears: Billing `#f08a4b`, Spam `#e7a58f`, Account changes `#d7a6e8`, Technical support `#c3b2f6`, Sales `#a9b5f2`, Needs review `#8ea6ff`.

## Type

| Role | Font |
|---|---|
| Logo | Grenze Gotisch Semibold, the wordmark only. Use the SVGs in [`logo/`](logo/). |
| Headings | Inter Tight Light 300, tracking −0.02 to −0.03 em |
| Body | Inter Tight Regular 400 |
| Labels, nav, buttons, data | IBM Plex Mono, uppercase, 0.1–0.14 em tracking for labels |

Display sizes: page H1 `clamp(44px, 6vw, 84px)`, section H2 `clamp(28px, 3.2vw, 44px)`. Numbers use tabular figures.

The wordmark must never be uppercased by an inherited style. Write the name as **Zils** in text, never "ZILS" or "zils".

## The quiet hierarchy

- Only headings and key numbers use text-1. Body is text-2. Labels are text-3.
- One headline and at most one short line per block. Longer explanations, methods and caveats go in collapsed rows.
- The headline comes first, then the main action, then one visual. Everything else is quiet or collapsed.

## Components

- **Nav:** sticky, 64 px. Logo left; links at the true page center; theme toggle and one outlined button right. The active page gets an orange underline.
- **Buttons:** primary is orange fill with dark text (white text in light mode); secondary is outlined. Both use uppercase mono. One primary button per view.
- **Collapsed rows:** full width, mono uppercase summary with a peach `+` / `−`.
- **Tables:** mono uppercase headers, generous row height, tabular figures, rows lift to the raised surface on hover.
- **Answer tag:** a box with a hatched square on its left holding a tiny confidence number, then the label in uppercase mono. When a decision lands, the square fills with the lane color.
- **Result strip:** two thin bars (Zils as spectrum, the comparison as hatched grey) with counts, then the difference in large light numerals.
- **Hatching** marks the comparison and the empty state: the result strip's comparison bar and the answer tag's square before a decision lands.

## Motion

- Sections fade up 16 px over 0.8 s when they scroll into view; cells stagger by about 110 ms.
- Bars fill from the left over about 1.4 s while their percentages count up.
- Continuous animations pause when off-screen or when the tab is hidden.
- `prefers-reduced-motion`: no fades, fills or counting. Everything renders in its final state.

## Light and dark

Dark is the default when no choice is saved. A sun/moon toggle switches themes, and the choice persists across pages. Every token above has a light value; never hard-code a dark-only color.
