# PyTexas Conference 2027 Website

## Development

### Before Opening a PR

Run `just link-check` and fix any broken links before you open a pull request.
The same check runs in GitHub Actions, where some sites block the checker, so a clean local run is the faster test.
If a working link fails only in CI, add it to `.lycheeignore`.

### PC Gotcha

If you are on a Windows machine, you will likely run into an error when running `mkdocs serve`. If you follow [the troubleshooting guide](https://squidfunk.github.io/mkdocs-material/plugins/requirements/image-processing/#troubleshooting) note that you may also need to [install MYSYS2](https://www.msys2.org/).

When installed and run, put this into the MYSYS2 terminal:

```
pacman -S mingw-w64-ucrt-x86_64-cairo
```

## Prerequisites

- Python 3.14 or later
- [uv](https://github.com/astral-sh/uv) - Modern Python package manager
- [just](https://github.com/casey/just) - Command runner (optional but recommended)
- Cairo library for image generation (macOS: `brew install cairo`, Linux: `apt install libcairo2`)

## Quick Start

### Using just (Recommended)
```bash
# Install dependencies
just install

# Start development server
just serve

# Run all quality checks
just check
```

### Using uv directly
```bash
# Install dependencies
uv sync

# Start development server
uv run mkdocs serve

# Build the site
uv run mkdocs build
```

## Available Commands

Run `just help` to see all available commands, or use these directly:

- `just serve` - Start development server on port 8000
- `just serve-port 8001` - Start on a specific port
- `just build` - Build the static site
- `just validate` - Build with strict validation
- `just link-check` - Check all links
- `just check` - Run all quality checks
- `just clean` - Clean generated files

## Adding Announcement Banners

To add announcement banners, edit `overrides/main.html`:
```html
{% block announce %}
    <p>Attend the <a href="https://conference.pytexas.org">PyTexas 2027 Conference</a> April 16 - 18, 2027</p>
{% endblock %}
```

## Package Management

This project uses `uv` for dependency management:

- Add a package: `uv add <package>`
- Remove a package: `uv remove <package>`
- Update lock file: `uv lock`

Dependencies are specified in `pyproject.toml` and locked in `uv.lock`.

## CI/CD Pipeline

The repository uses GitHub Actions for continuous integration and deployment:

1. **Link Check** - Validates all links on push/PR
2. **Dependency Review** - Security scanning on PRs
3. **Deploy** - Automatic deployment to GitHub Pages on main branch

## Project Structure

See [CLAUDE.md](CLAUDE.md) for detailed project structure and development guidelines.

## Hex Colors

The 2027 logo (sun, prickly pear, agave) shipped with a six-swatch sheet (`colorhex.svg`).
These are the brand colors, plus the colors the site adds on top of them.

| Role | Hex | CSS variable | Where it shows up |
|---|---|---|---|
| Peach | #FCBB77 | `--pytx-peach` | sun highlight; night headings, night hover, day hero gradient |
| Orange | #F79227 | `--pytx-orange` | sun rays, hill; buttons, night links |
| Pink | #D92849 | `--pytx-pink` | cactus fruit, agave; day accent (fills only, 3.9:1 on the night background) |
| Dark red | #A61E38 | `--pytx-red` | fruit shading; day links, button hover, announcement banner |
| Sage | #879B6B | `--pytx-sage` | cactus pads; borders, night table heads |
| Dark green | #687659 | `--pytx-green` | cactus shading; day headings, day table heads |
| Darker green | #4F5A44 | `--pytx-green-dark` | header bar, nav tabs, footer. Not on the sheet: it is the logo green darkened about 25% so cream text clears 7:1 instead of 4.6:1 |
| Cream | #FAFAF8 | `--pytx-cream` | day background. Not on the sheet |
| Ink | #2B2520 | `--pytx-ink` | day body text. Not on the sheet |
| Night | #14100E | `--pytx-night` | night background, a warm near-black so the logo's cutouts read as ink lines. Not on the sheet |

### What the delivered files actually contain

The swatch sheet and the artwork do not quite agree.
Audited 2026-10-14 against `pytexas27.zip`; none of this is visible at normal size, but it matters if you ever sample a color from a file.

- `pytexas_wavesun.svg` (the logo on the site) uses two colors the sheet omits: `#F79329` for the sun disk (two units off the sheet orange, used more than the sheet orange is) and `#AEBE96`, a light sage for the cactus pad highlights.
- `wordmark_final.svg` and the sheet's own wordmark are green `#69775B`, one unit off the sheet's `#687659`.
- The "AUSTIN, TX" subtitle in every wordmark is five near-identical oranges (`#F4932C`, `#F4942E`, `#F49630`, `#F49632`, `#F59937`), none of them the sheet orange.
- `wordmark_darkpink.svg` and `wordmark_lightpink.svg` each carry a stray `#C1272D` red on one small path.
- The wordmarks and sheet also hold a handful of zero-area grey paths (`#87917B`, `#808B73`, `#8B9580`, `#939D88`, `#969F8C`). Illustrator export residue; they draw nothing.

The site uses the sheet values, not the per-file ones.
The wordmark files are not used on the site, but the whole delivery is checked in under `docs/assets/images/logos/source/` for slides, badges, and anything else that needs it.
