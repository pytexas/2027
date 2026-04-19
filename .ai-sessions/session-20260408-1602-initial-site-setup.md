# Session Summary: PyTexas 2027 Initial Site Setup
**Date**: 2026-04-08
**Duration**: ~45 minutes
**Conversation Turns**: ~25
**Estimated Cost**: ~$15-20 (heavy file reads across 2025/2026 repos, many writes)
**Model**: Claude Opus 4.6

## Key Actions

### Research Phase
- Explored 2026 and 2025 repos in parallel (structure, git history, initial commits)
- Identified what 2026 launched with in its first commit vs. what was added later
- Read all key files from 2026: mkdocs.yml, content pages, CSS, workflows, hooks, templates

### Site Creation
- Created feature branch `initial-site-setup`
- Built full directory structure for 2027
- Copied and adapted all config files: mkdocs.yml, pyproject.toml, justfile, .gitignore, GitHub Actions workflows
- Copied reusable binary assets from 2026 (favicon, parking map, prospectus SVGs, virtual images)
- Created all content pages adapted for April 16-18, 2027 dates
- Created placeholder pages for all commented-out nav items (schedule, speaking, virtual)
- Set up schedule hook infrastructure (hooks/schedule.py with graceful skip when no data)
- Verified site builds successfully

### Styling & Theming
- Initially copied 2026's dual light/dark color scheme (wrong approach)
- Rewrote CSS to a single simplified scheme inspired by BBQ pit hero image
- Removed dark mode toggle from mkdocs.yml
- Colors: dark brown header, amber accents, green links, white background

### Content Refinements
- Updated hero image from broken SVG references to site-still-cooking.png placeholder
- Commented out prospectus table (not ready for launch), added mailing list CTA
- Updated homepage sponsor tile to point to sponsors mailing list
- Enabled Speaking tab with CFP date (Oct 1, 2026), meetup CFP link, proposal help section
- Fixed repo_name in both 2027 and 2026 mkdocs.yml (was "conference-site", now "pytexas/20XX")
- Hunted and replaced all emdashes and sentence-level hyphens

### Documentation
- Created CLAUDE.md with architecture overview and dev guide
- Wrote commit message to commit-msg.md

## Prompt Inventory

| Prompt/Command | Action Taken | Outcome |
|---|---|---|
| Set up 2027, look at 2026/2025 history | Parallel exploration of both repos, identified initial launch scope | Clear picture of what to build |
| Python version should be 3.14 | Updated .python-version | Corrected before writing other files |
| Do you have pages so I can turn on nav later? | Created 6 placeholder pages (schedule/*, speaking, virtual) | All nav entries backed by files |
| Added site-still-cooking.png | Updated home.html hero to use the image | Image displayed (but stretched) |
| Image is stretched terribly | Checked 2026 initial approach, simplified hero to use class not inline img div | Fixed with pytx-hero__image class |
| White box around image, change to match BBQ pit, remove dark mode | Rewrote CSS to single scheme, BBQ colors, white bg, no toggle | Clean look matching the image |
| Remove prospectus, update sponsor tile | Commented out prospectus like 2026 did, added mailing list CTA | Launch-ready sponsor pages |
| repo_name wrong | Fixed in both 2027 and 2026 mkdocs.yml | Both repos corrected |
| Links too brown, make them green | Changed link color to --pytx-green (#4A7C59) | Links stand out properly |
| Was there a speaking tab on initial 2026? | Checked, there wasn't. Discussed adding one for 2027 | Added speaking with CFP info |
| Add meetup CFP link, proposal help section | Added "Want Help Drafting Your CFP?" section with program@pytexas.org | Speaking page complete |
| CFP opens 10/1/2026 | Updated speaking page and homepage | Dates consistent |
| Kill all emdashes | Grep'd and replaced 2 instances | Clean prose |
| Hyphens scream AI | Confirmed fix, saved feedback to memory | Will avoid in future |

## Efficiency Insights

### What went well
- Parallel agent exploration of 2026 and 2025 repos saved significant time upfront
- Checking the initial 2026 git commit (`git show 3133b06:`) was key to understanding what to launch with vs. what comes later
- Copying the 2026 approach for commented-out prospectus, nav phasing, and placeholder images avoided reinventing patterns

### What could have been more efficient
- Initially copied the complex dual-scheme CSS from 2026's final state instead of its simpler initial state. Should have checked the initial commit CSS first.
- The hero image went through 3 iterations (SVG divs -> inline style -> class) because I started with the final 2026 approach instead of the initial one
- Could have asked about color scheme/dark mode preference before writing 490 lines of CSS that got replaced

### Course corrections
- User corrected Python version to 3.14 (I defaulted to 2026's 3.13)
- User flagged stretched image, which led to checking initial 2026 approach
- User flagged white box/wrong color scheme, leading to full CSS rewrite
- User flagged brown links not looking like links

## Process Improvements

- When setting up a new year's conference site, always check the **initial commit** of the prior year, not just the current state. The initial launch is much simpler.
- Ask about color scheme preferences before writing CSS. The "match the placeholder image" approach was the right call.
- For conference sites that phase content in, start with the simplest possible styling and build up.

## Observations

- The PyTexas conference site follows a clear annual pattern: launch simple ~1 year out, add CFP/tickets in fall, add schedule/speakers in winter, final polish in spring.
- The 2026 repo evolved from requirements.txt to pyproject.toml+uv mid-lifecycle. Starting 2027 with the modern stack from day one saves that migration.
- The schedule hook (hooks/schedule.py) is a nice piece of infrastructure that was added mid-2026. Including it from the start in 2027 means one less thing to build later.
- The "asking-for-sponsorship.md" advocacy guide with email templates is a unique and valuable piece of content that carries over well year to year.
