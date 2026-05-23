# TWB Unity Worker Report - 2026-05-14 - Account Inventory Persistence Plan

## Task

Study the prepared online account and inventory system and produce a conservative implementation plan for hooking The World Beneath Unity client into persistence, account identity, shared companion inventory, and cloud save behavior.

Scope: Main game / The World Beneath, with shared platform/account integration.

## Result

Planning pass completed. No Unity source implementation was performed in this slice.

The prepared website platform already provides the main pieces Unity needs:

- Website account identity and sessions.
- Game-device link flow for Unity clients.
- Bearer token auth for linked game clients.
- Platform manifest, starter pet catalog, platform state, origin state, inventory events, and game save endpoints.
- Cloud game save slots via `/api/platform/game-saves/{gameId}/{saveKey}`.
- A Unity sync-snapshot endpoint that currently records local Unity profile/snapshot data without importing local inventory into shared platform inventory.

The Unity client already has prototype integration code:

- Device-link client and token storage.
- Platform state fetch and local mirror storage.
- Full local save upload/load through platform game saves.
- Account home origin application.
- A destructive inventory mirror importer that can overwrite local Will/material/card inventory from platform stacks.

Primary conclusion: persistence should land in guarded slices. The dangerous part is shared inventory adoption, not account linking. Unity local save data should remain authoritative for main-game materials/progress while the website platform owns account identity, starter selection, shared companion cards, companion locks, account origin, explicit export events, and cloud save slots.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-14-twb-unity-account-inventory-persistence-plan-report.md`

No Unity source files were changed during this planning pass.

## Checks run

Source/document inspection only:

- Read current memory/hot/index/project hierarchy.
- Read shared platform wiki pages.
- Read website platform docs, Worker contract notes, Wrangler config, migrations, platform client JS, and relevant Worker endpoint code.
- Read Unity account-link, save, inventory mirror, settings UI, persistence, and player data code.

No build or Unity compile was run because this was a planning/reconnaissance slice with no source implementation.

## Cleanup performed

No temporary files were created.

## Risks

- `TwbPlatformInventoryMirrorImporter.ApplyToPlayer` currently overwrites local soft currency, material inventory, and card inventory from platform mirror data. This conflicts with the documented boundary that main-game materials remain local unless explicitly exported through named platform events.
- The Unity settings UI currently exposes an `Adopt` action that can apply the destructive mirror importer. This should not be an automatic or casual player-facing action for the main game.
- Unity cloud save game id is currently `twb-idle-prototype`; a canonical main-game id such as `twb-main` should be introduced with compatibility handling for existing prototype saves.
- Current Unity snapshot event ids are tick-based. They are unique but not retry-idempotent for the same logical operation.
- The website `README.md` appears stale about `sync-snapshot` mirroring Will/items/companions; Worker code and contract docs indicate Unity snapshot inventory is ignored until explicit export.
- Platform game saves are stored as JSON blobs without visible revision/etag conflict handling. Silent auto-overwrite would be risky.

## Memory-worthy notes

- Website account creation/login should remain the root identity flow.
- Unity should attach through game-device link instead of creating its own account/login flow.
- Shared companions are account-level platform inventory and should be projected into Unity read-only first, then locked/released explicitly when assigned to runs.
- Main-game materials and progression should remain local to Unity until an explicit shared export/reward contract is designed.
- Cloud save is suitable for full Unity save backup/sync, but needs conflict guardrails before automatic load or overwrite behavior.

## Do not promote to memory

- Do not promote this whole report verbatim.
- Do not treat the slice plan as a final architecture decision until Bob/orchestrator reviews it.
- Do not promote stale/conflicting README wording without reconciling it against Worker code and contract docs.

## Next recommended gate

Start with a safety-first Unity implementation slice:

1. Treat platform inventory mirror as read-only in the main game.
2. Rename or gate UI actions so `sync-snapshot` is presented as profile/cloud snapshot sync, not shared inventory adoption.
3. Disable or dev-gate the destructive `Adopt` action until an explicit import/migration flow is designed.
4. Add/complete DTO parsing for platform starter selection and companion card state.
5. Add narrow tests for platform-state parsing and for preventing accidental local inventory overwrite.

After that, proceed to guarded cloud save save/load with local backup and conflict comparison before any automatic pull.
