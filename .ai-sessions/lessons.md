# Lessons Learned

## Recent
<!-- 10 most recent lessons, newest first -->

- When restructuring a prior-year artifact (e.g. sponsor tiers), carry values forward verbatim and only change what a source explicitly says to change. Inferring "logically implied" removals (dropped Gold pitch, invented "no table") got corrected twice. (2026-09-02)
- Named-sponsorship and tier benefits live in the sibling prior-year repo (`/home/mmegger/Code/PyTexas/2026`); read `docs/sponsors/sponsor-us.md` there for exact rows instead of guessing. (2026-09-02)
- Exact-string Edit is fragile on wide markdown tables (trailing spaces, differing checkmark counts per row). Splice large table blocks by line-number markers in Python instead. (2026-09-02)
- The sponsor prospectus in `docs/sponsors/sponsor-us.md` is staged inside an HTML comment behind a "Coming Soon" gate; it renders nothing until uncommented, so a complete draft can be committed safely. (2026-09-02)
- Sponsor tier pricing and benefit definitions come from the "PyTexas <year> Budget" Google Sheet, including reviewer comments anchored to the sponsor-tier cells. (2026-09-02)
- When setting up a new year's conference site, check `git show <first-commit>:<file>` for the prior year's initial state, not the current state. The launch version is much simpler than the final version. (2026-04-08)
- The initial 2026 site used a single simple color scheme with a placeholder PNG hero. The dual light/dark scheme with SVG logos came later. Start simple. (2026-04-08)
- MkDocs Material `pytx-hero__image` class on an `<img>` tag directly (like 2026 initial) works better for placeholder PNGs than wrapping in flex divs with object-fit. (2026-04-08)
- Ask about color scheme and dark mode preferences before writing CSS. Writing 490 lines that get replaced wastes time. (2026-04-08)
- The schedule hook (hooks/schedule.py) gracefully skips when no data/schedule.yaml exists. Safe to include from day one. (2026-04-08)

## Categories

### MkDocs / Conference Site
- When setting up a new year's conference site, check `git show <first-commit>:<file>` for the prior year's initial state, not the current state. The launch version is much simpler than the final version. (2026-04-08)
- The initial 2026 site used a single simple color scheme with a placeholder PNG hero. The dual light/dark scheme with SVG logos came later. Start simple. (2026-04-08)
- MkDocs Material `pytx-hero__image` class on an `<img>` tag directly (like 2026 initial) works better for placeholder PNGs than wrapping in flex divs with object-fit. (2026-04-08)
- `repo_name` in mkdocs.yml controls the text shown next to the git icon in the header. Easy to forget to update from the prior year. (2026-04-08)
- The schedule hook (hooks/schedule.py) gracefully skips when no data/schedule.yaml exists. Safe to include from day one. (2026-04-08)

### Workflow
- Ask about color scheme and dark mode preferences before writing CSS. Writing 490 lines that get replaced wastes time. (2026-04-08)
- When restructuring a prior-year artifact, carry values forward verbatim and change only what a source explicitly calls out. Inferring implied removals got corrected twice. (2026-09-02)

### Sponsors / Prospectus
- Sponsor tier pricing and benefit definitions come from the "PyTexas <year> Budget" Google Sheet, including reviewer comments anchored to the sponsor-tier cells. (2026-09-02)
- Named-sponsorship and tier benefit rows live in the sibling prior-year repo (`/home/mmegger/Code/PyTexas/2026`, `docs/sponsors/sponsor-us.md`); read them there instead of guessing. (2026-09-02)
- The prospectus in `docs/sponsors/sponsor-us.md` is staged inside an HTML comment behind a "Coming Soon" gate; it renders nothing until uncommented, so a complete draft commits safely. (2026-09-02)

### Tooling
- Exact-string Edit is fragile on wide markdown tables (trailing spaces, differing checkmark counts per row). Splice large table blocks by line-number markers in Python instead. (2026-09-02)
