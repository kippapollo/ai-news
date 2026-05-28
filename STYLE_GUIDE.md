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

## Content depth — read without leaving the page

The goal is for a reader to consume every story IN FULL from this page, without needing to click through to the source. Each story must be substantial enough to stand on its own.

For every story, the agent MUST:
1. **WebFetch the source URL** (in addition to the WebSearch result snippet) to read what was actually published.
2. **Write a 200–400 word summary in the agent's own words** — not a bullet-list rewrite, but a coherent mini-article covering: what happened, the key facts/numbers, the context, why it matters, and (where relevant) any caveats or open questions.
3. **Optionally include 1–2 short attributed quotes** (1–3 sentences each, in quotation marks with attribution like `— Sam Altman, OpenAI`) when a direct quote adds color or precision the summary can't.
4. **Always link to the source** at the end of the card (`Read source →`) — the deep read should already be on the page; the link is for primary-source verification.

Boundaries:
- **Do NOT republish the source article verbatim or near-verbatim.** Summarize in your own words. Direct quotes are limited to 1–2 short passages per story with clear attribution (fair-use territory).
- If a source is paywalled / blocked / un-fetchable, do your best with the search snippet plus other publicly available context, and add a small `(source paywalled)` italic note in the card footer. Do not fabricate facts to fill space.
- Numbers, names, and dates must come from the fetched content — never invent.

Story-card layout to accommodate the deeper content:
- Headline (1.5–2rem)
- Tag chips (1–2)
- Kicker line: source · publication date
- The 200–400 word summary, set as proper editorial prose with paragraph breaks (typically 2–4 paragraphs)
- Optional pull-quote(s) — set apart visually (left border in accent color, slightly larger font, italic)
- Footer line: `Read source →` link

## Tag filtering (interactive)

The masthead includes a **filter bar** of tag chips that lets the reader pick a tag to scope what's shown on the page. This is the only interactive feature on the site — keep it lean.

Behavior:
- Default state: `All` is active; all stories visible.
- Click a tag chip: show only stories tagged with that tag (including the hero if it matches; if it doesn't match, hide the hero entirely so the page reflows cleanly).
- Click `All` to reset.
- Single-select (clicking a tag deactivates any previously active tag — including `All`).
- Each chip shows a count of stories carrying that tag in this edition. Counts are computed at render time.
- Tags with zero stories in the edition: render the chip in a disabled/dim state and make it unclickable (or omit it entirely — your call, but be consistent).

Implementation:
- Inline `<script>` (vanilla JS, no libraries, no CDN).
- Each filterable story element gets a `data-tags="tech application"` attribute (space-separated).
- Each filter chip is a `<button data-filter="tech">` etc.
- Click handler toggles which chip has `[aria-pressed="true"]`, then iterates story elements and toggles `hidden` attribute based on match.
- Hero is also a filterable element (treat as a story).
- Update the URL hash (`#filter=tech`) on filter change so links are shareable; on page load, read the hash and pre-apply the filter.
- Smooth: no animations needed beyond a 120ms fade-out on hidden elements (CSS transition on opacity then `hidden`).
- Accessibility: chips are `<button>` (focusable, keyboard-operable), use `aria-pressed`, announce filter change via `aria-live="polite"` region (visually hidden text like "Showing 4 of 10 stories — Tech").

Placement & style of filter bar:
- Directly BELOW the masthead identity row, attached to it visually (shared bottom border).
- `position: sticky; top: 0;` so it follows the reader. On mobile, it can be a horizontally scrollable strip if it overflows.
- Background matches page background; thin bottom rule when sticky-stuck (use `box-shadow` to indicate elevation).
- Chips: same uppercase letter-spaced style as tag chips on cards, but slightly larger and with a clear active state (filled with the tag's hue when pressed; outlined when not).
- An `All · 10` chip on the left, then one chip per tag with count, e.g. `Tech · 4`  `Application · 3`  `Economic · 2`  `Policy · 1`.

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
