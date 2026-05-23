# Final Decommission Report - 2026-05-13 - TWB Shared Platform BobNet Removal

## Window identity
- Project/window name: TWB Shared Platform BobNet Removal
- Scope: Shared platform/account system cleanup for The World Beneath website source
- Code/project directory: `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site`
- Related Obsidian lane, if known: Shared Platform / Account Systems

## Current state
The website-owned shared platform/account source now has the Bob/BobNet package-hub system removed from source code and fresh database build paths. The Worker no longer exposes Bob package, Bob catalog, Bob console-client, or admin Bob moderation routes. The admin account page no longer renders or loads Bob package review/report panels. Site hooks, tracking, forum/community copy, CSS, and Bob-named image assets were scrubbed.

The shared account/starter-pet/game-link/Garden-export work remains in the source tree and was not intentionally reverted. A database cleanup migration exists at `migrations\0016_remove_retired_package_hub.sql` to drop old Bob package tables and forum rows from existing databases when the remote migration gate is approved.

Unfinished: live production cleanup still needs remote D1 migration approval, optional live secret deletion approval, and a deployment gate. No live deploy or remote migration was performed in this final cleanup pass.

## Files changed
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\worker.js`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\admin\index.html`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\assets\css\styles.css`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\assets\downloads\theme-kits\twb-ios-webclips.mobileconfig`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\assets\js\account.js`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\assets\js\site.js`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\blog\2026\05\ashmantle-mastiff-threshold-defender.html`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\blog\2026\05\glyphwake-spawn-magic-freshwater-family.html`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\blog\2026\05\start-with-initiation-book-audiobook.html`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\community\index.html`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\community\forum\index.html`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\community\forum\board\index.html`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\community\forum\thread\index.html`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\login\index.html`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\profile\index.html`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\migrations\0001_twb_core.sql`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\migrations\0002_forum_core.sql`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\migrations\0006_forum_game_first_seed.sql`
- Deleted: `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\migrations\0007_bob_hub_packages.sql`
- Deleted: `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\migrations\0008_bob_hub_review_votes.sql`
- Deleted: `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\migrations\0009_bob_hub_provenance.sql`
- Added: `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\migrations\0016_remove_retired_package_hub.sql`
- Deleted Bob image assets under `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\assets\images\`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\SHARED_GAME_PLATFORM_PLAN.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-shared-platform-bobnet-removal-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-shared-platform-bobnet-removal-final-decommission-report.md`

Existing earlier shared-platform changes in the same website tree remain present, including `README.md`, `register\index.html`, `assets\js\twb-platform-client.js`, `TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`, `assets\images\starter-pets\`, `migrations\0014_account_creation_starter_pets.sql`, and `migrations\0015_garden_transfer_exports.sql`.

## Important decisions or discoveries
- Durable fact: Bob/BobNet package-hub routes and helper functions have been removed from `worker.js`.
- Durable fact: Fresh database rebuilds no longer create Bob forum seed categories or Bob package tables.
- Durable fact: Existing databases require `0016_remove_retired_package_hub.sql` to remove old Bob tables and rows.
- Warning: Cloudflare still has secret `BOB_FORGE_ADMIN_PASSWORD`; it was intentionally not deleted without explicit live secret-change approval.
- Warning: Remote D1 still has pending migrations `0015_garden_transfer_exports.sql` and `0016_remove_retired_package_hub.sql`.

## Tests or checks run
- `node --check worker.js` - passed.
- `node --check assets\js\site.js` - passed.
- `node --check assets\js\account.js` - passed.
- `npx wrangler --version` - returned `4.81.1`.
- `npx wrangler deploy --dry-run` - passed; no deployment performed.
- `npx wrangler d1 migrations apply twb-core --local` - passed; applied `0016_remove_retired_package_hub.sql` locally.
- Local D1 checks confirmed no `bob%` tables, forum categories, or forum groups remain after local cleanup migration.
- `npx wrangler d1 migrations list twb-core --remote` - read-only check; remote pending migrations are `0015_garden_transfer_exports.sql` and `0016_remove_retired_package_hub.sql`.
- `npx wrangler secret list` - read-only check; `BOB_FORGE_ADMIN_PASSWORD` still exists.
- `rg` cleanup searches show only intentional cleanup migration references plus a normal English phrase `idle bob` in a creature article.
- Served Wrangler dev smoke was attempted but failed to complete cleanly within command timeouts.

## Cleanup performed
Deleted old Bob image assets and Bob package migration source files. Removed temporary Wrangler dev logs from `%TEMP%`. Stopped stray Wrangler dev/workerd processes created by the served smoke attempt. No screenshots or scratch files were intentionally left behind.

## Risks / warnings
- Do not assume production is clean until remote D1 migrations are applied and production is redeployed.
- Do not delete `BOB_FORGE_ADMIN_PASSWORD` without explicit approval; it is a live Cloudflare secret.
- The old migration files `0007`, `0008`, and `0009` were deleted from source. This is acceptable for fresh rebuild cleanup but the existing remote database migration history may still record those names.
- Wrangler dev smoke was inconclusive due to local process/timeouts, although syntax, dry-run, and local D1 checks passed.

## Blockers
- Approval needed to apply remote D1 migrations.
- Approval needed to delete the live `BOB_FORGE_ADMIN_PASSWORD` secret.
- Approval needed for live deploy after cleanup.
- Served preview needs a calmer retry if visual/browser confirmation is required.

## Memory-worthy notes
- Bob/BobNet package-hub source is removed from TWB website account/platform source.
- Existing database cleanup is represented by `0016_remove_retired_package_hub.sql`.
- Production cleanup gate should handle remote migrations, optional secret deletion, deployment, and live verification in a controlled order.

## Do not promote to memory
- Failed Wrangler dev smoke mechanics unless the issue recurs.
- Temporary `%TEMP%` log file names.
- Broad chat/task narration from the cleanup window.

## Next recommended gate
Run a narrow production-readiness worker task: review diff, retry served preview if desired, then prepare a gated live cleanup sequence for remote migrations `0015` and `0016`, optional `BOB_FORGE_ADMIN_PASSWORD` deletion, Worker deploy, and live verification of account/register/profile/forum routes.
