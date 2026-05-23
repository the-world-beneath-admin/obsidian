# Launch Checklist

## Website Preview Rules

- Use the live site, a deployment preview, or a local web server for visual QA.
- Do not judge the website by opening local HTML files directly through `file://`.
- Root-relative paths such as `/assets/css/styles.css` are expected to fail or misresolve in direct-file previews.

## Deployment Safety

- Do not deploy from a dirty website repo without first identifying unrelated local changes.
- Confirm the exact changed files intended for deployment.
- Preview approved copy changes in a served environment before publishing.
- Keep live-site styling and existing page structure intact unless a design task explicitly changes them.
- Follow [[website-deployment-plan]] before publishing the approved homepage copy.
- For copy-only homepage deployment, the clean deployment workspace should show only `M index.html`.
- For future website work, start from updated `main` at or after merge commit `d39958b1e546b506e3e903fa91663ec57ae8a5a8`.
- Do not run D1 migrations, change Worker secrets, or alter R2 assets for copy-only homepage deployment.

## Platform Readiness

- Follow [[steam-coming-soon-readiness-plan]] before publishing or promoting a Steam Coming Soon page.
- Follow [[world-keys-kickstarter-itch-readiness-plan]] before releasing the first two free World Keys on itch.io or launching a Kickstarter pre-launch page.
- Follow [[kickstarter-phase-one-strategy]] and [[kickstarter-readiness-board]] before publishing the Kickstarter pre-launch page or campaign page.
- Treat Steam as the main-game wishlist funnel.
- Treat itch.io as the first free playable World Key release channel.
- Treat Kickstarter as the funding and campaign layer around playable proof, not as the free-game host.

## Current Deployment Status

- 2026-05-11: Approved homepage copy changes were applied to the local website source only.
- 2026-05-11: No deployment was performed.
- 2026-05-11: The public site at `https://the-world-beneath.com/` was confirmed to be a full styled website.
- 2026-05-11: The local homepage source was confirmed to render with full styling through `http://127.0.0.1:8000/`.
- 2026-05-11: Clean deployment plan created. Deployment is blocked until a production baseline matching the live site is established.
- 2026-05-11: Production baseline audit completed. Current production Worker version is `c5c01c6d-ce03-45e1-91f6-da9a5210a95d`. The current local website folder is the best available deployment-source candidate, but still needs an isolated deployment workspace before publishing.
- 2026-05-11: Isolated deployment workspace created at `C:\Users\yrred\Desktop\Marketing\Websites\twb-homepage-copy-deploy-20260511`. Dry-run passed and served preview at `http://127.0.0.1:8001/` rendered correctly. Awaiting explicit deployment approval.
- 2026-05-11: Approved homepage copy deployed. Wrangler uploaded only `/index.html`; new production Worker version is `02ef6cfa-a1a6-4ba7-bfb0-715d63e87791`. Live verification passed.
- 2026-05-11: Website source-control baseline repaired on branch `codex/website-production-baseline-20260511` at commit `f510e2b`. User approved old archaeology/Bob Forge removals and website wiki additions. PR #1 was merged into `main` at merge commit `d39958b1e546b506e3e903fa91663ec57ae8a5a8`; local `main` was fast-forwarded and Wrangler dry-run verified.
- 2026-05-11: Local SEO/site growth branch `codex/seo-site-growth-pass-20260511` created from merged `main`. Metadata, structured data, robots, and sitemap edits passed local served checks and Wrangler dry-run. No deployment performed.
- 2026-05-11: SEO/site growth PR #2 merged into `main` at `cce7f30efb3c46e8cede2dc15a66bca0b90294f0`. Cloudflare did not auto-deploy after merge, so deployment was performed manually with Wrangler after user approval. New production version is `734f5282-affa-43b4-90ec-2f9d36a315c8`; live verification passed.
- 2026-05-11: Platform readiness plans created for Steam Coming Soon and for the first two free World Keys on itch.io with Kickstarter as the campaign layer. No platform pages were published.
- 2026-05-11: Local pre-live World Keys funnel source update applied on branch `codex/world-keys-prelive-funnel-20260511`. Changed `index.html` and `world-keys/index.html`, served preview at `http://127.0.0.1:8002/`, and Wrangler dry-run passed after generated Playwright artifacts were removed. No deployment performed.
- 2026-05-11: User approved deployment. Deployed pre-live World Keys funnel with Wrangler; uploaded exactly `/index.html` and `/world-keys/index.html`. Production version is `6a0ee9b8-c27c-4ed9-be6a-ddd38da54d55`. Live verification passed. PR #3 was merged into `main` at `1e55a67`.
- 2026-05-22: Kickstarter package intaken under `memory/raw/launch/kickstarter/2026-05-22/`. Active internal recommendation is a `$150,000` Phase One campaign, Garden as free proof before launch, Trenchworks as first paid digital reward with Steam preferred and itch.io/direct fallback, Creator Kit/canon archive/AI coordinator as platform deliverables, and strict no-investment/no-unlimited-IP/no-physical-reward guardrails.
