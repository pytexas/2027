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

**Before opening a PR:** run `just link-check` and get it passing locally. CI runs the same check, but some sites return 403 to GitHub's runners; add those URLs to `.lycheeignore`. The recipe skips `site/404.html` because its root-relative `/2027/` links cannot resolve from local files.

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
  - `home.html` — Hero section: the 2027 logo (`docs/assets/images/logos/pytexas2027_logo.svg`) above the CFP button. One SVG serves both color modes; its seams are transparent cutouts, so the hero background shows through them.
  - `main.html` — Site-wide announcement banner.
- **`docs/stylesheets/extra.css`** — Custom color schemes (`pytx2027_light` for day, `pytx2027` for night). The six logo colors are declared once on `:root`; each scheme then maps them onto Material's `--md-*` variables. `social.cards_layout_options` in `mkdocs.yml` uses the same palette and the logo SVG.

### Navigation Phasing

Several nav sections in `mkdocs.yml` are commented out for later activation. The placeholder pages already exist — just uncomment when ready. `Speaking` is already live (CFP opened October 2026).

- `Schedule` section — uncomment when schedule is published (populate `data/schedule.yaml`)
- `Virtual Attendance` — uncomment when virtual event details are confirmed
- `Our Sponsors` listing — uncomment when sponsors are signed (add logos to `docs/assets/images/sponsors/`)

### CI/CD Pipeline (GitHub Actions)

1. **link-check.yml** — Builds with `--strict`, runs lychee link checker. Triggers on all pushes/PRs.
2. **ci.yml** — Deploys to GitHub Pages. Only runs on `main` after link-check succeeds.
3. **check.yml** — Dependency vulnerability review on PRs.

### Color Scheme

Colors from the 2027 logo (sun, prickly pear, agave):

| Color      | Hex     | CSS Variable    | Used for |
|------------|---------|-----------------|----------|
| Peach      | #FCBB77 | `--pytx-peach`  | night headings, night hover, hero gradient |
| Orange     | #F79227 | `--pytx-orange` | buttons, night links |
| Pink       | #D92849 | `--pytx-pink`   | day accent (fills only, too light for night text) |
| Dark red   | #A61E38 | `--pytx-red`    | day links, button hover, announcement banner |
| Sage       | #879B6B | `--pytx-sage`   | borders, night table heads |
| Dark green | #687659 | `--pytx-green`  | day headings, day table heads |
| Darker green | #4F5A44 | `--pytx-green-dark` | header bar, nav tabs, footer (derived from the logo green for contrast; not on the delivered sheet) |

Supporting colors not in the logo: cream `#FAFAF8` (day background), ink `#2B2520` (day body text), night `#14100E` (night background, a warm near-black so the logo's cutouts read as ink lines). The Hex Colors section of `README.md` also records where the delivered SVGs differ from the swatch sheet.

When changing colors: update the `:root` block in `extra.css`, the two scheme blocks, the `.pytx-container` gradients, `cards_layout_options` in `mkdocs.yml`, the Mermaid `pie` theme variables in `docs/sponsors/sponsor-us.md`, and the Hex Colors section of `README.md`.

## Key Conventions

- Conference content pages live in `docs/`. Venue, food, parking, hotel info carries over year-to-year.
- Sponsor logos go in `docs/assets/images/sponsors/`, speaker photos in `docs/assets/images/speakers/`.
- The schedule is data-driven: edit `data/schedule.yaml`, not `docs/schedule/index.md` (it gets overwritten on build).
- Prospectus demographic data in `docs/sponsors/sponsor-us.md` uses Mermaid pie charts — update with post-conference survey data.
- `.ai-sessions/` is gitignored. Session summaries and `lessons.md` stay local and are never staged. The global pre-commit hook still expects a staged session file, so commits here need `--no-verify`.
- The `asking-for-sponsorship.md` page has email templates with year-specific dates that need updating.
