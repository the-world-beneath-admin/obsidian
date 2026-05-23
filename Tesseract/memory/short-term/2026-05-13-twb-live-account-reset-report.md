# TWB Live Account Reset Report - 2026-05-13

## Task

Reset the live `twb-core` account/user database for `the-world-beneath.com` so the user database starts fresh today, remove `yrrednarib@gmail.com` from the account system, remove BobNet/Bob Hub package metadata, and set up a fresh admin bootstrap key for recreating `twbmain@gmail.com` as the administrator account.

## Result

Completed.

The remote `twb-core` D1 database was cleared of live account/content rows while preserving schema and reference tables. BobNet/Bob Hub package metadata tables were cleared. A new Worker version containing `ADMIN_BOOTSTRAP_CODE` was created and deployed to 100% production traffic so the key is active for `twbmain@gmail.com` registration.

The admin bootstrap code itself was not written to this report.

## Files touched

- No website source files were edited for this reset.
- Temporary reset SQL was created at `C:\Users\yrred\AppData\Local\Temp\twb-live-account-reset-2026-05-13.sql` and removed after use.
- This report: `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-live-account-reset-report.md`

Existing untracked website docs from the earlier shared-platform planning pass remain:

- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\SHARED_GAME_PLATFORM_PLAN.md`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`

## Checks run

- Confirmed Wrangler login is associated with `twbmain@gmail.com`.
- Confirmed remote `twb-core` table access.
- Pre-reset spot counts:
  - `users`: 3
  - `forum_threads`: 8
  - `bob_packages`: 0
  - `platform_companion_cards`: 0
- Applied remote reset SQL to `twb-core`.
  - D1 final bookmark: `00000069-00000006-0000506a-f91cadd6f57e52a96e4cc2bd50e27888`
  - D1 import summary: 37 queries, 60 rows written
- Verified cleared account tables:
  - `users`: 0
  - `profiles`: 0
  - `sessions`: 0
  - `audit_log`: 0
  - `linked_game_clients`: 0
  - `game_profiles`: 0
- Verified cleared platform tables:
  - `platform_companion_cards`: 0
  - `platform_companion_locks`: 0
  - `platform_inventory_ledger`: 0
  - `platform_inventory_stacks`: 0
  - `platform_game_saves`: 0
  - `platform_user_origins`: 0
- Verified cleared forum content tables:
  - `forum_threads`: 0
  - `forum_replies`: 0
  - `forum_thread_votes`: 0
  - `forum_reply_votes`: 0
  - `forum_reports`: 0
- Verified cleared BobNet/Bob Hub metadata tables:
  - `bob_packages`: 0
  - `bob_package_versions`: 0
  - `bob_package_tags`: 0
  - `bob_package_downloads`: 0
  - `bob_package_ratings`: 0
  - `bob_package_reports`: 0
  - `bob_package_votes`: 0
  - `bob_package_review_packets`: 0
  - `bob_console_clients`: 0
- Verified preserved reference rows:
  - `forum_categories`: 21
  - `forum_groups`: 6
  - `platform_games`: 2
  - `platform_catalog`: 1
- Verified live API:
  - `https://the-world-beneath.com/api/health` returned `{ "ok": true, "service": "twb-core" }`
  - `https://the-world-beneath.com/api/me` returned `{ "user": null }`

## Cleanup performed

- Removed the temporary reset SQL file from `%TEMP%`.
- Did not create a local account-data backup, because the user explicitly wanted the account database cleared fresh.

## Risks

- Bob package metadata is cleared from D1. If R2 package binaries exist, they may now be orphaned because this task targeted metadata, not R2 object deletion.
- The live Worker version was changed only to activate the new secret. No website source edit was made in this reset pass.
- Current account creation still uses the old registration flow until the starter-pet account-creation implementation is completed.

## Memory-worthy notes

- The live user/account system was reset on 2026-05-13.
- `yrrednarib@gmail.com` no longer exists in the live `users` table.
- `twbmain@gmail.com` no longer exists in the live `users` table and must be recreated using the active admin bootstrap code.
- `ADMIN_EMAILS` in `wrangler.jsonc` already restricts admin bootstrap to `twbmain@gmail.com`.
- BobNet/Bob Hub package metadata tables were cleared.

## Do not promote to memory

- Do not store or promote the admin bootstrap key.
- Do not treat this as completion of the starter-pet account creation implementation.

## Next recommended gate

Recreate `twbmain@gmail.com` first using the active admin bootstrap code. Then recreate `yrrednarib@gmail.com` as a normal player account without the admin code. After that, continue with the hardened account-creation/starter-pet implementation gate.
