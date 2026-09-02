# Session Summary: 2027 Sponsor Prospectus Draft

**Date**: 2026-09-02
**Duration**: ~40 minutes
**Conversation Turns**: 6
**Estimated Cost**: ~$2-3 (Opus, several large Drive/file reads)
**Model**: claude-opus-4-8

## Key Actions

- Confirmed no 2027 prospectus existed yet: sponsor pages carried over from 2026, demographic SVGs still 2024, no downloadable PDF, sponsors nav still commented out.
- Read the "PyTexas 2027 Budget" sheet in Google Drive, including the four open comments from Mason and Laura Santamaria that define sponsor-tier benefits.
- Mapped Laura's comments to tiers: Platinum (talk-or-workshop + table), Gold (table), Community (no pitch, rotating slide), Opportunity Grant (no stage time, add-on).
- Drafted the 2027 prospectus in `docs/sponsors/sponsor-us.md` as a single 2026-style benefits matrix (Platinum, Gold, Community + named sponsorships Lanyard, Live Captioning, Food, Coffee Bar) plus an add-ons table.
- Pulled named-sponsorship benefit rows verbatim from the 2026 repo (`/home/mmegger/Code/PyTexas/2026`) per Mason's instruction that those did not change.
- Split the old combined Food/Coffee "signage OR coffee logo" choice: Food gets breakfast/lunch signage, Coffee Bar gets coffee-area logo.
- Scrubbed removed-tier references (Bronze $1K, "Gold+ pitches", "$1K-$12K range") from `docs/sponsors/asking-for-sponsorship.md` email templates.

## Prompt Inventory

| Prompt/Command | Action Taken | Outcome |
|---|---|---|
| Do we have our 2027 prospectus yet? | Searched docs/, found only stale 2024 assets | Reported no real prospectus exists |
| Look in 2027 Google Drive budget, extrapolate from comments | Read budget sheet + comments | Proposed tier structure with pricing + benefits |
| Draft it; note removed tiers; apply no-customization-below-Platinum rule | Branched, wrote prospectus + fixed email templates | Draft on branch; flagged Silver/Bronze/Networking removed |
| Did we remove Gold pitch time? | Re-checked comments | Corrected: restored Gold + Platinum 2-min pitch |
| Add-ons require a package; tickets only in non-add-on packages; named sponsorships = 2026; check pytexas/2026 | Read 2026 prospectus, rebuilt as full matrix | Named sponsorships carry exact 2026 rows |
| Community replaced Bronze | Confirmed Community inherits Bronze's 1 ticket / no discount | Validated existing draft numbers |

## Efficiency Insights

**What went well:**
- Splicing the large table by line-number markers in Python after exact-string Edit failed on whitespace/checkmark-count drift.
- Checking the sibling 2026 repo locally instead of guessing named-sponsorship benefits.

**What could improve:**
- Over-extrapolated twice (dropped Gold pitch, invented "no table" for named sponsorships) before Mason corrected. Should default to "carry forward unless a comment explicitly removes it."

**Course corrections:**
- Restored Gold/Platinum pitch after Mason flagged it.
- Rebuilt named sponsorships from 2026 rows instead of my invented "logo-only" version.

## Process Improvements

- When a prior-year artifact exists, pull exact values from it before inferring; only change what is explicitly called out as changed.
- Exact-string Edit is fragile on wide markdown tables (trailing spaces, checkmark counts). Prefer line-marker splicing for large table blocks.

## Observations

- The prospectus lives inside an HTML comment behind a "Coming Soon" gate; it renders nothing until uncommented. Safe to stage complete.
- One remaining open item: Community's included-ticket count was the only value with no 2026 source, now resolved (inherits Bronze: 1 ticket, no discounted).

## Suggested Skills for Next Session

- `content-design:review-content`: if the prospectus prose gets a copy pass before going public.
