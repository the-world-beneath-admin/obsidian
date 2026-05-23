# TWB Shared Platform Worker Report - 2026-05-13 - Garden Account Panel Removal

## Task

Remove the visible TWB account/account merger panel from Glassroot Garden for now. Leave account UI ownership for a later pass while avoiding source cleanup outside the requested surface.

## Result

Removed the in-game `TWB ACCOUNT` panel and its Link/Sync buttons from the Glassroot Garden canvas. The underlying shared-platform client and quiet export plumbing remain available for a future UI hook, but the player-facing Garden scene no longer displays the account attachment widget.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\dist\assets\index-*.js` refreshed by `npm run build`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\dist\index.html` refreshed by `npm run build`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-glassroot-garden-account-panel-removal-report.md`

## Checks run

- `npm run build` from `C:\Users\yrred\Desktop\Unity\TWB-Farming` passed.
- `rg` check confirmed the removed Garden scene no longer contains `TWB ACCOUNT`, `createPlatformPanel`, `platformStatusText`, `platformButtonText`, `platformLinkPoll`, `beginPlatformLink`, `pollPlatformLink`, or `createPlatformButton`.
- Playwright smoke check loaded `http://127.0.0.1:5173/`, confirmed the Phaser canvas was present, and confirmed the page text no longer includes `TWB ACCOUNT`.

## Cleanup performed

Removed the temporary Playwright screenshot:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\glassroot-account-panel-removed-smoke.png`

## Risks

Garden no longer exposes a player-facing way to link or sync an account from inside the canvas. Quiet platform export processing still depends on a token already being present in local storage, so future account UI needs to provide the explicit link/sync experience.

## Memory-worthy notes

The user wants the Garden account merger/account link surface removed from the current game UI and added later as a deliberate UI pass.

## Do not promote to memory

Do not record the removed panel as an accepted Garden UI direction. It was temporary scaffolding.

## Blockers

No blocker for the removal. Future platform attachment still needs a designed Garden UI entry point when the user is ready.

## Next recommended gate

Keep the shared-platform backend/client contract ready, then add Garden account linking through a purpose-built UI surface rather than the temporary top-right canvas panel.
