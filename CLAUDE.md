# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

PyTexas 2027 Conference website — a static site built with MkDocs Material, deployed to GitHub Pages. Conference dates: **April 16-18, 2027** in Austin, TX at the Austin Central Library.

## Build & Development Commands

All commands use `just` (task runner) with `uv` (Python package manager):

```bash
just install          # Install dependencies (uv sync)
just serve            # Local dev server on port 8000
just serve-port 8001  # Dev server on specific port
just build            # Build static site to site/
just validate         # Build with --strict flag
just link-check       # Build + check all links with lychee
just check            # Run all quality checks (alias for link-check)
just clean            # Remove site/, .lycheecache/, __pycache__/
just deploy           # Deploy to GitHub Pages (production only)
```

**System prerequisite:** Cairo library (`brew install cairo` on macOS).

## Architecture

### Content Pipeline

```
docs/*.md  ──────────────────────────┐
data/schedule.yaml ─→ hooks/schedule.py ─→ docs/schedule/index.md ──→ mkdocs build ──→ site/
overrides/*.html ────────────────────┘
docs/stylesheets/extra.css ──────────┘
```

- **`docs/`** — Markdown source files. MkDocs renders these into the static site.
- **`hooks/schedule.py`** — MkDocs `on_pre_build` hook that reads `data/schedule.yaml` and auto-generates `docs/schedule/index.md`. Skips gracefully if no YAML exists yet.
- **`overrides/`** — MkDocs Material template overrides:
  - `home.html` — Hero section with placeholder image. When the 2027 logo is ready, uncomment the day/night SVG `<div>` blocks and remove the placeholder `<img>` tag. The logo SVGs go in `docs/assets/images/logos/pytexas2027_day_color.svg` and `pytexas2027_night_color.svg`.
  - `main.html` — Site-wide announcement banner.
- **`docs/stylesheets/extra.css`** — Custom color scheme (`pytx2027` / `pytx2027_light`). Colors are placeholders from 2026; update CSS custom properties when the 2027 logo palette is finalized. Also update `social.cards_layout_options` in `mkdocs.yml` to match.

### Navigation Phasing

Several nav sections in `mkdocs.yml` are commented out for later activation. The placeholder pages already exist — just uncomment when ready:

- `Speaking` — uncomment when CFP opens (update dates/links in `docs/speaking.md`)
- `Schedule` section — uncomment when schedule is published (populate `data/schedule.yaml`)
- `Virtual Attendance` — uncomment when virtual event details are confirmed
- `Our Sponsors` listing — uncomment when sponsors are signed (add logos to `docs/assets/images/sponsors/`)

### CI/CD Pipeline (GitHub Actions)

1. **link-check.yml** — Builds with `--strict`, runs lychee link checker. Triggers on all pushes/PRs.
2. **ci.yml** — Deploys to GitHub Pages. Only runs on `main` after link-check succeeds.
3. **check.yml** — Dependency vulnerability review on PRs.

### Color Scheme

Placeholder colors (from 2026 — update when 2027 logo is designed):

| Color  | Hex     | CSS Variable    |
|--------|---------|-----------------|
| Green  | #204F3C | `--pytx-green`  |
| Yellow | #C2B64A | `--pytx-yellow` |
| Orange | #C73810 | `--pytx-orange` |
| Brown  | #443229 | `--pytx-brown`  |
| Blue   | #4B8EC2 | `--pytx-blue`   |
| Cream  | #FAFAF8 | `--pytx-light-cream` |

When updating colors: change both `pytx2027_light` and `pytx2027` (dark) scheme blocks in `extra.css`, gradient backgrounds in the `.pytx-container` rules, and `cards_layout_options` in `mkdocs.yml`.

## Key Conventions

- Conference content pages live in `docs/`. Venue, food, parking, hotel info carries over year-to-year.
- Sponsor logos go in `docs/assets/images/sponsors/`, speaker photos in `docs/assets/images/speakers/`.
- The schedule is data-driven: edit `data/schedule.yaml`, not `docs/schedule/index.md` (it gets overwritten on build).
- Prospectus demographic data in `docs/sponsors/sponsor-us.md` uses Mermaid pie charts — update with post-conference survey data.
- The `asking-for-sponsorship.md` page has email templates with year-specific dates that need updating.
