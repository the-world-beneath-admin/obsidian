# Current Website Admin And Support Task

## Status

Active - live foundation deployed 2026-05-22; admin-session smoke and game-side report button remain.

## Scope

Shared website/platform work for The World Beneath website:

```text
C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site
```

This is website/shared platform work, not main Unity, Garden, Alchemy, Trenchworks, marketing desktop app, or sprite automation work.

## Goal

Build the foundation for:

1. Admin-only member/customer visibility:
   - account totals
   - active/non-banned member counts
   - usernames / public handles
   - email addresses where already stored in the account database
   - safe email-prep/export surface
2. Bug reporting and customer-service tickets:
   - user-facing report/complaint submission API
   - support/ticket database
   - game/source fields so reports can come from current games and website
   - admin queue for viewing, filtering, assigning/statusing, and resolving tickets

## Important Email Boundary

First pass should not send bulk email automatically.

Implement a safe admin-only foundation such as:

- member list / counts
- copy/export recipient list for eligible users
- saved admin message drafts or email-campaign notes if useful
- future provider integration notes

Do not add live email sending until provider choice, account permissions, unsubscribe handling, rate limits, audit logs, and platform/compliance expectations are reviewed.

## Read First

- [[hot]]
- [[index]]
- [[wiki/game-dev/project-hierarchy]]
- [[wiki/shared-platform/overview]]
- [[wiki/shared-platform/account-and-auth]]
- [[wiki/shared-platform/implementation-roadmap]]
- [[wiki/shared-platform/open-questions]]
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\AGENTS.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\README.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\docs\architecture.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\docs\testing.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\docs\conventions.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\docs\common-pitfalls.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\SHARED_GAME_PLATFORM_PLAN.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\worker.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\admin\index.html`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\js\account.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\css\styles.css`

## Likely Files

- `worker.js`
- `admin\index.html`
- `assets\js\account.js`
- `assets\css\styles.css`
- `migrations\0020_admin_support_tickets.sql` or next available migration number if `0020` is taken
- `TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`
- optional docs under `docs\`

## Required Data Model Direction

Support tickets should support:

- ticket id
- submitter user id when logged in
- submitter email / contact field when supplied
- source game id / surface, such as `website`, `the-garden`, `the-alchemy-lab`, `twb-trenchworks`, `main-game`
- category, such as `bug`, `support`, `complaint`, `feedback`
- severity or priority
- status, such as `open`, `triage`, `in_progress`, `waiting`, `resolved`, `dismissed`
- title / summary
- body / reproduction steps
- client context JSON for game version, browser/device, save id, screen, build channel, or logs
- admin notes / resolution
- created / updated / resolved timestamps

## Allowed Write Paths

- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\worker.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\admin\`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\js\`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\css\`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\migrations\`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\docs\`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\`

## Forbidden Write Paths

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\log.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\`
- `C:\Users\yrred\Desktop\Marketing\TWB-Marketing\`
- remote D1 migrations
- live deployment
- Cloudflare secrets or production configuration changes
- destructive git operations, broad staging, blanket cleanup, reset, or revert

## Hard Rules

- Admin member/customer data must require admin authentication.
- Do not expose email addresses to non-admin users.
- Do not add automatic bulk email sending in this pass.
- Do not run remote D1 migrations or live deploys without explicit user approval.
- Keep public report submission rate-limitable and validate payload size.
- Preserve backward compatibility for existing account, forum, and platform APIs.
- Workers and child subagents must not update permanent Obsidian memory.

## Checks

Run from:

```powershell
cd C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site
```

Preferred:

```powershell
powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1
```

If full dry-run is too slow:

```powershell
powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1 -SkipWranglerDryRun
```

For migration work:

```powershell
npx wrangler d1 migrations apply twb-core --local
```

Blocked without explicit approval:

```powershell
npx wrangler d1 migrations apply twb-core --remote
npx wrangler deploy
```

## Done Criteria

- Done locally - Admin page shows member/account totals and existing user list data to admin users only.
- Done locally - Admin page includes a safe email-prep/export surface, not automatic bulk sending.
- Done locally - Support/ticket migration exists and has applied locally.
- Done locally - Public/user ticket submission API exists with source game/surface and category fields.
- Done locally - Admin ticket queue API and UI exist for listing/filtering/updating tickets.
- Done locally - API contract notes are updated for games to call bug/customer-service submission later.
- Done locally - Local checks passed, including Wrangler dry-run.
- Done locally - Child and orchestrator review reports were written to `memory/short-term/`.
- Done live - Remote D1 migrations `0015`-`0020` applied to `twb-core`.
- Done live - Worker/assets deployed to `the-world-beneath.com` and `www.the-world-beneath.com` as version `3f30b86b-f992-4b49-8787-bfe5110d5900`.
- Done live - Public smoke checks passed for root/admin pages, anonymous admin API rejection, ticket validation rejection, and remote migration list.
- Remaining - Manual admin-session browser smoke with seeded users/tickets.
- Remaining - Game-side Report Bug button/client helper.
- Remaining - Rate limiting/abuse controls before broad public exposure.
- Remaining - Provider-safe email sending plan before any real bulk/customer email integration.

## Report Destination

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\YYYY-MM-DD-website-admin-support-worker-report.md
```
