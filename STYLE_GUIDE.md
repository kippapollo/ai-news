# AI News — Design System

Reference for the AI News Bot. Every generated HTML page (homepage and per-cadence editions) MUST follow this guide. Self-contained, editorial-quality, no external dependencies.

## Philosophy

Aim for the visual quality of editorial publications like The Verge, Stratechery, The Information, Pirate Wires — not a generic blog template. Every page should feel intentional, hand-typeset, with strong typographic hierarchy. Beauty over busyness; restraint over noise.

## Hard constraints

- SINGLE self-contained HTML file per page.
- NO external resources: no CDN scripts, no Google Fonts, no `<img src="https://...">`, no third-party iframes, no analytics, no tracking pixels.
- All visuals are INLINE SVG or pure CSS.
- All fonts are system fonts.
- Semantic HTML5: `<article>`, `<header>`, `<main>`, `<section>`, `<footer>`.
- Responsive (360px → 1400px+).
- Print-friendly (no fixed positioning; links visible in print).
- Light AND dark mode via `@media (prefers-color-scheme: dark)`.
- Includes `<meta name="viewport" content="width=device-width, initial-scale=1">` and `<meta name="description">`.

## Typography

- **Headlines**: system serif `Georgia, "Times New Roman", Charter, serif` OR commit to a sans display `system-ui, -apple-system, "Segoe UI", sans-serif`. Pick one direction per page and stay consistent.
- **Body**: sans-serif system stack `system-ui, -apple-system, "Segoe UI", Roboto, Helvetica, Arial, sans-serif`.
- **Line-height**: 1.6–1.7 body; 1.1–1.2 display headlines.
- **Letter-spacing**: tighter (-0.01em to -0.02em) on large headlines, default on body.
- **Tabular numerals on dates**: `font-feature-settings: "tnum"`.
- **Body size**: ~18px desktop, scaled responsively.

## Color & palette

- Warm off-white background: `#f7f5ef` (NOT pure white).
- Deep ink text: `#11151a` (NOT pure black).
- Muted secondary text: `#5a6068`.
- ONE accent color per edition — sophisticated, saturated but mature. Pick from:
  - Burnt orange `#c2410c`
  - Deep teal `#115e59`
  - Navy `#1e3a8a`
  - Wine `#881337`
  - Forest `#166534`
  - Aubergine `#6b21a8`

  Use the accent SPARINGLY: SVG decorations, link hover, masthead rule, category chips. NEVER in body text. **Rotate the accent per edition** so consecutive issues feel distinct.

- **Dark mode** via `@media (prefers-color-scheme: dark)`: background `#15181c`, text `#e6e3dc`, secondary `#9a9690`, accent stays vivid (may shift one notch lighter for contrast).

## Story tagging

Every story (hero AND cards) is tagged with **1–2** category tags drawn from this fixed taxonomy:

| Tag | Meaning | Accent hue family |
|---|---|---|
| **Tech** | Model releases, research papers, benchmarks, infrastructure (chips, datacenters, compute) | blue family |
| **Application** | Products, features, integrations, real-world deployments, user-facing launches | teal family |
| **Economic** | Funding rounds, M&A, IPOs, revenue, leadership changes, market moves | green family |
| **Policy** | Regulation, legislation, lawsuits, government action, geopolitics, export controls | amber family |
| **Safety** | AI safety/alignment, incidents, misuse, security, content moderation | red family |
| **Trend** | Meta-narratives, broader industry shifts, cultural moments, cross-cutting analysis | purple family |

Rules:
- Assign 1 tag if the story fits cleanly; up to 2 if it genuinely spans categories. Never more than 2.
- Pick the most specific applicable tag — e.g. "OpenAI raises $40B" is **Economic** (not Trend); "EU AI Act enforcement begins" is **Policy** (not Trend); "GPT-6 released" is **Tech**, optionally + **Application** if it launches simultaneously in ChatGPT.
- Render tags as small **uppercase letter-spaced chips** (font-size ~0.7rem, letter-spacing 0.08em) with subtle tinted backgrounds — each tag family has its own muted hue. Keep them quiet — they support the headline, they don't compete with it. Solid chips in light mode, slightly more saturated in dark mode.
- Tags appear: on each story card (above or below the headline), in the hero (kicker line above the lead headline), and as filter-style summary chips on the homepage hero/footer (e.g. "Today's edition: 4 Tech · 3 Application · 2 Economic · 1 Policy").
- Tag colors are SEPARATE from the per-edition accent color. Tag colors stay consistent across editions so readers learn them; the per-edition accent color rotates for variety.

## Required visual elements (every article page)

1. **MASTHEAD** — top-of-page identity bar:
   - Publication name `AI NEWS` in strong typography (uppercase, letter-spaced)
   - A small INLINE SVG decorative mark (~40–60px, abstract/geometric)
   - Thin rule below (1–2px, accent color)
   - Edition info: cadence label + date/period (tabular nums)

2. **HERO** — above-the-fold treatment for the LEAD/most-important story:
   - Large editorial headline: `clamp(2rem, 5vw, 3.5rem)`
   - Dek (subhead) summary
   - Source pill / kicker
   - A **generative INLINE SVG hero graphic** occupying ~30–50% of the hero area. Use gradients, geometric shapes, abstract waves, dot fields, contour lines, isometric forms, or similar generative-art motifs. **Vary the SVG per edition** — do not copy the same shape every day; it should feel hand-composed for this issue. Use the accent color and neutrals only.

3. **BIG PICTURE / OVERVIEW** — the lede paragraph(s):
   - Distinct typographic treatment: larger body size, oversized first letter or italic drop-cap
   - Visually separated from the rest with whitespace and a divider motif

4. **STORY CARDS** — for non-hero stories:
   - Headline: 1.25–1.5rem, bold
   - Summary paragraph
   - Footer line: source · date · `Read source →` link (`target="_blank" rel="noopener"`)
   - Generous spacing; subtle card frame OR strong whitespace separation — pick one approach and use it consistently within a page

5. **SECTION DIVIDERS** — between major sections, use small INLINE SVG ornaments (not plain `<hr>`): dots, diamonds, asterism, or other typographic ornaments. ~20–40px.

6. **FOOTER / COLOPHON**:
   - "AI News" + edition info + "Generated [date]"
   - Back-to-home link (`../index.html`) on per-cadence pages

## Homepage (`index.html`) specifics

- Same masthead identity as article pages (same SVG mark style, same palette family).
- **HERO**: feature the most recent edition prominently. Hero card with date, a "Big Picture" excerpt (~150–200 chars) drawn from the latest edition, CTA `Read today's briefing →`. Adapt a hero SVG motif.
- **ARCHIVE**: list ALL editions found in `daily/`, `weekly/`, `monthly/`, `quarterly/`, `yearly/` — grouped into 5 labeled sections (`Daily / Weekly / Monthly / Quarterly / Annual`). Within each, newest first. Two-column responsive grid (single column on mobile). Each edition as a small card with date/period + small accent chip noting cadence.
- Cadences get slightly different accent chip colors so they're distinguishable, but the OVERALL palette stays unified within one rendering of the index.

## Longer cadences (monthly, quarterly, yearly)

In addition to the above:
- **Table of contents** with anchor links at the top (after hero, before body).
- **Themes section**: each theme as a card or pull-quote treatment, possibly with its own small SVG glyph.
- Yearly may use a wider hero (full-bleed gradient + SVG) and feel more like a magazine cover.

## Anti-patterns to avoid

- Generic Bootstrap-looking cards with default drop shadows.
- Pure black on pure white.
- Multiple competing accent colors on one page.
- Emoji icons in place of real visual design.
- Centered narrow body text (left-align is editorial standard).
- Walls of plain text without typographic structure.
- External fonts (Google Fonts CDN) or external images.
- Decorative SVG that's identical on every edition — regenerate per issue.
- Lorem-ipsum-shaped filler — every word earns its place.
