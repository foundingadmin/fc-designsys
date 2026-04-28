# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repository Is

This is the **Founding Creative Design System** — a static, no-build-step design system hosted on GitHub Pages at `brand.foundingcreative.com`. It is the single source of truth for Founding Creative's visual language and is consumed directly by team members via Claude Design.

There is no package manager, no bundler, no test suite, and no CI pipeline. All files are plain HTML, CSS, and static assets that browsers consume directly.

## How to Preview

Open either HTML file directly in a browser — no server required:

- `index.html` — interactive design system reference (all tokens, components, and live demos)
- `index-print.html` — A3 print-optimised variant of the same content (forces `print-color-adjust: exact` and page breaks per section)

For accurate font rendering during local development, serve the files over HTTP rather than the `file://` protocol (some browsers block local font loading):

```bash
python3 -m http.server 8080
# then open http://localhost:8080
```

## Repository Structure & Architecture

The system is split across two CSS files that must be loaded in order:

1. **`css/tokens.css`** — loaded first. Declares all `@font-face` rules, then defines every design token as a CSS custom property on `:root`. Also defines the three color schemes (`.scheme-mint`, `.scheme-light`), the base reset, and global element styles (`h1`–`h6`, `body`, `a`, `::selection`).

2. **`css/components.css`** — loaded second, depends on tokens. Contains all reusable component classes (`.btn`, `.chip`, `.navbar`, `.card`, `.icon-tile`, `.section`, `.holo-bg`, stack utilities, etc.).

Both HTML files embed additional page-specific styles in a `<style>` block for layout and demo scaffolding that is not part of the reusable component library.

## Design Token Conventions

- **Color scheme tokens** (`--bg`, `--fg`, `--border`, `--accent`, `--text`, `--text-dim`) are semantic aliases that remap under `.scheme-mint` and `.scheme-light`. Always use semantic tokens in components; use primitives only when a value is unconditionally fixed.
- **Spacing** follows an 8pt grid: `--s-1` (4px) through `--s-13` (150px).
- **Typography**: `--font-display` is Gelica (serif, weights 200–900 including italics); `--font-body` is Manrope (variable, 200–800). Headings always use `font-weight: 500` via the base reset.
- **Radius scale**: `--r-xs` → `--r-2xl` → `--r-full`. Match radius to element type — `--r-full` for buttons/chips, `--r-lg` for cards, `--r-2xl` for hero panels.
- **Holographic colors** (`--holo-cyan`, `--holo-mint`, `--holo-lavender`, etc.) are used exclusively for accent glow effects, gradient overlays, and the `.holo-bg` background treatment. They are not for text or UI chrome.

## Key Component Patterns

**`.holo-bg`** is the brand's signature background treatment — a conic gradient rotating behind a wave-pattern overlay and a dark veil. It requires four child elements (`.holo-bg__grad`, `.holo-bg__waves`, `.holo-bg__veil`, `.holo-bg__fade`) and a positioned parent. The `--light` modifier removes the dark veil.

**`.btn`** variants are `--primary` (mint fill), `--secondary` (ghost), and `--link` (underline). All buttons get an animated holographic glow ring on hover via a `::before` pseudo-element; the `--link` variant suppresses this with `display: none`.

**Color-schemed cards** (`.card--scheme-navy/teal/plum`, `.site-card--prism/rocket/orbit`) use the deep anchor colors (`--deep-navy`, `--deep-teal`, `--deep-plum`) with matching holographic border colors.

## Branching & Release Workflow

- **Never commit directly to `main`**. All changes go through a pull request.
- After merging, tag a release using semantic versioning:
  - Patch (`v1.0.x`): typos, minor corrections
  - Minor (`v1.x.0`): new components or backwards-compatible additions
  - Major (`vx.0.0`): redesigns or breaking token/class renames

## Assets

- **`assets/logos/`** — canonical SVG logo files in four variants (brandmark, icon, wave, wordmark) × two colors (black, white). Use these in production.
- **`uploads/`** — raw uploaded source files (fonts, images, slides). Not for direct use; canonical versions are in `assets/` and `fonts/`.
- **`fonts/`** — all Gelica `.otf` weight files plus Manrope variable `.ttf`. Referenced by `@font-face` in `tokens.css` with relative `../fonts/` paths.
