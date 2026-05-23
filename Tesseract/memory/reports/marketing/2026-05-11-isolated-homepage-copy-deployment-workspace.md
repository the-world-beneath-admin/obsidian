# Marketing Report - 2026-05-11 - Isolated Homepage Copy Deployment Workspace

## Task

Create an isolated deployment workspace for the approved Variant 1 homepage copy without touching or deploying from the dirty website repo.

## Result

Created isolated deployment workspace:

```text
C:\Users\yrred\Desktop\Markeing\Websites\twb-homepage-copy-deploy-20260511
```

No deployment was performed.

## Source

Copied from the production-baseline candidate:

```text
C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site
```

Excluded from the isolated copy:

- `.git`
- `.wrangler`
- `*.log`

Reason: these are not needed for the deployable static/Worker source and should not be part of a clean deployment candidate.

## Approved Copy Present

Confirmed in the isolated workspace:

- Page title: `The World Beneath - Dungeon Runs, Creature Growth, Shared-World RPG`
- Hero line: `Run dungeons. Grow creatures. Shape the world beneath.`
- Hero body begins: `The World Beneath is a shared-world RPG where dungeon runs feed`
- CTA direction begins: `Follow development, join the community, and help shape what`

## Checks Run

### Wrangler Dry Run

Command:

```powershell
npx wrangler deploy --dry-run
```

Result:

- Passed.
- Read `258` files from the isolated workspace.
- Total upload: `180.63 KiB`
- Gzip upload: `34.23 KiB`
- Bindings reported:
  - `TWB_DB`
  - `ASSETS`
  - `ADMIN_EMAILS`
  - `ALLOW_FIRST_USER_ADMIN`

Note: the isolated workspace reads fewer raw files than the source candidate because `.git`, `.wrangler`, and log files were intentionally excluded. The deployable upload size matches the earlier candidate dry run.

### Served Preview

Preview URL:

```text
http://127.0.0.1:8001/
```

Result:

- Homepage rendered with full styling.
- Approved Variant 1 copy rendered in the hero.
- Browser warning/error quick check: `0`.

### Route Checks

All returned `200`:

- `/`
- `/game/`
- `/progress/`
- `/world-keys/`
- `/register/`
- `/assets/css/styles.css`
- `/assets/js/site.js?v=brand-seo-20260429`

Key page signals present:

- `/game/`: `A living game world beneath the ordinary one`
- `/progress/`: `The build path for the game world`
- `/world-keys/`: `No public World Key game is live right now`

## Deployment Readiness

Status: ready for final user approval gate before real deployment.

The next command would be:

```powershell
npx wrangler deploy
```

from:

```text
C:\Users\yrred\Desktop\Markeing\Websites\twb-homepage-copy-deploy-20260511
```

Do not run that command without explicit user approval.

## Risks

- The isolated workspace is a source candidate, not a Git-clean branch.
- The exact May 10 deployment source folder no longer exists.
- The current deployment would publish from a copied workspace rather than from `origin/main`.
- Wrangler reports an available update from `4.81.1` to `4.90.0`; do not update Wrangler mid-release unless separately tested.

## Memory-Worthy Notes

- Fact: isolated deployment workspace created at `C:\Users\yrred\Desktop\Markeing\Websites\twb-homepage-copy-deploy-20260511`.
- Fact: isolated dry-run upload size is `180.63 KiB / gzip: 34.23 KiB`.
- Fact: isolated served preview passed homepage visual and console quick check.
- Warning: do not deploy without explicit approval from this point.

## Do Not Promote To Memory

- Do not mark Variant 1 as deployed.
- Do not treat the dirty source repo as safe.
- Do not run migrations for this copy-only deployment.

## Follow-Up Recommendation

Ask the user for final deployment approval. If approved, deploy only from the isolated workspace and immediately verify the live site.
