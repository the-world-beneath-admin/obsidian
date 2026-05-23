# Marketing Report - 2026-05-11 - Homepage Copy Source Update

## Task

Apply approved Variant 1 copy to the local homepage source for The World Beneath.

## Scope

- Main game / The World Beneath.
- Local source only.
- No deployment performed.

## Source Updated

- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\index.html`

## What Changed

- Updated homepage `<title>`.
- Updated meta description, Open Graph description, Twitter description, and structured-data website description.
- Updated homepage hero strong line to:
  - "Run dungeons. Grow creatures. Shape the world beneath."
- Updated homepage hero body copy to the approved shared-world RPG pitch.
- Replaced the old proof-of-work/FeastFolio hero line with the approved CTA direction:
  - "Follow development, join the community, and help shape what comes next."

## Checks Run

- Local source was inspected before editing.
- Live homepage, game page, and progress page were checked on 2026-05-11 before selecting the homepage as the first update surface.
- Served local preview opened at `http://127.0.0.1:8000/`.
- Confirmed the local homepage renders with full styling and approved Variant 1 copy in the served preview.
- Browser warnings/errors during the quick served-preview check: none reported.
- No deployment was run in this step.

## Risks

- The website repo was already dirty with many unrelated modified, deleted, and untracked files before this update.
- Only `index.html` was intentionally changed for the homepage copy update.
- Live site will not change until the site source is deployed.

## Memory-Worthy Notes

- Decision - Homepage is the first copy surface to receive the approved main-game copy foundation.
- Warning - Deployment should be handled separately because the website repo has many unrelated pending changes.

## Do Not Promote To Memory

- Do not mark this as deployed.
- Do not assume other pages were updated.
- Do not treat the dirty website repo state as caused by this task.

## Follow-Up Recommendations

- Use the served local preview or a deployment preview for any further visual checks.
- Cleanly isolate a deployable website change set before publishing.
- Decide whether to update the Game page hero after the deployment plan is clean.
