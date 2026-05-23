# Website Admin/Support Implementation Child Report

Date: 2026-05-22

## Scope

Website/shared platform only:

```text
C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site
```

## What Changed

- Added a local D1 migration for support/customer-service tickets and ticket events.
- Added public/authenticated ticket submission route:
  - `POST /api/support/tickets`
- Added admin-only support queue routes:
  - `GET /api/admin/support/tickets`
  - `PATCH /api/admin/support/tickets/:ticketId`
- Extended `GET /api/admin/users` with admin member stats and an active-account email export list.
- Added admin page UI for:
  - member/account stats
  - manual email-prep list copy
  - ticket filtering by status/category/source game
  - ticket status/priority/severity/admin-notes/resolution updates
- Updated shared platform client contract notes so games can later wire bug-report buttons to the support-ticket API.

## Files Touched

- `worker.js`
- `admin/index.html`
- `assets/js/account.js`
- `assets/css/styles.css`
- `migrations/0020_admin_support_tickets.sql`
- `TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-website-admin-support-implementation-child-report.md`

## Checks Run

From `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site`:

```powershell
node --check worker.js
node --check assets\js\account.js
npx wrangler d1 migrations apply twb-core --local
powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1 -SkipWranglerDryRun
powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1
```

Results:

- `node --check worker.js` passed.
- `node --check assets\js\account.js` passed.
- Local D1 migration applied successfully: `0020_admin_support_tickets.sql`.
- Fast local verification passed.
- Full local verification passed, including Wrangler dry-run.

## Cleanup Performed

- No broad cleanup was performed.
- No staging, commit, reset, remote migration, or live deploy was run.

## Risks

- The admin email surface is intentionally a manual export/prep list only. A real email provider integration still needs unsubscribe handling, consent policy, rate limits, audit logging, and provider selection.
- Public ticket submission is payload-validated and size-limited, but production hardening should add stronger rate limiting/abuse controls before large public exposure.
- The admin UI was syntax/build verified but not manually browser-tested with a seeded local admin session in this pass.

## Memory-Worthy Notes

- Website/shared platform now has the first support-ticket/customer-service foundation.
- Bug reports, complaints, support requests, and feedback share one ticket table with category/status fields.
- Games should submit tickets through `POST /api/support/tickets`; only admins should read/update the queue.
- Email remains manual-prep only, not automatic sending.

## Follow-Up Recommendations

1. Seed or create local admin test data and manually verify `/admin/` ticket/member flows.
2. Add a small shared bug-report client helper for browser World Keys.
3. Add provider-safe email campaign planning only after consent/unsubscribe/compliance decisions.
4. Consider adding per-IP/account rate limits for `POST /api/support/tickets` before public launch.
