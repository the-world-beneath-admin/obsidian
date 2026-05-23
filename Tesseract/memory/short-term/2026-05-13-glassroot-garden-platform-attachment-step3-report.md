# TWB Shared Platform Worker Report - 2026-05-13 - Step 3 Garden Platform Attachment

## Task

Proceed with the next hook-in step: connect Glassroot Garden to the shared platform for account linking, read-only account pet state, and server-allowlisted transfer-bundle exports.

Scope: Glassroot Garden World Key plus shared platform client integration. Website source from Step 2 was not deployed in this pass.

## Result

Implemented a narrow Garden-side platform attachment:

- Added a Garden platform client module with TWB account device-link support.
- Added a small in-game account panel with `Link` and `Sync` buttons.
- Garden can start the website device-link flow, poll for approval, store the bearer token locally, and read `/api/platform/state`.
- Account companion cards are summarized in the Garden UI as shared pets once synced.
- Transfer bundles now create pending platform export records when they resolve.
- Pending exports are saved in the Garden local save and retried after account sync/link.
- Export calls use the Step 2 server-allowlisted endpoint, not generic inventory events.

Garden local crop/plot/drying/bundling state remains local.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\platform\twbPlatformClient.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\dist\` was refreshed by `npm run build`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-glassroot-garden-platform-attachment-step3-report.md`

## Checks run

- `npm run build`
- Started/confirmed local dev server at `http://127.0.0.1:5173/`
- Playwright smoke loaded the page, found the canvas, captured a screenshot, and verified the new TWB account panel was visible.

Build passed. Vite still reports the known large chunk warning for the Phaser bundle.

## Cleanup performed

- Removed the temporary Playwright screenshot `output/playwright/glassroot-platform-link-smoke.png`.
- Left the dev server running on `127.0.0.1:5173` for user testing.
- Left `dist/` in place because the project already uses it as build output and `npm run build` refreshed it.

## Risks

- The Garden export endpoint and catalog migration from Step 2 are still local website source only unless deployed separately.
- A linked Garden running against live `https://the-world-beneath.com` will need the Step 2 Worker deploy and remote migration before transfer export calls succeed.
- This pass reads shared pets and displays them, but Garden companion gameplay still uses the existing local companion models. Full account-pet projection and companion picker are still future work.
- Pending export records rely on local save persistence until a fuller server-side Garden action/save authority exists.

## Memory-worthy notes

- Garden now has the first browser World Key account-link path.
- Garden transfer bundles are queued locally and exported only through a game-specific endpoint.
- Shared pets are visible as synced account companion-card names but not yet gameplay-driving Garden companions.

## Do not promote to memory

- Do not promote this as live production integration yet.
- Do not promote transfer exports as full proof of legitimate in-game completion; they are queued client-side requests to a server allowlist.

## Blockers

- Deploy Step 1/2 website Worker changes and apply migration `0015_garden_transfer_exports.sql` remotely before live Garden export testing.
- Implement full Garden account-pet projection/picker.
- Add linked-client list/revoke UI on the website.
- Add server-side Garden completion proof if exports need stronger anti-cheat authority.

## Next recommended gate

Deploy the website shared-platform changes when approved, then test the full loop:

1. Create/link a website account.
2. Open Garden.
3. Approve device link.
4. Sync account state and confirm starter pets appear.
5. Complete a transfer bundle.
6. Confirm the Garden export row appears in platform inventory.
