# BobNet Package Hub Retirement

## Summary

The Bob/BobNet package-hub system has been removed from the local website shared-platform source, but production cleanup is not complete until the remote database migrations and deployment gate are explicitly approved and run.

## Source-Side Status

Reported complete in local source:

- Bob package, catalog, console-client, and admin Bob moderation routes removed from `worker.js`.
- Admin account page no longer renders Bob package review/report panels.
- Site hooks, tracking, forum/community copy, CSS, and Bob-named image assets were scrubbed.
- Fresh database rebuild paths no longer create Bob forum seed categories or Bob package tables.
- Old Bob package migration source files `0007`, `0008`, and `0009` were deleted from source.
- Cleanup migration `migrations\0016_remove_retired_package_hub.sql` exists for existing databases.

## Preserved Shared Platform Work

The cleanup did not intentionally revert shared account, starter-pet, game-link, or Garden-export work. The source tree still includes:

- `migrations\0014_account_creation_starter_pets.sql`
- `migrations\0015_garden_transfer_exports.sql`
- `SHARED_GAME_PLATFORM_PLAN.md`
- `TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`
- `assets\js\twb-platform-client.js`
- `assets\images\starter-pets\`

## Production Status

Not complete:

- Remote D1 still needs pending migrations `0015_garden_transfer_exports.sql` and `0016_remove_retired_package_hub.sql`.
- Live deployment has not been performed for this cleanup.
- Cloudflare secret `BOB_FORGE_ADMIN_PASSWORD` still exists and must not be deleted without explicit approval.

## Checks Reported

- `node --check worker.js` passed.
- `node --check assets\js\site.js` passed.
- `node --check assets\js\account.js` passed.
- `npx wrangler deploy --dry-run` passed.
- `npx wrangler d1 migrations apply twb-core --local` passed and applied `0016_remove_retired_package_hub.sql` locally.
- Local D1 checks found no `bob%` tables, forum categories, or forum groups after the cleanup migration.
- Remote migration list showed `0015_garden_transfer_exports.sql` and `0016_remove_retired_package_hub.sql` pending.
- Served Wrangler dev smoke was inconclusive due to local process/timeouts.

## Rules

- Do not assume production is clean until remote migrations, deploy, and live verification are complete.
- Do not delete `BOB_FORGE_ADMIN_PASSWORD` without explicit user approval.
- Do not run remote D1 migrations without explicit user approval.
- Do not deploy without explicit user approval.

## Next Gate

Run a narrow production-readiness task:

- review the diff
- retry served preview if desired
- prepare the exact live sequence for remote migrations `0015` and `0016`
- optionally delete `BOB_FORGE_ADMIN_PASSWORD` only if approved
- deploy only if approved
- live-verify account, register, profile, forum, and shared-platform routes

## Sources

- [[short-term/2026-05-13-twb-shared-platform-bobnet-removal-final-decommission-report]]
