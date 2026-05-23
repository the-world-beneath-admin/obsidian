# Marketing Report - 2026-05-11 - Clean Homepage Copy Deployment Plan

## Task

Create a clean deployment plan for publishing the approved Variant 1 homepage copy without deploying unrelated website changes.

## Result

Created a formal 11-step deployment plan at:

```text
memory/wiki/launch/website-deployment-plan.md
```

No deployment was performed.

## Sources Reviewed

- Live site baseline: `https://the-world-beneath.com/`
- Local served preview: `http://127.0.0.1:8000/`
- Website repo: `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site`
- `README.md`
- `wrangler.jsonc`
- `.assetsignore`
- `index.html`
- `git status --short`
- `git diff -- index.html`
- `git fetch origin`
- `git show origin/main:index.html`

## Key Findings

- The public site is already a full styled website.
- The approved Variant 1 homepage copy renders correctly in the served local preview.
- The website deploy shape is a Cloudflare Worker with static assets served from the repo root through the `ASSETS` binding.
- The recorded deploy command is `npx wrangler deploy`.
- The current website repo is not safe to deploy as-is.
- The working tree had 691 changed entries during inspection: 47 modified, 597 deleted, and 47 untracked.
- After `git fetch origin`, `origin/main` still contains the older "Community through shared story" homepage wording.
- `main`, `origin/main`, and `HEAD` appear older than the currently live modernized homepage wording, so a clean checkout from those refs may not be the correct live baseline.
- Current branch `codex/archaeology-release-ready-step8` is 7 commits ahead of `origin/main` and 1 commit ahead of local `main`.

## Recommendation

Do not deploy from the current dirty website folder.

First establish a clean production baseline that matches the live full website, then apply only the approved `index.html` homepage copy change in an isolated deploy workspace.

## Deployment Scope

Allowed for this deployment:

- `index.html`

Not allowed for this deployment:

- CSS changes
- Worker/API changes
- D1 migrations
- R2 uploads
- Account/forum/wiki/platform changes
- Game page copy
- Progress page copy
- World Keys page copy
- Archaeology cleanup or restoration

## Checks Already Run

- Confirmed live site opens with styling and no quick-check browser warnings/errors.
- Confirmed local served preview opens with styling and no quick-check browser warnings/errors.
- Confirmed approved homepage copy appears in the served local preview.
- Confirmed repo deployment configuration points at Cloudflare Worker routes for `the-world-beneath.com` and `www.the-world-beneath.com`.

## Risks

- Deploying the dirty repo could publish hundreds of unrelated file changes and deletions.
- Deploying from `main` or `origin/main` without baseline verification could downgrade the live website.
- Direct `file://` preview can falsely suggest the site is unstyled.
- Copy-only deploys should not run migrations or alter Worker secrets.

## Memory-Worthy Notes

- Warning: the current website repo is not a valid deployment source until a clean baseline is established.
- Decision candidate: all public-site deployments should pass a single-file or intentional-file diff gate before deploy.
- Fact: the clean homepage copy deployment plan has 11 steps.

## Do Not Promote To Memory

- Do not mark the Variant 1 homepage copy as deployed.
- Do not treat `main` or `origin/main` as the production baseline until verified.
- Do not assume the 691 dirty entries are disposable.

## Follow-Up Recommendations

1. Establish the clean production baseline.
2. Create an isolated deployment workspace.
3. Apply only the approved `index.html` copy changes.
4. Run served preview checks.
5. Ask for explicit user approval before running `npx wrangler deploy`.
