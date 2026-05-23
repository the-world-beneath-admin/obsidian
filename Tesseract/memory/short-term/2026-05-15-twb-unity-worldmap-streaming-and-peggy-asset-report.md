# TWB Unity Worker Report - 2026-05-15 - Worldmap Streaming and Peggy Asset Cleanup

## Task

Fix the world map full-zoom streaming path that appeared to show low-resolution fallback assets beyond the test set, and remove the invalid Peggy image from the game while preserving it on the Desktop.

## Result

Peggy's incorrect 1024 image was removed from Unity Resources and moved to the Desktop. Peggy's starter catalog entry now uses the valid `util-peggy` icon for both sprite and key art.

The world map renderer now holds hosted full-zoom tiles for live/cached R2 content instead of immediately painting local fallback sprites while the network request is pending. This should make true streaming state visible and prevent low-resolution shipped fallback tiles from masquerading as downloaded full-resolution tiles.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\StarterPets\StarterPetCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`
- Moved out of game: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\PetIcons\Special\EphemrialSpirit\special-ephemrial-spirit-peggy-1024.png`
- Moved to Desktop: `C:\Users\yrred\Desktop\special-ephemrial-spirit-peggy-1024.png`
- Moved to Desktop: `C:\Users\yrred\Desktop\special-ephemrial-spirit-peggy-1024.png.meta`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed with 0 errors and 3 existing warnings.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` reported failed due one Unity editor-log error signal.
- Editor-log signal was Unity Connect/project services HTTP 401, not a TWB compile/runtime exception.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile` could not run because another Unity instance had the project open. Unity exit code was 0, but the automation aborted before compile.
- Public R2 hosted tile spot-checks returned HTTP 200 for sampled `worldmap/v1/styled` z5/z8 URLs.

## Cleanup performed

No source cleanup beyond removing the invalid Peggy asset from Unity Resources. The Unity automation artifact from the blocked compile run was left in place as evidence of the open-editor blocker.

## Risks

If a hosted tile is missing or the network is unavailable, preferred hosted full-zoom tiles now show the loading/fallback tint rather than silently drawing local fallback art. That is intentional for diagnosis, but it may expose blank/loading areas until the tile arrives or the cache is populated.

The R2 dry-run upload progress markers appear stale: it reported many z8 files as needing upload, while sampled public URLs were reachable. This should be verified before any broad re-upload.

## Memory-worthy notes

The apparent low-resolution streaming issue was likely caused by renderer fallback order, not necessarily missing R2 objects: the renderer requested hosted tiles, then immediately used shipped fallback sprites when the hosted tile was not already cached.

## Do not promote to memory

Do not promote the Peggy 1024 image as a valid game asset. It was intentionally removed from the game and preserved only on the Desktop.

## Next recommended gate

With Unity open, reload the world map at full zoom and confirm uncached hosted tiles transition from loading/fallback tint to downloaded R2 tiles. If the downloaded tiles still look low-resolution after this change, the next issue is the source tile art or upload contents, not the runtime fallback path.
