# TWB Shared Platform Worker Report - 2026-05-13 - Hook Readiness Audit

## Task

Audit whether the website-owned account, database, and client wiring are ready for the main game and World Keys to hook into the shared account/inventory platform.

## Result

The starter-pet account foundation is live and functional enough for website-created accounts: live `/api/platform/starter-pets` returns six starters with two ATK, two DEF, and two UTIL options, and unauthenticated `/api/platform/state` correctly returns `401`.

The hook-in foundation is not fully ready yet. Local website code contains the Garden transfer export endpoint and catalog migration, but production does not. Remote D1 still has `0015_garden_transfer_exports.sql` pending, live `/api/platform/manifest` reports zero `the-garden` catalog rows, and live `POST /api/platform/world-keys/garden/transfer-bundles/export` returns `404`.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-shared-platform-hook-readiness-audit.md`

## Checks run

- Read memory: `hot.md`, `index.md`, and `wiki/game-dev/project-hierarchy.md`.
- Inspected website migrations `0010`, `0011`, `0012`, `0014`, and `0015`.
- Inspected Worker routes for auth, starter-pet registration, platform state, game-device link, Unity snapshot sync, generic inventory events, and Garden export.
- Inspected website `twb-platform-client.js`.
- Inspected Garden `src/platform/twbPlatformClient.ts`.
- Inspected Unity `TwbPlatformAccountLinkClient.cs` and Settings platform hooks.
- Checked Alchemy for real platform endpoint usage; only planning docs mention it.
- `npx wrangler --version` returned `4.81.1`.
- `npx wrangler d1 migrations list twb-core --local` reported no pending local migrations.
- `npx wrangler d1 migrations list twb-core --remote` reported pending `0015_garden_transfer_exports.sql`.
- `npx wrangler deploy --dry-run` passed and read `2630` assets.
- Live `/api/platform/manifest` returned `schemaVersion: 1`, six starter pets, zero Garden catalog rows, and no Garden export endpoint in the manifest.
- Live `/api/platform/starter-pets` returned `ATK:2`, `DEF:2`, `UTIL:2`, and `accountLocked: true`.
- Live `/api/platform/state` without login returned `401`.
- Live Garden export POST returned `404`.
- `npx wrangler secret list` confirmed `ADMIN_BOOTSTRAP_CODE` exists, but its value remains unreadable as expected.

## Cleanup performed

No temporary files were created.

## Risks

- Local website source is ahead of live production for the Garden export endpoint and migration.
- Garden currently has hidden/quiet platform client plumbing but no approved player-facing account UI after the temporary panel was removed.
- Alchemy remains local/prototype-only for shared inventory.
- Main Unity has account-link and platform mirror plumbing, but it still needs a narrow integration pass against the live account contract and current game ID decisions.
- Leftover Bob/BobNet package routes, styles, forum categories, migrations, and secrets still exist in the website codebase/database lineage and should be deliberately removed or isolated before calling the platform clean.

## Memory-worthy notes

Production is ready for website account creation with starter pets, but not ready for World Key export hook-in until the local Garden export Worker code is deployed and migration `0015` is applied remotely.

## Do not promote to memory

Do not treat the Garden export route as live yet. The local code exists, but the live site currently returns `404`.

## Blockers

- Apply remote D1 migration `0015_garden_transfer_exports.sql`.
- Deploy the local Worker code that exposes `/api/platform/world-keys/garden/transfer-bundles/export`.
- Decide whether to remove or quarantine Bob/BobNet tables, routes, and UI before broader platform hookup.
- Add game-specific export authority for Alchemy and any main-game exported materials.
- Add shared companion projection/lock contracts per game surface.

## Next recommended gate

Run a production hook-in gate: apply remote migration `0015`, deploy the local Worker, verify the live manifest exposes the Garden export endpoint and Garden catalog rows, then perform an authenticated test export with a throwaway player account before wiring game UI around it.
