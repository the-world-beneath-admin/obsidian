# TWB Shared Platform Worker Report - 2026-05-13 - Account Inventory Foundation

## Task

Remove remaining Bob/BobNet package-hub remnants from the website-owned shared platform/account source while preserving the current account creation, starter pet, game-link, Garden export, and shared inventory work.

## Result

Source-side Bob/BobNet cleanup is complete. The Worker no longer exposes Bob package, Bob catalog, Bob console-client, or admin Bob moderation routes. The account admin UI no longer loads Bob queues. Site routing/page hooks/tracking no longer know about Bob pages. Forum/community copy no longer advertises Bob Console. Bob CSS and image assets were removed. Fresh database rebuilds no longer create Bob forum seed categories or Bob package tables, and `0016_remove_retired_package_hub.sql` was added for existing databases.

No live deploy, remote D1 migration, or Cloudflare secret mutation was performed.

## Files touched

- Website source: `worker.js`, `assets/js/account.js`, `assets/js/site.js`, `assets/css/styles.css`, `admin/index.html`, `profile/index.html`, `community/index.html`, `community/forum/index.html`, `community/forum/board/index.html`, `community/forum/thread/index.html`, `login/index.html`
- Copy cleanup: `blog/2026/05/start-with-initiation-book-audiobook.html`, `blog/2026/05/ashmantle-mastiff-threshold-defender.html`, `blog/2026/05/glyphwake-spawn-magic-freshwater-family.html`, `SHARED_GAME_PLATFORM_PLAN.md`
- Config/asset cleanup: `assets/downloads/theme-kits/twb-ios-webclips.mobileconfig`, Bob-named images under `assets/images/`
- Migrations: edited `0001_twb_core.sql`, `0002_forum_core.sql`, `0006_forum_game_first_seed.sql`; deleted `0007_bob_hub_packages.sql`, `0008_bob_hub_review_votes.sql`, `0009_bob_hub_provenance.sql`; added `0016_remove_retired_package_hub.sql`

## Checks run

- `node --check worker.js`
- `node --check assets/js/site.js`
- `node --check assets/js/account.js`
- `npx wrangler --version` -> `4.81.1`
- `npx wrangler deploy --dry-run` -> passed
- `npx wrangler d1 migrations apply twb-core --local` -> applied `0016_remove_retired_package_hub.sql` locally
- Local D1 checks confirmed no `bob%` tables, forum categories, or forum groups remain after the cleanup migration.
- `npx wrangler d1 migrations list twb-core --remote` -> remote still has pending `0015_garden_transfer_exports.sql` and `0016_remove_retired_package_hub.sql`
- `npx wrangler secret list` -> `BOB_FORGE_ADMIN_PASSWORD` still exists remotely
- `rg` cleanup search leaves only the intentional cleanup migration plus a normal animation phrase, `idle bob`, in a creature article.

Served Wrangler dev smoke was attempted but did not complete cleanly within the command timeout. The spawned dev processes were stopped and temporary log files were removed.

## Cleanup performed

Deleted Bob image assets and old Bob package migration files from source. Removed temporary Wrangler dev logs from `%TEMP%`. Stopped the stray Wrangler dev/workerd processes created by the served smoke attempt.

## Risks

- The remote database is not cleaned until `0016_remove_retired_package_hub.sql` is applied remotely.
- The live Worker still has the old deployed code until a future deployment gate.
- Cloudflare secret `BOB_FORGE_ADMIN_PASSWORD` remains because deleting a live secret is a separate secret-change gate.
- Historical applied migration records may still show old Bob migration names in environments where they already ran; source and live tables can still be cleaned with `0016`.

## Memory-worthy notes

- Bob/BobNet package-hub source has been removed from the website Worker, admin UI, CSS, assets, and fresh migration path.
- Existing databases should use `0016_remove_retired_package_hub.sql` to drop retired Bob package tables and remove old Bob forum rows.
- Remote pending migrations before live cleanup: `0015_garden_transfer_exports.sql` and `0016_remove_retired_package_hub.sql`.
- Remote secret cleanup remains: `BOB_FORGE_ADMIN_PASSWORD`.

## Do not promote to memory

- Temporary Wrangler dev smoke failure details unless they recur.
- `%TEMP%` log file names from the failed smoke attempt.

## Blockers

- Remote D1 migration approval is needed before production database cleanup.
- Explicit Cloudflare secret deletion approval is needed before removing `BOB_FORGE_ADMIN_PASSWORD`.
- Live deployment approval is needed before production code stops serving old Bob/BobNet routes.

## Next recommended gate

Review this source cleanup, then if approved run the production gate in this order: deploy dry-run, remote D1 migration apply for `0015` and `0016`, delete the retired `BOB_FORGE_ADMIN_PASSWORD` secret if desired, deploy Worker, and verify live account/register/profile/forum routes.
