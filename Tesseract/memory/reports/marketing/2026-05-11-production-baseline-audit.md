# Marketing Report - 2026-05-11 - Production Baseline Audit

## Task

Establish the safest available production baseline before any deployment of the approved Variant 1 homepage copy.

## Result

Production baseline status: candidate baseline identified, not yet converted into a clean deployment workspace.

Best available baseline candidate:

```text
C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site
```

Reason: this folder packages the same number of assets as the May 10 production deployment and matches key live-page signals for Game, Progress, and World Keys. The homepage differs because the approved Variant 1 copy has already been applied locally and has not been deployed.

No deployment was performed.

## Sources Reviewed

- Live site:
  - `https://the-world-beneath.com/`
  - `https://the-world-beneath.com/game/`
  - `https://the-world-beneath.com/progress/`
  - `https://the-world-beneath.com/world-keys/`
- Local website folder:
  - `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site`
- Git refs:
  - `origin/main`
  - `main`
  - `HEAD`
- Wrangler:
  - `npx wrangler --version`
  - `npx wrangler deployments status`
  - `npx wrangler deployments list`
  - `npx wrangler versions view c5c01c6d-ce03-45e1-91f6-da9a5210a95d`
  - `npx wrangler deploy --dry-run`
- Wrangler deploy logs:
  - `C:\Users\yrred\AppData\Roaming\xdg.config\.wrangler\logs\wrangler-2026-05-10_17-25-19_316.log`
- Decommission archive summary:
  - `C:\Users\yrred\Desktop\Archive\BobNet-BobCord-Daedalus-Decommission-20260510-121643\DECOMMISSION_SUMMARY.md`

## Key Findings

- Current production Worker version:
  - `c5c01c6d-ce03-45e1-91f6-da9a5210a95d`
- Production deployment created:
  - `2026-05-10T17:25:19.536Z`
- Production deployment author:
  - `twbmain@gmail.com`
- Wrangler source:
  - `Unknown (deployment)` / `Unknown (version_upload)`
- Wrangler version used locally:
  - `4.81.1`
- Wrangler reports an available update to:
  - `4.90.0`

## Deployment Source Clue

The May 10 Wrangler log shows the production deployment read assets from:

```text
C:\Users\yrred\Desktop\Archive\BobNet-BobCord-Daedalus-Decommission-20260510-121643\local\Desktop\BoB-Console\the-world-beneath-site
```

That exact folder no longer exists.

The archive contains older or partial website folders, but the inspected backup under `Bobs_Storage\backups\the-world-beneath-site` does not match the current full live website.

## Asset Count Match

The May 10 deploy log says:

```text
Read 2439 files from the assets directory
```

A dry-run from the current local website folder also reports:

```text
Read 2439 files from the assets directory
```

This is the strongest local evidence that the current website folder is the surviving source-equivalent candidate for the current live deployment.

## Live Page Signal Check

Live pages checked:

| Page | Live status | Local candidate status |
| --- | --- | --- |
| Home | Live uses pre-approved modernized copy | Local uses approved Variant 1 copy |
| Game | Live title and modern game-page signal match local | Match |
| Progress | Live title and roadmap signal match local | Match |
| World Keys | Live title and retired-key signal match local | Match |

Home difference is expected because Variant 1 has been applied locally but not deployed.

## Git Findings

- Current branch inspected:
  - `codex/archaeology-release-ready-step8`
- Latest local commit:
  - `920e4e3 Prepare archaeology release candidate`
- Current branch is 7 commits ahead of `origin/main`.
- `origin/main` still contains older homepage wording.
- The local website repo still has 691 changed entries:
  - 47 modified
  - 597 deleted
  - 47 untracked

Therefore, Git does not currently provide a clean production baseline.

## Wrangler Version Details

The current production version has:

- Handler: `fetch`
- Compatibility date: `2026-03-26`
- D1 binding: `TWB_DB`
- Asset binding: `ASSETS`
- Environment variables:
  - `ADMIN_EMAILS`
  - `ALLOW_FIRST_USER_ADMIN`
- Secrets present:
  - `ADMIN_BOOTSTRAP_CODE`
  - `BOB_FORGE_ADMIN_PASSWORD`

No secrets were read.

## Baseline Decision

Candidate baseline for the next step:

```text
C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site
```

This is not a clean Git baseline. It is a deployment-source candidate.

The next safe step is to create an isolated deployment workspace from this candidate, then prove the intended deployment diff is copy-only before any public deploy.

## Risks

- Deploying from `origin/main` could downgrade the live website.
- Deploying from the current dirty Git repo without isolation could publish unrelated historical or platform changes.
- The exact May 10 deployment source folder no longer exists.
- The current local folder is strongly supported as a candidate, but not mathematically proven to match every deployed asset byte-for-byte.
- Wrangler source metadata does not point to a Git commit.

## Memory-Worthy Notes

- Fact: current production Worker version is `c5c01c6d-ce03-45e1-91f6-da9a5210a95d`.
- Fact: May 10 deployment and current local dry-run both report `2439` asset files.
- Warning: Git refs are not the current production baseline.
- Warning: the deployment source folder named in the May 10 Wrangler log no longer exists.
- Decision candidate: use the current local website folder as the source candidate for an isolated deployment workspace, not as a direct deployment target.

## Do Not Promote To Memory

- Do not mark Variant 1 as deployed.
- Do not call the current dirty Git repo clean.
- Do not treat `origin/main` as production source.
- Do not delete or reset the dirty website folder.

## Follow-Up Recommendations

1. Create an isolated deployment workspace from the candidate folder.
2. In that workspace, preserve the production-like full site and the approved Variant 1 homepage copy.
3. Initialize or attach Git only inside the isolated workspace if needed for a clean diff gate.
4. Run `npx wrangler deploy --dry-run` in the isolated workspace.
5. Preview the isolated workspace through a served environment.
6. Ask for explicit approval before any real `npx wrangler deploy`.
