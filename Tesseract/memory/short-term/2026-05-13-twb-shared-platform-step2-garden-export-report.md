# TWB Shared Platform Worker Report - 2026-05-13 - Step 2 Garden Export Endpoint

## Task

Proceed with the next blocker burn-down step for hooking the main game and World Keys into the cloud-based account/inventory platform.

Scope: shared platform/account systems. Step 2 was the Glassroot Garden server-side export gate for transfer bundles.

## Result

Implemented a local website Worker endpoint for Glassroot Garden transfer-bundle exports:

```text
POST /api/platform/world-keys/garden/transfer-bundles/export
```

The endpoint requires website/session or linked-game bearer authentication. It accepts an allowlisted Garden `recipeId` and a stable `bundleId` or `sourceEventId`, then the Worker calculates the shared inventory output. Client-provided item IDs and quantities are ignored.

Exports write:

- `sourceGameId`: `the-garden`
- `eventType`: `GARDEN_TRANSFER_BUNDLE_EXPORTED`
- one account-bound shared bundle item
- idempotent ledger row through the existing platform inventory ledger path

Also added catalog migration rows for all 20 current Garden transfer bundle outputs.

## Files touched

- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\worker.js`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\assets\js\twb-platform-client.js`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\migrations\0015_garden_transfer_exports.sql`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\SHARED_GAME_PLATFORM_PLAN.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-shared-platform-step2-garden-export-report.md`

## Checks run

- `git diff --check -- worker.js assets\js\twb-platform-client.js TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md SHARED_GAME_PLATFORM_PLAN.md migrations\0015_garden_transfer_exports.sql`
- `npx wrangler deploy --dry-run`
- `npx wrangler d1 migrations apply twb-core --local`
- `npx wrangler d1 execute twb-core --local --command "SELECT COUNT(*) AS garden_bundle_rows FROM platform_catalog WHERE source_game_id = 'the-garden' AND catalog_id LIKE 'garden_bundle_%';"`

Results:

- Worker dry-run passed.
- Local migration applied successfully.
- Local catalog check returned `garden_bundle_rows = 20`.
- No remote migration or live deploy was run.

## Cleanup performed

No temporary files were created. Local D1 migration state was updated as part of the requested local validation.

## Risks

- This endpoint is safer than generic inventory events because output is server-allowlisted, but it still does not prove the Garden bundle was legitimately completed. A future Garden authority step should validate against cloud save/action state.
- Garden browser source is not yet wired to call the endpoint.
- Remote D1 has not received migration `0015_garden_transfer_exports.sql` until a later approved remote migration.
- Live Worker does not include the new endpoint until a later approved deploy.

## Memory-worthy notes

- Garden transfer recipes export one shared bundle per non-compost crop.
- Current exported bundle catalog contains 20 account-bound rows, one for each Garden non-compost crop.
- The shared platform should prefer game-specific export endpoints over public generic inventory events.

## Do not promote to memory

- Do not promote this as live; it is local source plus local D1 only.
- Do not promote this as full Garden game-state authority; it is an allowlisted export gate.

## Blockers

- Wire Glassroot Garden to authenticate with the platform and call this export endpoint when transfer bundles resolve.
- Add completion proof/server-side Garden action validation.
- Add linked-client list/revoke UI.
- Define Alchemy and main-game export contracts.
- Continue BobNet/Bob package source cleanup separately.

## Next recommended gate

Step 3 should connect Glassroot Garden read-only account state and transfer exports:

- add platform client usage to Garden
- link/read account pets and starter companion cards
- call the Garden export endpoint when a transfer bundle resolves
- keep Garden crops, plots, drying, bundling, and unfinished processing in Garden-local save state
