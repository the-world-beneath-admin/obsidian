# TWB Unity Worker Report - 2026-05-14 - Worldmap Hosted Streaming

## Task

Set up the completed world map tile pack for Cloudflare/R2 hosting and wire the main Unity world map so full zoom z8 tiles stream from the hosted source as needed, then persist to the player device cache.

## Result

Completed. The hosted pack is uploaded to the `twb-worldmap` R2 bucket under `worldmap/v1/styled/`.

Unity now prefers the persistent downloaded cache / hosted live URL for full zoom z8 hosted ops-table tiles, while keeping shipped local Resources tiles, ocean fallback, and parent-tile fallback available so the map does not blank while downloads are pending.

The hosted cache namespace was bumped to `twb_ops_table_hosted_v20260514` so old local downloads do not mask the refreshed hosted pack.

## Files touched

- `Assets/_TWB/Scripts/Domain/WorldMap/WorldMapTileSourceRegistry.cs`
- `Assets/_TWB/Scripts/UnityBridge/UI/Builders/WorldMapSurfaceBuilder.cs`
- `tools/worldmap/upload-worldmap-r2-direct.ps1`
- `memory/briefs/current-game-dev-task.md`
- `memory/short-term/2026-05-14-twb-unity-worldmap-hosted-streaming-worker-report.md`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed with 0 warnings and 0 errors.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` returned `probably-clean`, 0 error signals, 0 warning signals.
- R2 hosted upload completed with a fresh 2026-05-14 progress ledger:
  - `46220` hosted files prepared.
  - `0` files need upload on final dry-run.
- R2 URL spot checks returned HTTP 200, `image/png`, and `public, max-age=31536000, immutable` for sampled z5, z6, and z8 tiles.

## Cleanup performed

Removed the temporary shard PID file after upload completion.

Kept upload logs and the 2026-05-14 R2 progress ledger under `diagnostics/worldmap/` as deployment evidence. These are not source cleanup candidates until Bob/orchestrator decides whether to retain or archive them.

## Risks

High-concurrency R2 API uploads hit HTTP 429 and token-refresh contention during the bulk run. Final completion used lower-concurrency/single-process resume passes, and the final dry-run confirms the hosted pack is complete.

First-time z8 views may initially show the shipped local fallback while hosted tiles download. Once downloaded, tiles are saved under Unity persistent data and reused permanently unless the user explicitly clears downloaded map storage.

The public URL is still the existing R2 dev URL, not a custom production CDN domain.

## Memory-worthy notes

The full hosted ops-table pack is live at the existing default base URL:

`https://pub-068fc51d7ff04de49e919c3c795828d4.r2.dev/worldmap/v1/styled/{z}/{x}/{y}.png`

Hosted file count is `46220`: z5/z6/z8 tile PNGs plus hosted metadata files.

The Unity cache namespace for hosted ops-table downloads is now `twb_ops_table_hosted_v20260514`.

## Do not promote to memory

Do not promote the transient upload shard process details, failed high-concurrency attempts, PID file, or individual batch logs unless needed for deployment troubleshooting.

## Next recommended gate

Run a manual Unity smoke pass: open the world map, switch to full zoom/Area 220km, pan to an uncached z8 location, confirm hosted tiles download and persist, then toggle cached/offline map mode to confirm already-downloaded tiles still render.
