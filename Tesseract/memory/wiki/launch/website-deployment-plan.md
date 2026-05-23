# Website Deployment Plan

## Purpose

Safely publish approved website copy changes for The World Beneath without deploying unrelated local website work.

## Current Status

Status: Homepage copy deployed and live-verified. Source-control baseline repaired and merged into `main`.

The approved Variant 1 homepage copy is applied locally to:

```text
C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\index.html
```

The local served preview renders correctly at:

```text
http://127.0.0.1:8000/
```

Deployment performed on 2026-05-11 from the isolated deployment workspace after explicit user approval.

Isolated deployment workspace:

```text
C:\Users\yrred\Desktop\Marketing\Websites\twb-homepage-copy-deploy-20260511
```

Served preview:

```text
http://127.0.0.1:8001/
```

Dry-run status:

```text
Passed - 180.63 KiB / gzip 34.23 KiB
```

Deployment result:

```text
Uploaded exactly one changed static asset: /index.html
Production version: 02ef6cfa-a1a6-4ba7-bfb0-715d63e87791
```

Source-control baseline result:

```text
Branch: codex/website-production-baseline-20260511
Commit: f510e2b
Status: Merged into main
PR: https://github.com/dodo-arcforge-interactive/the-world-beneath-site/pull/1
Merge commit: d39958b1e546b506e3e903fa91663ec57ae8a5a8
Dry-run: 180.63 KiB / gzip 34.23 KiB
```

## Production Baseline Audit - 2026-05-11

Historical production Worker version before the approved homepage-copy deployment:

```text
c5c01c6d-ce03-45e1-91f6-da9a5210a95d
```

Production deployment timestamp:

```text
2026-05-10T17:25:19.536Z
```

The May 10 Wrangler deployment log says the deployment read `2439` files from the assets directory. A dry-run from the current local website folder also reads `2439` files.

Best available deployment-source candidate:

```text
C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site
```

Important: this is a candidate baseline, not a clean Git baseline. It must be copied into an isolated deployment workspace before any deploy.

## Deployment Shape

- Site: `https://the-world-beneath.com/`
- Repo: `https://github.com/dodo-arcforge-interactive/the-world-beneath-site.git`
- Local repo: `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site`
- Current branch inspected: `codex/archaeology-release-ready-step8`
- Current clean baseline branch: `codex/website-production-baseline-20260511`
- Current clean baseline commit: `f510e2b`
- Current merged baseline commit on `main`: `d39958b1e546b506e3e903fa91663ec57ae8a5a8`
- Worker entrypoint: `worker.js`
- Cloudflare config: `wrangler.jsonc`
- Static assets binding: `ASSETS`
- Static asset directory: repo root
- Deploy command recorded in repo README: `npx wrangler deploy`

## Safety Findings - 2026-05-11

- The working tree had 691 changed entries before deployment planning:
  - 47 modified
  - 597 deleted
  - 47 untracked
- The current dirty repo must not be deployed as-is.
- After `git fetch origin`, `origin/main` still contains the older "Community through shared story" homepage wording.
- `main`, `origin/main`, and `HEAD` do not appear to contain the same modernized homepage wording currently visible on the live site.
- Current branch `codex/archaeology-release-ready-step8` is 7 commits ahead of `origin/main` and 1 commit ahead of local `main`.
- A clean checkout from `main` or `origin/main` may downgrade the live website if used without confirming the production baseline.
- Direct `file://` previews are invalid for visual QA because root-relative assets can fail.
- The source-control baseline was repaired on `codex/website-production-baseline-20260511` at commit `f510e2b` and merged into `main` as commit `d39958b1e546b506e3e903fa91663ec57ae8a5a8`.
- Future website work should branch from updated `main`.
- The user approved removing old archaeology, archaeology story, Bob Forge, and archaeology map material, and approved keeping website wiki additions.

## Approved Deployment Scope

For this deployment, only the approved homepage copy should change.

Allowed file:

```text
index.html
```

Approved copy changes:

- Page title: `The World Beneath - Dungeon Runs, Creature Growth, Shared-World RPG`
- Hero line: `Run dungeons. Grow creatures. Shape the world beneath.`
- Hero body: `The World Beneath is a shared-world RPG where dungeon runs feed creature growth, crafting, inventory progression, and a larger hidden world shaped by player societies.`
- CTA direction: `Follow development, join the community, and help shape what comes next.`
- Matching meta, Open Graph, Twitter, and structured-data descriptions.

Out of scope:

- Game page copy
- Progress page copy
- World Keys page copy
- CSS or visual design changes
- Worker/API changes
- D1 migrations
- R2 uploads
- Archaeology route, asset, or deletion cleanup

## Formal Deployment Plan - 11 Steps

1. Freeze the dirty website workspace.

Do not run `git add .`, do not deploy, and do not clean or reset the current folder. The dirty state may contain user work or partially completed older site work.

2. Establish the production baseline.

Identify the exact source state that matches the currently live full website. Do not assume `main`, `origin/main`, or the current branch is the production baseline until verified.

3. Create an isolated deployment workspace.

Use a fresh clone, clean worktree, or separate copy based on the verified production baseline. The deployment workspace should not inherit the 691 dirty entries from the current folder.

Current recommendation: create the isolated workspace from the candidate folder identified in the production baseline audit, not from `origin/main`.

4. Apply only the approved homepage copy patch.

Change only `index.html`. No CSS, worker, route, migration, account, forum, wiki, World Key, or archaeology files should change in this deployment.

5. Run the diff gate.

Before preview or deployment, verify:

```powershell
git status --short
git diff --stat
```

Expected result:

```text
M index.html
```

Any other changed file blocks deployment until reviewed.

6. Preview through a served environment.

Use either a local static server, `wrangler dev`, or a Cloudflare preview. Do not use direct `file://` previews.

Known working static preview command:

```powershell
python -m http.server 8000 --bind 127.0.0.1 --directory "C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site"
```

7. Run visual and console checks.

Check:

- Home page first viewport
- Header/menu
- CTA buttons
- Link to Game page
- Link to Register page
- Discord link
- Browser console warnings/errors
- Desktop and mobile widths if possible

8. Run deployment preflight.

For this copy-only deployment:

- Do not run D1 migrations.
- Do not change Worker secrets.
- Do not upload R2 assets.
- Confirm `wrangler.jsonc` still targets `the-world-beneath.com` and `www.the-world-beneath.com`.

9. Deploy only from the clean deployment workspace.

Run:

```powershell
npx wrangler deploy
```

Only proceed if the diff gate still shows only `index.html`.

Completed on 2026-05-11 after explicit approval. Future deployments should still use a clean Git baseline once source control is repaired.

10. Verify the live site after deployment.

Check:

- `https://the-world-beneath.com/`
- Page title
- Hero line
- Hero body
- CTA direction
- CSS/images loaded
- Browser console warnings/errors
- Links to `/game/`, `/progress/`, `/world-keys/`, and `/register/`

11. Record the deployment result.

Update:

- `memory/log.md`
- `memory/wiki/launch/launch-checklist.md`
- `memory/wiki/marketing/copy-bank.md`
- A deployment report under `memory/reports/marketing/`

Mark the approved homepage copy as deployed only after live verification passes.

## Rollback Rule

Do not improvise rollback during a panic.

Before deployment, identify the previous Cloudflare Worker deployment/version in the Cloudflare dashboard or Wrangler environment. If live verification fails, roll back to that previous known-good deployment and record what failed.

## Hard Stop Conditions

Stop before deployment if:

- More than `index.html` is changed in the clean deployment workspace.
- The deploy workspace does not match the current full live website baseline.
- The page renders unstyled or with missing images in a served preview.
- The browser console shows new homepage errors.
- The deploy command asks for account, route, database, or secret changes unrelated to the copy update.
- The user has not approved moving from preview to deploy.
