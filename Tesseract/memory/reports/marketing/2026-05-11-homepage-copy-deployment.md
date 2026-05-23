# Marketing Report - 2026-05-11 - Homepage Copy Deployment

## Task

Deploy the approved Variant 1 homepage copy for The World Beneath from the isolated deployment workspace.

## Result

Deployed successfully.

Deployment workspace:

```text
C:\Users\yrred\Desktop\Markeing\Websites\twb-homepage-copy-deploy-20260511
```

Deploy command:

```powershell
npx wrangler deploy
```

## Deployment Details

Wrangler result:

- Uploaded exactly 1 new or modified static asset:
  - `/index.html`
- Already uploaded assets reused:
  - `189`
- Total upload:
  - `180.63 KiB`
- Gzip upload:
  - `34.23 KiB`
- Production Worker:
  - `the-world-beneath-site`
- Production domains:
  - `the-world-beneath.com`
  - `www.the-world-beneath.com`
- New production version:
  - `02ef6cfa-a1a6-4ba7-bfb0-715d63e87791`
- Deployment timestamp:
  - `2026-05-11T21:39:33.912Z`
- Author:
  - `twbmain@gmail.com`

## Live Verification

Homepage verification passed on:

```text
https://the-world-beneath.com/
```

Confirmed live:

- Page title: `The World Beneath - Dungeon Runs, Creature Growth, Shared-World RPG`
- Hero line: `Run dungeons. Grow creatures. Shape the world beneath.`
- Meta/pitch text includes approved Variant 1 language.

Key routes checked:

| Route | Status |
| --- | --- |
| `/` | 200 |
| `/game/` | 200 |
| `/progress/` | 200 |
| `/world-keys/` | 200 |
| `/register/` | 200 |
| `/assets/css/styles.css` | 200 |
| `/assets/js/site.js?v=brand-seo-20260429` | 200 |

Browser live check:

- Title present.
- Hero present.
- Pitch present.
- CTA present.
- Browser warning/error quick check: `0`.

Note: browser screenshot capture timed out once, but DOM and console verification passed.

## Checks Not Run

- No D1 migrations were run.
- No Worker secrets were changed.
- No R2 assets were changed.
- No Game, Progress, or World Keys copy edits were deployed in this task.

## Risks

- Deployment used the isolated workspace rather than a clean Git branch because Git refs did not match the live production baseline.
- The original dirty website repo remains dirty and should not be deployed directly.
- Future deployments still need a cleaner source-control baseline.

## Memory-Worthy Notes

- Decision: approved Variant 1 is now the live homepage copy.
- Fact: deployment uploaded only `/index.html`.
- Fact: new production Worker version is `02ef6cfa-a1a6-4ba7-bfb0-715d63e87791`.
- Warning: keep using isolated deployment workspaces until the website source-control baseline is repaired.

## Do Not Promote To Memory

- Do not assume Game page, Progress page, or World Keys page copy was updated.
- Do not mark the website repo as clean.
- Do not treat `origin/main` as production source.

## Follow-Up Recommendations

1. Repair the website source-control baseline so production source can be deployed from Git cleanly.
2. Decide whether to update the Game page hero using the same deployment discipline.
3. Keep the isolated deployment workspace until the next stable website baseline is confirmed.
