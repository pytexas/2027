# Lessons Learned

## Recent
<!-- 10 most recent lessons, newest first -->

- When setting up a new year's conference site, check `git show <first-commit>:<file>` for the prior year's initial state, not the current state. The launch version is much simpler than the final version. (2026-04-08)
- The initial 2026 site used a single simple color scheme with a placeholder PNG hero. The dual light/dark scheme with SVG logos came later. Start simple. (2026-04-08)
- MkDocs Material `pytx-hero__image` class on an `<img>` tag directly (like 2026 initial) works better for placeholder PNGs than wrapping in flex divs with object-fit. (2026-04-08)
- Ask about color scheme and dark mode preferences before writing CSS. Writing 490 lines that get replaced wastes time. (2026-04-08)
- The schedule hook (hooks/schedule.py) gracefully skips when no data/schedule.yaml exists. Safe to include from day one. (2026-04-08)
- `repo_name` in mkdocs.yml controls the text shown next to the git icon in the header. Easy to forget to update from the prior year. (2026-04-08)

## Categories

### MkDocs / Conference Site
- When setting up a new year's conference site, check `git show <first-commit>:<file>` for the prior year's initial state, not the current state. The launch version is much simpler than the final version. (2026-04-08)
- The initial 2026 site used a single simple color scheme with a placeholder PNG hero. The dual light/dark scheme with SVG logos came later. Start simple. (2026-04-08)
- MkDocs Material `pytx-hero__image` class on an `<img>` tag directly (like 2026 initial) works better for placeholder PNGs than wrapping in flex divs with object-fit. (2026-04-08)
- `repo_name` in mkdocs.yml controls the text shown next to the git icon in the header. Easy to forget to update from the prior year. (2026-04-08)
- The schedule hook (hooks/schedule.py) gracefully skips when no data/schedule.yaml exists. Safe to include from day one. (2026-04-08)

### Workflow
- Ask about color scheme and dark mode preferences before writing CSS. Writing 490 lines that get replaced wastes time. (2026-04-08)
