# Apollo AI News — Design System

Reference for the Apollo AI News Bot. Every generated HTML page (homepage and per-cadence editions) MUST follow this guide. Self-contained, editorial-quality, no external dependencies.

## Brand

- **Publication name**: `Apollo AI News` (display form). The wordmark and sun-mark are locked.
- **Logo**: lives at repo root as `logo.svg`. Agent MUST read this file and INLINE its contents inside the masthead link on every page. Do NOT redesign the logo per edition — it is the brand mark.
- **Favicon**: lives at repo root as `favicon.svg`. Same rule: do not regenerate.
- **Brand accent** (fixed, used in logo and favicon only): burnt orange `#c2410c`. This is separate from the per-edition accent color which rotates.

Page `<title>` format: `Apollo AI News — Daily · YYYY-MM-DD` (substitute cadence + date/period).
Meta description: 1–2 sentences derived from the Big Picture lede.

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
- Includes a favicon link: `<link rel="icon" type="image/svg+xml" href="…/favicon.svg">`. From `index.html` use `href="favicon.svg"`; from cadence pages (in subdirectories) use `href="../favicon.svg"`. The favicon file lives at the repo root and stays constant across editions — do NOT regenerate it.

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

## Voice & prose

The writing must not read like AI slop. Follow these rules in every paragraph the agent writes (leads, story summaries, themes, callouts).

**Cut the throat-clearing.** No openers like `Here's what happened`, `It's worth noting`, `In a significant development`, `As the AI landscape evolves`, `In the past 24 hours we've seen`. Start with the fact.

**No em dashes.** Use periods, commas, or colons. The em dash is the single strongest AI tell. If a sentence wants an em dash, split it.

**Active voice, named actor.** `Anthropic raised $30B at a $900B valuation` — not `$30B was raised at a $900B valuation`. Not `The funding emerged from a Series F` — say who led it. Inanimate things do not take human verbs (`The decision indicates...` → name the decider).

**Drop the adverbs.** `notably`, `significantly`, `dramatically`, `crucially`, `arguably`, `interestingly`, `largely`, `essentially`, `effectively`, `actually`, `simply`, `clearly`. Strip them on the editing pass. The verb should carry the weight.

**No vague intensifiers.** `significant`, `substantial`, `key`, `critical`, `major`, `historic`, `unprecedented`, `groundbreaking`, `paradigm-shifting`, `game-changing`. Say the number, the comparison, or the consequence. `The third-largest seed round on record` beats `a significant raise`.

**No "not X, but Y" / "It's not just X — it's Y".** State Y directly.

**Skip the rhetorical questions.** No `What does this mean for AI?` No `So why now?` Tell the reader.

**No meta-paragraphs about meaning.** Cut `Here's why this matters`, `The implications are far-reaching`, `Looking ahead, the question becomes`. If the importance isn't obvious from the facts, you haven't reported enough facts. The reader infers significance from concrete detail.

**Vary sentence length.** Two short sentences in a row, then one long one. Don't end every paragraph with a punchy fragment.

**Two beats three.** When listing, two items often reads cleaner than three. Don't pad to a list of three for cadence.

**Trust the reader.** No `Importantly`, `Of course`, `Naturally`. No hedging filler (`it should be noted that`, `as one might expect`). State the thing.

**Pull-quotes earn their place.** Only include a pull-quote when the source's exact phrasing carries information your summary cannot. If a quote sounds like marketing or generic punditry, cut it.

**For "Big Picture" / lede paragraphs specifically:** Open with the single most consequential new fact, in one sentence. Add 2–4 sentences of concrete context (numbers, names, comparisons). Don't restate the headlines that follow.

**For "Themes" sections (weekly+):** Each theme is a noun phrase naming a concrete pattern, not a vibe (`Hyperscalers move on custom silicon` > `Shifting compute dynamics`; `Frontier labs price-cut against open weights` > `Pricing pressure intensifies`). The theme paragraph then names the specific instances inside the period that show the pattern.

**For headlines:** active verb, concrete numbers, no labels (`Cognition raises $1B at $26B` not `MAJOR FUNDING: Cognition closes Series F`). 6–14 words.

If a paragraph could appear in any AI news roundup without changing a word, rewrite it.

## Content depth — read without leaving the page

The goal: a reader consumes every story IN FULL from this page without ever needing to click to the source. Each expanded story is a comprehensive own-words retelling that captures everything the source article reports.

For every story, the agent MUST:

1. **WebFetch the source URL** and read the actual article in full (not just the search snippet).

2. **Inventory the source.** Extract every concrete data point: every dollar amount, percentage, growth rate, headcount, model name, version number, named person and role, date, quote, comparison, methodology detail, caveat, and downstream consequence the article mentions. The reader must come away knowing what someone who read the source knows.

3. **Write a comprehensive 800–1500 word retelling in the agent's own words.** Coherent editorial prose, multiple sections if useful (with `<h4>` subheads inside the `<details>` content). Cover:
   - What happened (the news itself)
   - The numbers, names, and concrete facts from the source
   - The context (what came before, what the actors had previously said or done)
   - The mechanics or method (how the thing works, if relevant)
   - Caveats, dissenting voices, open questions, and limitations the article notes
   - Downstream implications the article identifies

4. **Include 4–8 short attributed direct quotes** (1–3 sentences each, in quotation marks with attribution like `— Dario Amodei, Anthropic CEO`). Use quotes for: the source's most precise wording on a key claim, statements that carry their speaker's voice, numbers stated in direct address, dissent or pushback. Distribute quotes across the piece rather than clustering them.

5. **Footer:** end with `Read source →` link for primary-source verification.

Fair-use boundaries:
- The retelling is the agent's own composition. **Do NOT paste paragraphs of source text into the prose.** Each direct quote is bounded to 1–3 sentences and clearly attributed.
- Numbers, names, dates, and quotes must come from the fetched content. Never invent.
- If a source is paywalled, blocked, or un-fetchable: write what you can from the search snippet and any other publicly available context, then mark `(source paywalled — partial coverage)` in italic at the bottom of the card. Do not fabricate to fill space.

**Per-story SVG thumbnail (always visible, in the summary row):**

Each non-hero story card carries a small **generative SVG thumbnail** (~120×80px) inside the summary row, alongside the headline. The thumbnail is unique to the story — its composition is invented by the agent for that specific story — and stays visible in both collapsed and expanded states.

Purpose: visual scanability. A reader skimming the page sees a column of distinct marks next to headlines and recognizes stories at a glance.

Rules:
- Abstract / geometric / typographic. NOT literal illustrations, NOT company-logo lookalikes, NOT emoji-like icons. Think Swiss editorial design: shapes, marks, simple invented iconography that suggests the story's subject without depicting it.
- Uses the per-edition accent color + neutrals only. No third color.
- Distinct per story — never reuse the same composition across cards in one edition.
- Inline SVG, viewBox roughly `0 0 120 80` (proportions can vary a little for hero/feature stories). Width on desktop ~120px.
- `aria-hidden="true"` and `role="presentation"` (decorative).
- Composition idea generators: split-rect + connector, layered arcs, dot-field with one accented dot, two intersecting shapes, axis + plotted point, stacked bars, numeric glyph treatment (the year, the percentage, the dollar amount as a typographic mark), contour pattern, etc. Pick something that resonates with the story.

Story-card layout (summary row):
- CSS grid: `grid-template-columns: 120px 1fr; gap: 1.25rem;` on desktop.
- Thumbnail in the left column, vertically aligned to the headline.
- Right column: tag chips + headline + kicker + teaser + expand control.
- On narrow screens (<600px): single column, thumbnail above the headline at full width (clipped to a thinner aspect ratio like 320×80).
- Hero story uses the larger `hero-art` treatment (existing) — no separate small thumbnail needed for the hero.

**Story-card UX — collapsed by default, expand inline:**

Stories use a progressive-disclosure pattern so the page reads as a scannable index. Implement with the native `<details>` element so it works without JS, then enhance with CSS for smooth expansion.

Collapsed state (always visible — what shows by default):
- Tag chip(s) (1–2)
- Headline (1.5–2rem)
- Kicker line: source · publication date · small `Source ↗` external link (subtle, for verification)
- 1–2 sentence **teaser** drawn from the summary — concrete, not "click to read more"-style filler
- Expand control labeled `Read in full ▾` (button-styled, accent-color hover)

Expanded state (revealed when reader clicks the expand control):
- The full 200–400 word own-words summary (2–4 paragraphs of editorial prose)
- Optional pull-quote(s) — set apart visually (left border in accent color, slightly larger font, italic, attribution line beneath)
- A bottom `Read source →` link (full version of the kicker link)
- Collapse control labeled `Collapse ▴`

Implementation:
```html
<details class="story" data-tags="tech application">
  <summary>
    <div class="tag-row">…tag chips…</div>
    <h3 class="headline">…</h3>
    <p class="kicker">Source name · 2026-05-28 · <a href="…" target="_blank" rel="noopener">Source ↗</a></p>
    <p class="teaser">1–2 sentence teaser.</p>
    <span class="expand-control">Read in full ▾</span>
  </summary>
  <div class="full-content">
    <p>…200–400 word summary…</p>
    <blockquote class="pull-quote">"…" <cite>— Attribution</cite></blockquote>
    <p class="source-footer"><a href="…" target="_blank" rel="noopener">Read source →</a></p>
  </div>
</details>
```

CSS notes:
- `details > summary { list-style: none; cursor: pointer; }` and `summary::-webkit-details-marker { display: none; }` — hide the default browser triangle (you have your own ▾/▴ glyph in the expand control).
- Style the expand-control inside `summary` to look like a quiet text button; change its text content via CSS using `details[open] summary .expand-control::before { content: "Collapse ▴"; }` and matching default — OR via inline JS that flips text on toggle. Either is fine; choose what reads cleaner.
- Smooth open/close: use `details[open] .full-content` with a `transition: opacity 180ms ease, transform 180ms ease;` and a small upward slide-in.

Filter interaction: tag filters operate on the OUTER `<details>` element via `data-tags`. Filtered-out stories are `hidden`; remaining stories stay in whatever collapsed/expanded state the reader left them in.

Hero behavior: the LEAD story is also a `<details>` with the same UX, but it MAY be `<details open>` by default if the cadence is daily (lead story expected to be read). For weekly+ cadences, lead also defaults collapsed to keep the page index-like. Pick what reads better per cadence.

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
| **Tech** | Model releases, research, benchmarks, infrastructure. Covers six sub-areas the agent must continuously sweep: **(1) Frontier models** (Anthropic, OpenAI, Google DeepMind, Meta, xAI, Mistral, Cohere, Inflection, etc. — new releases, capability jumps, benchmark results, scaling work); **(2) Open-source models** (Llama, Qwen, DeepSeek, Mistral OSS, Phi, Gemma, OLMo, Yi — releases, fine-tunes, license shifts, leaderboards); **(3) Agents** (agent frameworks, tool-use systems, planning research, browser/computer-use agents, multi-agent systems, agent evaluation); **(4) Frameworks** (inference engines like vLLM/llama.cpp/Ollama; orchestration like LangChain/LlamaIndex; protocols like MCP; SDKs; training stacks); **(5) Research** (papers, methods, evaluations, alignment, interpretability, scaling laws, novel architectures); **(6) General tech** (hardware: chips, datacenters, networking, power; compilers, kernels, low-level tooling). | blue family |
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
   - **Inline the contents of `logo.svg`** (read the file from repo root) inside an `<a href>` link to the homepage. From cadence pages use `<a href="../index.html">`; from `index.html` use `<a href="./">` or `<a href="index.html">`. The link has no underline but is a real `<a>` with hover/focus states. The logo IS the publication wordmark + sun mark — do not add separate "AI NEWS" text alongside it.
   - Thin rule below the masthead row (1–2px, per-edition accent color — NOT the fixed brand accent)
   - Edition info on the right side of the masthead row: cadence label + date/period (tabular nums)

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

- Same masthead identity as article pages (inlined `logo.svg`, same palette family).
- **HERO**: feature the most recent edition prominently. Hero card with date, a "Big Picture" excerpt (~150–200 chars) drawn from the latest edition, CTA `Read today's briefing →`. Adapt a hero SVG motif.
- **ABOUT** (placed directly below the hero, before the archive): a short editorial section headed `What is Apollo AI News?`. 3–5 sentences in the agent's own voice covering:
  - The site publishes daily, weekly, monthly, quarterly, and annual AI-news editions.
  - Each edition is written to be read end-to-end on the page itself — no clicking through to sources required.
  - Coverage is tagged by category (Tech, Application, Economic, Policy, Safety, Trend) and the masthead filter lets the reader scope to one tag.
  - The site is generated and published automatically by a Claude Opus 4.7 agent that searches the web, reads source articles, and writes the summaries.
  - Apply Voice & Prose rules — factual and brief, no marketing language, no "we believe", no superlatives, no first-person plural posturing.
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
