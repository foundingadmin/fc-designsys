# DECK.md — Founding Creative Presentation System

> Extracted from the gold-standard BrandForge Gauntlet PPT (May 2026).
> This file lives alongside CLAUDE.md and SKILL.md in the design system repo.
> Any AI session generating a Founding deck must read this file before writing a single line of HTML.

---

## 1. Canvas

| Property | Value |
|---|---|
| Aspect ratio | 16:9 |
| Native PPT size | 10" × 5.625" (9144000 × 5143500 EMU) |
| HTML target | 1280 × 720px logical canvas |
| Scale factor | Use `aspect-ratio: 16/9` with `width: 100%` — never hard-code px |
| Background | Full-bleed image or solid fill — no bare white |

The deck lives as a single HTML file with keyboard/click navigation. Each slide is a `<section class="slide">` absolutely positioned or scroll-snapped. Slide canvas is always 16:9.

---

## 2. Fonts

Exact fonts embedded in the PPT. Use Google Fonts CDN equivalents for HTML.

| Role | PPT Typeface | HTML Equivalent | Weight |
|---|---|---|---|
| Display headline | Gelasio Medium | `Gelasio` (Google Fonts) | 500 |
| Display emphasis | Gelasio SemiBold | `Gelasio` | 600, italic |
| Body / UI primary | Manrope | `Manrope` (Google Fonts) | 400 |
| Body medium | Manrope Medium | `Manrope` | 500 |
| Body semibold | Manrope SemiBold | `Manrope` | 600 |
| Body light | Manrope Light | `Manrope` | 300 |
| Code / mono accent | Roboto Mono Medium | `Roboto Mono` (Google Fonts) | 500 |
| Supporting UI | Roboto | `Roboto` (Google Fonts) | 400/600 |

Google Fonts import (always include this):
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Gelasio:ital,wght@0,400;0,500;0,600;1,400;1,500;1,600&family=Manrope:wght@300;400;500;600;700&family=Roboto+Mono:wght@500&family=Roboto:wght@400;600&display=swap" rel="stylesheet">
```

---

## 3. Type Scale

PPT stores sizes as hundredths of a point. Conversion: `sz / 100 * (96/72) = px`.

| Use | PPT sz | Points | HTML px (at 1280px canvas) | Font |
|---|---|---|---|---|
| Section divider title | 6300 | 63pt | 84px | Gelasio 500 |
| Cover / closing hero | 4320–4520 | 43–45pt | 57–60px | Gelasio 500 |
| Statement headline | 2620 | 26.2pt | 35px | Gelasio 500 |
| Body headline | 2220 | 22.2pt | 30px | Manrope 500 |
| Sub-headline | 1920 | 19.2pt | 26px | Manrope 500 |
| Large label / eyebrow | 1200–1300 | 12–13pt | 16–17px | Manrope 700 |
| Body copy | 1000–1120 | 10–11.2pt | 13–15px | Manrope 400 |
| Small label / tag | 700–900 | 7–9pt | 9–12px | Manrope 600 |
| Footer / legal | 500 | 5pt | 6.7px | Manrope 400 |

Scale all sizes proportionally when the viewport is not 1280px wide. Use `clamp()` or `vw`-based units.

---

## 4. Color Palette

Extracted from all slide XML. These are the actual hex values used.

### Core

| Name | Hex | Usage |
|---|---|---|
| Black | `#000000` | Primary background (dark slides) |
| White | `#FFFFFF` | Primary text on dark, background on light slides |
| Off-white | `#EFEFEF` | Light surface, subtle dividers |
| Mid grey | `#CCCCCC` | Muted text, secondary dividers |
| Dark grey | `#999999` | Dimmed / secondary body text |
| Dimmer grey | `#666666` | Tertiary text, captions |
| Ink | `#434343` | Text on light backgrounds |

### Accent (mint family — primary brand signal)

| Name | Hex | Usage |
|---|---|---|
| Mint highlight | `#C9FFDC` | Text highlight background (the "marker" effect on key words) |
| Mint bright | `#5AFE94` | Bold accent, icon fill, active states |
| Mint glow | `#7EF893` | Brand mint (matches design system token `--mint`) |

### Holo / spectrum (section color accents)

| Name | Hex | Usage |
|---|---|---|
| Holo cyan | `#A4FCFF` | Cyan section accent |
| Holo blue | `#8FDBFC` | Blue section accent |
| Holo lavender | `#C9CCFF` | Lavender section accent |
| Holo purple | `#AD97FF` | Deep purple accent |
| Holo pink | `#FFC8D2` | Pink section accent |
| Holo yellow | `#FED05A` | Amber/yellow accent |
| Holo cream | `#FFF0C9` | Warm cream accent |
| Holo lilac | `#F9E3FF` | Soft lilac accent |

These holo colors appear as tag/chip backgrounds and section card backgrounds. One color per section, used sparingly.

---

## 5. Layout Grid

Derived from guides in `presentation.xml` and text box positions across all slides.

```
Slide: 1280 × 720px
─────────────────────────────────────────────────────────────────
Top margin:    ~37px  (guide: 288 units)
Left margin:   ~37px  (guide: 288 units)
Right margin:  ~37px
Bottom margin: ~37px
Footer zone:   663–720px (last ~57px reserved for footer bar)

Column midpoint: ~571px (near the 4080150 EMU divider line in slide 2)
─────────────────────────────────────────────────────────────────
```

**Headline zone (content slides):** starts at y=119px, x=64px, spans 88% of width.
**Body zone:** starts at y=278px, x=148px (indented ~85px from left edge on two-col layouts).
**Logo position (cover):** x=63px, y=64px (top left).
**Footer position:** y=663px, full width. Left = confidential text. Right = "Founding Creative | Raise your flag™ | [slide#]".

---

## 6. Slide Types

18 slides in the source deck. These are the canonical patterns.

### Type A — Cover

**Background:** Full-bleed image (dark/photographic), with a large visual element cropped right.
**Elements:**
- Wordmark logo top-left (63px, 64px)
- Title block, bottom-left quadrant: Gelasio Medium, 59px, white, line-height 80%
- Subtitle line: Manrope 400, 20px, white (the named deck/product)
- CTA pill bottom-center: semi-transparent white rounded rect, keyboard nav label inside
- Footer: copyright left, "Raise your flag™" right

```html
<section class="slide slide--cover">
  <img class="slide__bg" src="[bg-image]" alt="">
  <img class="slide__logo" src="[wordmark-white.svg]" alt="Founding Creative">
  <div class="slide__title-block">
    <h1 class="t-display">From Zero to Market-Ready</h1>
    <p class="t-subtitle">The BrandForge Gauntlet.</p>
  </div>
  <div class="slide__footer">
    <span class="t-legal">©2026 Founding Creative. All rights reserved. Confidential and proprietary.</span>
    <span class="t-legal">Raise your flag™</span>
  </div>
</section>
```

---

### Type B — Statement (hero sentence)

**Background:** Dark (black or near-black). Full bleed.
**Elements:**
- Large Gelasio headline, white, top half of slide (~y=119px)
- Key phrase in *italic Gelasio SemiBold* with mint highlight (`#C9FFDC` text color, or `background: #C9FFDC; color: #000`)
- Below headline: two-column contrast block (muted grey "The Problem" vs white "The Founding Solution")
- Section divider line between columns
- Footer bar (persistent on all non-cover slides)

Key pattern: inline text highlight on emphasis words — black text on `#C9FFDC` mint background, applied to 1-2 words per paragraph maximum.

```html
<section class="slide slide--statement">
  <h2 class="t-hero">Most startups die in <em class="highlight">the gap</em>.</h2>
  <div class="slide__two-col">
    <div class="col col--muted">
      <p class="t-label">The Problem:</p>
      <p class="t-body-lg">Traditional agencies are too <em>slow/expensive</em>. In-house is too <em>narrow</em>.</p>
    </div>
    <div class="col col--bright">
      <p class="t-label">The Founding Solution:</p>
      <p class="t-body-lg">We provide <mark class="mint-highlight">high-fidelity</mark> branding + technical launch in <mark class="mint-highlight">weeks</mark>, not months.</p>
    </div>
  </div>
</section>
```

---

### Type C — Section Divider

**Background:** Dark.
**Elements:**
- Single large Gelasio 500 headline, white, centered or left-aligned, 84px, filling most of the slide
- No body copy, no footer body — just the massive type and the standard footer bar
- Often a number or short phrase ("Why Founding?", "01 Brand", etc.)

```html
<section class="slide slide--section">
  <h2 class="t-section-title">Why Founding?</h2>
</section>
```

---

### Type D — Content Grid (cards / features)

**Background:** Dark.
**Elements:**
- Headline top (Gelasio, ~35px, white, with italic mint emphasis)
- Grid of 3–5 cards below. Each card has:
  - A holo color chip/tag label (e.g. `#A4FCFF` background, small Manrope SemiBold label, 9px)
  - Short bold title (Manrope 600, ~13px)
  - Body copy (Manrope 400, ~13px, grey `#CCCCCC`)
- Cards use dark surface with subtle borders or no border

```html
<section class="slide slide--grid">
  <h2 class="t-hero">A brand <em class="italic-mint">only</em> humans can use is <em class="italic-mint">half</em> a brand.</h2>
  <div class="slide__cards">
    <div class="card">
      <span class="chip chip--cyan">Built for all</span>
      <p class="t-body">Great brands built for humans first — then structured for AI tools too.</p>
    </div>
    <!-- repeat -->
  </div>
</section>
```

---

### Type E — Stat / Number Slide

**Background:** Dark.
**Elements:**
- Large number or percentage as display text (Manrope SemiBold or Gelasio, very large)
- Supporting label below the number (Manrope 400, smaller)
- Multiple stat blocks in a row or 2×2 grid
- Accent color dots or chips alongside each stat

---

### Type F — Two-Column Content

**Background:** Dark.
**Elements:**
- Left col: icon + label + body paragraph (Manrope 400, ~13px, `#CCCCCC`)
- Right col: different content block or image
- Divider: thin white horizontal rule or vertical rule between cols
- Used for Problem/Solution, Before/After, Feature/Benefit

---

### Type G — Closing / CTA

**Background:** Dark, full bleed.
**Elements:**
- Large Manrope 400–500 hero statement (~57px), white (NOT Gelasio — this one uses Manrope)
- Subhead (Manrope 400, ~20px)
- Short body paragraph (Manrope 400, ~16px, light grey)
- CTA link or button: "Book a virtual coffee" style, Manrope 600, ~12px
- URL in small text below

```html
<section class="slide slide--close">
  <h2 class="t-close-hero">Ready when you are</h2>
  <p class="t-body-lg">Whether you're ready to start building or just want to think out loud, Founding Creative is happy to help.</p>
  <p class="t-body">No pressure. No pitch.</p>
  <a class="cta-link" href="https://foundingcreative.com/coffee">Book a virtual coffee</a>
  <p class="t-small">www.foundingcreative.com/coffee</p>
</section>
```

---

## 7. Persistent Footer

Every slide except the cover gets this footer bar at the bottom (~57px tall).

```
Left:  "Confidential and proprietary information"   Manrope 400, 6.7px, white
Right: "Founding Creative  |  Raise your flag™  |  [slide number]"   Manrope 400, 6.7px, white
```

Include a small Founding wordmark or flag icon left of the confidential text where the logo appears in the source.

---

## 8. CSS Token Map

```css
:root {
  /* Canvas */
  --slide-w: 1280px;
  --slide-h: 720px;
  --slide-ratio: 16/9;

  /* Margins */
  --margin: 37px;
  --footer-h: 57px;

  /* Colors */
  --black:        #000000;
  --white:        #FFFFFF;
  --grey-mid:     #CCCCCC;
  --grey-dark:    #999999;
  --grey-dim:     #666666;
  --mint-hl:      #C9FFDC;   /* text highlight background */
  --mint-bright:  #5AFE94;   /* icon / active */
  --mint:         #7EF893;   /* brand system token */
  --cyan:         #A4FCFF;
  --blue:         #8FDBFC;
  --lavender:     #C9CCFF;
  --purple:       #AD97FF;
  --pink:         #FFC8D2;
  --yellow:       #FED05A;

  /* Type */
  --font-display: 'Gelasio', Georgia, serif;
  --font-body:    'Manrope', system-ui, sans-serif;
  --font-mono:    'Roboto Mono', monospace;
  --font-ui:      'Roboto', system-ui, sans-serif;

  /* Type scale (at 1280px canvas) */
  --t-section:    84px;   /* section divider */
  --t-hero:       60px;   /* cover / closing hero */
  --t-statement:  35px;   /* statement headline */
  --t-headline:   30px;   /* body headline */
  --t-subhead:    26px;   /* sub-headline */
  --t-label:      17px;   /* eyebrow / label */
  --t-body:       15px;   /* body copy */
  --t-small:      12px;   /* small label */
  --t-footer:     6.7px;  /* footer legal */
}
```

---

## 9. Highlight / Emphasis Rules

The deck's most distinctive micro-pattern. Two flavors:

**Mint text highlight (primary):** Black text on `#C9FFDC` mint background.
Used inline on 1–2 key words per paragraph. In HTML:
```html
<mark class="mint-hl">high-fidelity</mark>
```
```css
.mint-hl { background: var(--mint-hl); color: #000; padding: 0 3px; border-radius: 2px; }
```

**Italic mint text (display):** Gelasio SemiBold italic, color `#C9FFDC`, no background.
Used in large display headlines (Gelasio tier). One phrase per headline.
```html
<em class="display-em">the gap</em>
```
```css
.display-em { font-style: italic; font-weight: 600; color: var(--mint-hl); }
```

Never combine both on the same word. Never apply to more than one phrase per slide.

---

## 10. Navigation & Interactivity

The HTML deck uses keyboard and click navigation:
- Arrow keys / spacebar advance slides
- Click anywhere advances
- Slide number displayed in footer (auto-incremented)
- Store current slide in `localStorage` so refresh preserves position

```js
let current = parseInt(localStorage.getItem('slide') || '0');
const slides = document.querySelectorAll('.slide');
function goTo(n) {
  slides[current].classList.remove('active');
  current = Math.max(0, Math.min(n, slides.length - 1));
  slides[current].classList.add('active');
  localStorage.setItem('slide', current);
}
document.addEventListener('keydown', e => {
  if (e.key === 'ArrowRight' || e.key === ' ') goTo(current + 1);
  if (e.key === 'ArrowLeft') goTo(current - 1);
});
document.addEventListener('click', () => goTo(current + 1));
```

---

## 11. Voice & Copy Rules

- Sentence case everywhere — headlines, labels, CTAs, all of it
- One italic/highlighted emphasis phrase per slide — not per paragraph, per slide
- No em dashes — use a comma, a period, or restructure the sentence
- "Founding Creative" on first mention, "Founding" after that
- Footer always reads: "Founding Creative  |  Raise your flag™  |  [#]"
- Copyright line: "©[year] Founding Creative. All rights reserved. Confidential and proprietary information."
- Tagline: "Raise your flag™" — always with ™

---

## 12. Image Treatment

- Cover slide: full-bleed dark photographic or abstract image. Right half carries the main visual. Left half is darker for text legibility.
- Content slides: background is typically a solid near-black (`#000` or close) — no images needed unless the slide type explicitly calls for one.
- Logos and icons: use SVGs from `assets/logos/`. Wordmark white on dark slides.
- Holographic wave: use `assets/logos/wave-white.svg` as a textural element on closing slides or covers — large, behind content, partially cropped.

---

## 13. Building a New Deck — Checklist

Before generating any slide:
1. Read `CLAUDE.md` for architecture conventions
2. Read `css/tokens.css` for all design tokens
3. Read this file (`DECK.md`) for slide patterns
4. Confirm the target deck type (sales, proposal, intro, case study)
5. Choose 1–2 holo accent colors for the deck (use consistently, not per-slide randomly)
6. Write the full slide list as an outline before writing HTML
7. Use the exact font stack from Section 2 — never substitute
8. Apply the type scale from Section 3 — never invent new sizes
9. Implement persistent footer on every non-cover slide (Section 7)
10. Add localStorage slide position (Section 10)

---

*Source: BrandForge Gauntlet PPT · Founding Creative · May 2026*
*Maintained by: Tyler / Josh — update when the gold-standard deck is updated*
