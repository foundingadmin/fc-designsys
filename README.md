# Founding Creative Design System

The official design system for Founding Creative — a static, no-build-step reference hosted at [brand.foundingcreative.com](https://brand.foundingcreative.com) and version-controlled here as the single source of truth for our visual language, tokens, and components.

---

## What Is This?

A **living design system** built in plain HTML and CSS — no bundler, no package manager, no build step. It evolves as our brand and products grow, and every team member pulls from the same source rather than maintaining local copies.

- All design decisions are version-controlled and traceable
- Token and component changes propagate to everyone automatically
- Any AI agent or tool can load the system fresh from `main` before doing creative work
- The hosted reference at `brand.foundingcreative.com` updates on every merge to `main`

---

## Viewing the Design System

The hosted version at **[brand.foundingcreative.com](https://brand.foundingcreative.com)** is always current with `main`.

For local development, serve over HTTP so fonts load correctly:

```bash
python3 -m http.server 8080
# then open http://localhost:8080
```

| File | Purpose |
|---|---|
| `index.html` | Interactive reference — all tokens, components, and live demos |
| `index-print.html` | A3 print-optimised variant with page breaks per section |
| `how-to.html` | Setup guide for connecting Claude to this design system |

---

## Using This System in AI Agents and Tools

To get consistent, on-brand output from any AI agent, coding tool, or generative workflow, point it at this repository before asking it to produce any visual work. The key files to load are:

| File | What it gives the agent |
|---|---|
| `css/tokens.css` | Every colour, spacing, radius, and typography token |
| `css/components.css` | All reusable component classes and their variants |
| `index.html` | A live reference showing tokens and components in context |
| `CLAUDE.md` | Conventions, naming rules, and patterns to follow |

**The principle:** read these files fresh from `main` at the start of each session. Do not rely on a cached or bundled snapshot — the repo is the source of truth, and it changes.

A prompt like this works well as a preamble in any tool that can fetch URLs or read files:

> Before generating anything, read the Founding Creative design system from `github.com/foundingadmin/designsystem-foundingcreative` (branch: `main`). Load `css/tokens.css`, `css/components.css`, and `CLAUDE.md`. Use only the tokens and component classes defined there. Do not invent new colour values, font stacks, or spacing values.

---

## Repository Structure

```
/
├── README.md              # You are here
├── CLAUDE.md              # Architecture notes and conventions for Claude Code
├── SKILL.md               # Skill definition for the founding-creative-design Claude skill
├── index.html             # Interactive design system reference
├── index-print.html       # A3 print variant
├── how-to.html            # Claude setup guide
├── favicon.svg
├── site.webmanifest
├── CNAME                  # brand.foundingcreative.com
├── css/
│   ├── tokens.css         # All design tokens as CSS custom properties
│   └── components.css     # All reusable component classes
├── assets/
│   ├── logos/             # Canonical SVG logos (brandmark, icon, wave, wordmark × black/white)
│   └── …                  # OG images, holographic texture, flag assets
├── fonts/                 # Gelica (.otf) and Manrope variable (.ttf) font files
└── uploads/               # Raw source files (not for direct use)
```

---

## For Maintainers

### Making Changes

1. Create a branch for your changes — never commit directly to `main`
2. Edit `css/tokens.css` or `css/components.css` (and `index.html` to demo any new additions)
3. Preview locally with `python3 -m http.server 8080`
4. Open a pull request with a clear description of what changed and why
5. Once merged, tag a release using semantic versioning

### Versioning

| Version bump | When to use |
|---|---|
| `v1.0.x` | Typos, minor corrections |
| `v1.x.0` | New components or backwards-compatible additions |
| `vx.0.0` | Redesigns or breaking token/class renames |

All releases are tagged and documented in the [Releases](../../releases) section of this repository.

---

## Questions & Contributions

Open an issue or pull request. Direct commits to `main` are not permitted — all changes go through a PR to keep the system stable and traceable.

---

*Founding Creative Design System — maintained by the Founding Creative team.*
