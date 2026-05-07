---
name: founding-creative-design
description: >
  Use this skill to generate on-brand interfaces, prototypes, mocks, decks,
  and production code for Founding Creative. Always fetches the latest design
  tokens, components, and brand guidelines directly from the live GitHub
  repository before doing any creative work.
user-invocable: true
---

## Step 1 — Fetch the live design system

Before doing anything else, read the following files directly from the
canonical repository at `github.com/foundingadmin/DesignSystem-Founding`
(default branch: `main`). Do not rely on any locally bundled or cached copy.

Read in this order:

1. `README.md` — brand voice, visual rules, component patterns, do/don't
2. `CLAUDE.md` — architecture notes, token conventions, branching workflow
3. `DECK.md` — presentation design standard: canvas, fonts, type scale, colour, layouts, and component patterns for every Founding deck
4. `css/tokens.css` — every design token as a CSS custom property
5. `css/components.css` — all reusable component classes
6. `index.html` — living reference showing tokens and components in use

If any file has changed since a previous session, the fetched version is
authoritative. Discard any prior knowledge of values that conflict.

---

## Step 2 — Understand the brand at a glance

After reading the source files, internalise these non-negotiables:

**Voice**
Confident craftsperson. Plain English, no jargon. "We" for the agency,
"you" for the reader. Sentence case everywhere. One italic mint phrase per
headline, never two. No emoji in any shipped surface.

**Palette**
- Canvas: `--n-black` (#000000)
- Primary accent: `--mint` (#7EF893) — used for eyebrows, links, buttons,
  italic emphasis, focus glow
- Holographic spectrum (`--holo-cyan`, `--holo-mint`, `--holo-lavender`):
  hero backgrounds and SiteLaunch cards only — never general UI chrome
- Deep anchors (`--deep-navy`, `--deep-teal`, `--deep-plum`): SiteLaunch
  card backgrounds only

**Typography**
- Display / voice: Gelica Medium 500 (serif). Italic + mint for emphasis.
- Body / UI: Manrope variable (sans). 400 body, 600 UI, 700 eyebrows.
- Eyebrows: 12px Manrope 700, `letter-spacing: 0.16em`, `text-transform: uppercase`, mint colour.

**Key classes**
`.btn`, `.btn--primary`, `.btn--secondary`, `.btn--link`, `.btn--small`
`.chip`, `.chip--mint/cyan/holo-mint/lavender`, `.chip--dot`, `.chip__icon`
`.chip--link`, `.chip--hover-fill/glow/lift/underline`
`.navbar`, `.navbar__nav`, `.navbar__actions`, `.navbar__burger`
`.card`, `.card--case`, `.card--interactive`, `.card--hover-lift/zoom/glow/reveal/tint`
`.holo-bg` (requires four children: `__grad`, `__waves`, `__veil`, `__fade`)

---

## Step 3 — Choose an output mode

**Prototypes / mocks / decks / throwaway artifacts**
- Link `css/tokens.css` and `css/components.css` from the repo (or copy
  inline) and build a self-contained static HTML file.
- Use gradient placeholders where real photography would sit.
- No build tools, no bundler — plain HTML + CSS + vanilla JS only.

**Production code**
- Apply the exact token names and class names from the system.
- Do not invent new color values or font stacks — always resolve to a token.
- Follow the branching workflow in `CLAUDE.md`: new branch → PR → merge.

---

## Step 4 — Stay current

This skill has no expiry and no bundled snapshot. Every session starts with
a fresh fetch from `main`. If you are told the repo has been updated, re-read
the affected files before continuing. The repository is the single source of
truth — not this file, not any prior conversation.

---

## Usage

### Decks

`DECK.md` is the canonical specification for every Founding Creative presentation. It was extracted from the gold-standard BrandForge Gauntlet deck (May 2026) and covers canvas sizing, font stack, type scale, colour palette, layout patterns, and slide-component conventions. Any session generating a Founding deck must read `DECK.md` before writing a single line of HTML.

**What it governs**
- 16:9 canvas at 1280 × 720px logical size, responsive via `aspect-ratio: 16/9`
- Font stack: Gelasio (display), Manrope (body/UI), Roboto Mono (code accent), loaded via Google Fonts CDN
- Full type scale converted from PPT point sizes to HTML px at the 1280px canvas
- Brand colour application: when to use `--mint`, holographic spectrum, deep anchors, and neutral greys
- Named slide layouts (Title, Section Break, Two-Column, Full-Bleed Image, Stats, Timeline, etc.)
- Reusable slide components: eyebrow labels, stat blocks, timeline rails, image frames, and the holographic gradient treatment

**Relationship to the live deck**
Each deck that ships should be logged in `studio.foundingcreative.com` as a project entry. That entry links to two things: the live deck URL and the raw `DECK.md` file on GitHub. This pairing makes `DECK.md` the master record — a team member opening the GTM deck entry sees both the rendered output and the specification that produced it. If the deck is regenerated or handed off to a new session, reading `DECK.md` is sufficient to reproduce the design intent exactly.

**When to use**
Use `DECK.md` (not the general brand guidelines alone) whenever the output is a slide deck, pitch, or presentation — whether built as a standalone HTML file, a Keynote export, or a PowerPoint. The general design tokens in `tokens.css` still apply for colour and spacing, but `DECK.md` overrides or extends them wherever presentation-specific conventions differ.
