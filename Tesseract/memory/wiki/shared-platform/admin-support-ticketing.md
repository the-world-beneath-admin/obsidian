# Admin Support Ticketing

## Status

Website/shared-platform foundation implemented locally and deployed live on 2026-05-22.

## Scope

This page covers the website admin member/customer surface and support-ticket/customer-service foundation in:

```text
C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site
```

## Implemented Locally

- Admin member stats on `/admin/`.
- Admin-only user list remains available with emails, display names, public handles, role, tier, and status.
- Manual email-prep/export list for active, non-banned accounts.
- No automatic bulk email sending.
- D1 support-ticket tables in `migrations\0020_admin_support_tickets.sql`.
- Public/authenticated ticket creation route:
  - `POST /api/support/tickets`
- Admin ticket queue routes:
  - `GET /api/admin/support/tickets`
  - `PATCH /api/admin/support/tickets/:ticketId`
- Admin ticket queue UI on `/admin/`.
- Ticket contract notes in `TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`.

## Security Decisions

- Member emails and support-ticket admin views must be admin-only.
- PII/admin ticket routes use a website-session admin guard, not game-client bearer auth.
- Email is manual-prep/export only until provider choice, consent rules, unsubscribe handling, rate limits, and audit logging are reviewed.
- Support-ticket submission is size-limited and validates category, priority, severity, status, title, body, source game/surface, and client context.
- Support tickets are separate from forum moderation reports.

## Ticket Categories

- `bug`
- `support`
- `complaint`
- `feedback`

## Ticket Statuses

- `open`
- `triage`
- `in_progress`
- `waiting`
- `resolved`
- `dismissed`

## Live Deployment

Remote D1 migrations applied on 2026-05-22:

- `0015_garden_transfer_exports.sql`
- `0016_remove_retired_package_hub.sql`
- `0017_global_achievement_framework.sql`
- `0018_platform_pet_catalog_inventory.sql`
- `0019_backfill_companion_world_key_skills.sql`
- `0020_admin_support_tickets.sql`

Worker/assets deployed to:

- `the-world-beneath.com`
- `www.the-world-beneath.com`

Cloudflare Worker version:

```text
3f30b86b-f992-4b49-8787-bfe5110d5900
```

Post-deploy smoke:

- `/` returned `200`.
- `/admin/` returned `200`.
- `/api/admin/users` returned anonymous `401`.
- `/api/admin/support/tickets` returned anonymous `401`.
- Empty `POST /api/support/tickets` returned validation `400` without creating a ticket.
- Remote D1 migration list reported no migrations to apply.

Public ticket entry points added and deployed on 2026-05-22:

- Contact page form at `/contact/#support-ticket`.
- Forum ticket buttons on the forum index, board view, and thread view.
- Shared footer `Submit Ticket` link pointing to `/contact/#support-ticket`.
- Shared `site.js` support-ticket form handler posts to `POST /api/support/tickets`.

## Current Blockers

- Manual admin-session browser test with seeded users/tickets is still required.
- Actual in-game Report Bug buttons are not wired yet.
- Rate limiting / abuse controls should be added before broad public exposure.
- Email-provider integration is blocked pending consent/unsubscribe/compliance and provider planning.

## Verified Checks

Bob/orchestrator re-ran after patching the admin guard:

```powershell
node --check worker.js
node --check assets\js\account.js
powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1 -SkipWranglerDryRun
npx wrangler d1 migrations apply twb-core --local
powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1
```

Results:

- JavaScript syntax checks passed.
- Local verification passed.
- Local D1 migration check reported no migrations to apply because the child worker had already applied `0020` locally.
- Wrangler dry-run passed.

Live deployment checks on 2026-05-22:

```powershell
npx wrangler d1 migrations apply twb-core --remote
npx wrangler deploy
npx wrangler d1 migrations list twb-core --remote
curl.exe -I https://the-world-beneath.com/
curl.exe -I https://the-world-beneath.com/admin/
curl.exe -s -o NUL -w "%{http_code} %{content_type}\n" https://the-world-beneath.com/api/admin/users
curl.exe -s -o NUL -w "%{http_code} %{content_type}\n" https://the-world-beneath.com/api/admin/support/tickets
curl.exe -s -o NUL -w "%{http_code} %{content_type}\n" -X POST https://the-world-beneath.com/api/support/tickets -H "Content-Type: application/json" --data "{}"
```

## Sources

- [[briefs/current-website-admin-support-task]]
- [[short-term/2026-05-22-website-admin-support-implementation-child-report]]
- [[short-term/2026-05-22-website-admin-support-orchestrator-review]]
