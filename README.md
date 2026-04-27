# Founding Creative Design System

The official design system for Founding Creative — built with Claude Design and version-controlled here for use across all team members and projects.

This repository serves as the single source of truth for Founding Creative's visual language, components, and design standards. Rather than maintaining local copies or building from scratch, every team member connects their personal Claude Design account directly to this repository to access the latest system automatically.

---

## What Is This?

This is a **living design system** — meaning it evolves over time as our brand, products, and standards grow. It was initially generated using Claude Design and is maintained here so that:

- All team members work from the same design foundation
- Updates are version-controlled and traceable
- No one needs to rebuild or manually sync design assets
- Individual Claude accounts stay connected to the latest without extra effort

---

## Getting Started

### Connect This Repo to Your Claude Design Account

Rather than building a design system from scratch, point Claude Design directly to this repository to load the Founding Creative Design System into your personal account.

1. **Open Claude Design** and begin the flow to create a new design system
2. **When prompted to set up your design system**, choose the option to connect an existing source rather than building manually
3. **Provide the following repository address** when asked:
   ```
   git clone https://github.com/foundingadmin/DesignSystem-Founding.git
   ```
4. **Complete the setup** — Claude Design will pull in the latest version of the design system automatically
5. **You're connected** — any future updates pushed to this repo will be reflected when you sync

> ⚠️ Do not manually recreate or duplicate the design system locally. Always connect to this repository to ensure you're working from the current version.

---

## For Maintainers

### Updating the Design System

When updates are made to the design system (new components, token changes, revised guidelines), they should be committed to this repository following the branching and review process below.

1. Create a new branch for your changes
2. Make and test your updates
3. Open a pull request with a clear description of what changed and why
4. Once reviewed and merged, tag a new release using semantic versioning (e.g. `v1.1.0`)

### Versioning

This repository follows [semantic versioning](https://semver.org/):

| Version bump | When to use |
|---|---|
| `v1.0.1` | Small fixes, typos, minor corrections |
| `v1.1.0` | New components or additions, backwards compatible |
| `v2.0.0` | Major redesign or breaking changes |

All releases are tagged and documented in the [Releases](../../releases) section of this repository.

---

## Repository Structure

```
/
├── README.md          # You are here
├── [design system files exported from Claude Design]
```

This structure will grow as the system evolves. Refer to individual release notes for details on what's included in each version.

---

## Questions & Contributions

If you have questions about the design system, notice something outdated, or want to propose a change, open an issue in this repository or reach out to the team directly.

All contributions should go through a pull request — direct commits to `main` are discouraged to keep the system stable and traceable.

---

*Founding Creative Design System — maintained by the Founding Creative team.*
