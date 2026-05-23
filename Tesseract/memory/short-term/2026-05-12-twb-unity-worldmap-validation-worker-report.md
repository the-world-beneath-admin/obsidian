# TWB Unity Worker Report - 2026-05-12 - Worldmap Validation

## Task

Run a conservative validation/smoke pass for the main The World Beneath Unity project after the Peggy and Stanly starter guardian fixes. Confirm build health, Unity reload/status, Peggy/Stanly validation, and world map smoke readiness before any further visual, route/lane, HoloGlyph, starter expansion, or cleanup work.

Scope: Main game / The World Beneath.

## Result

Completed with one narrow smoke-blocker fix.

The required `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed before any fix. A focused world-map smoke test then failed because the starter map generated no dungeon nodes. Root cause: `WorldMapConfig.MinDungeonTraceMapZoomLevel` was `12`, but `WorldMapService.ClampZoom` currently collapses supported zooms to `5`, `6`, or `8`, which made dungeon trace generation impossible in normal town-map mode.

Changed the minimum dungeon trace zoom to `8`, matching the current town-map close mode. After that, the world map Stage 1 acceptance smoke passed and generated dungeon nodes route into runnable dungeon families.

Peggy and Stanly starter guardian validation passed before and after the change.

Unity batch compile ran, but the automation summary still reports failure from two Mono shutdown lines:

- `abort_threads: Failed aborting id: 0000000000001524, mono_thread_manage will ignore it`
- `abort_threads: Failed aborting id: 0000000000005D80, mono_thread_manage will ignore it`

Unity itself exited `0`, and no C# compile errors, Peggy/Stanly validation exceptions, or world-map runtime smoke failures remained in the focused passing checks.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Config\WorldMapConfig.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-12-twb-unity-worldmap-validation-worker-report.md`

Note: `WorldMapConfig.cs` is currently untracked in the dirty Unity worktree, so Bob/orchestrator should review ownership before any staging or commit pass.

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore`
  - Before fix: passed, 0 warnings, 0 errors.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile`
  - Before fix: Unity exit code 0, automation summary marked failed only because of the two `abort_threads` lines.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status -TailLines 300`
  - Marked failed only because the same two `abort_threads` lines were present in the editor log tail.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-systemconsole -TestFilter ephemrial_spirit`
  - Before fix: passed, 2/2.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-systemconsole -TestFilter world_map_stage1_acceptance_smoke`
  - Before fix: failed with `Expected generated dungeon nodes.`
- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore`
  - After fix: passed, 4 warnings, 0 errors.
  - Warnings were existing/non-blocking: one unreachable-code warning in `InMemoryGameCOnfigProvider.cs`, two unassigned `UIShellBootstrap` field warnings, and one unassigned `WorldMapVisualStackStats.FoldedContributorGlyphs` warning.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile`
  - After fix: Unity exit code 0, automation summary marked failed only because of the same two `abort_threads` lines.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-systemconsole -TestFilter ephemrial_spirit`
  - After fix: passed, 2/2.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-systemconsole -TestFilter world_map_stage1_acceptance_smoke`
  - After fix: passed, 1/1.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-systemconsole -TestFilter world_map_generated_nodes_runnable`
  - After fix: passed, 1/1.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-systemconsole -TestFilter world_map_travel_and_run_route`
  - After fix: passed, 1/1.

Optional adjacent checks also run:

- `world_map_dungeon_traces_close_zoom_only`
  - Failed after fix because the test still asserts starter `MapZoomLevel >= 12`, while current service close/town zoom is `8`.
- `world_map_ui_guardrails_contract`
  - Failed due an exact source-shape assertion missing `BuildWorldMapTownInfluenceFields(` in the expected order. This appears to be a source-contract/test-shape issue rather than the world-map open/runtime smoke blocker handled here.

## Cleanup performed

No scratch source files, screenshots, or temporary hand-authored files were created. Unity automation artifacts under `artifacts\unity-automation\` were retained as validation evidence.

No git staging, commit, revert, reset, or broad cleanup was performed.

## Risks

- Unity automation currently treats Mono `abort_threads` shutdown lines as error signals even when Unity exits `0`. This keeps compile/status summaries marked failed unless the parser or Unity shutdown issue is handled separately.
- `world_map_dungeon_traces_close_zoom_only` still has a stale zoom expectation (`>= 12`) that conflicts with the current 5/6/8 zoom table.
- `world_map_ui_guardrails_contract` still fails on a brittle exact source-order/source-shape assertion. It may need a separate test-hardening or UI-polish gate.
- The Unity worktree remains heavily dirty, and the touched `WorldMapConfig.cs` is untracked in git status.

## Memory-worthy notes

- WorldMapService currently clamps map zoom to three effective modes: world `5`, region `6`, and town/close `8`.
- Setting `WorldMapConfig.MinDungeonTraceMapZoomLevel` above `8` disables generated dungeon traces in the current zoom model.
- After setting `MinDungeonTraceMapZoomLevel` to `8`, the focused world-map acceptance smoke passes through starter home, map snapshot, generated dungeon node, travel, and dungeon backend handoff.
- Peggy remains clean as a Faith utility starter, and Stanly remains clean as a Might attack starter in the focused `ephemrial_spirit` SystemConsole slice.

## Do not promote to memory

- Do not promote the transient pre-fix `Expected generated dungeon nodes` failure except as background evidence for the corrected zoom threshold.
- Do not promote the Mono `abort_threads` lines as a gameplay validation failure without a separate automation/parser review.
- Do not promote the optional UI guardrail source-shape failure as final visual direction.

## Next recommended gate

Before route/lane or visual polish work, run a small test-maintenance gate:

- update or retire the stale `world_map_dungeon_traces_close_zoom_only` `MapZoomLevel >= 12` assertion so it follows `WorldMapService.TownMapModeZoomLevel`
- harden or update `world_map_ui_guardrails_contract` if that source-contract test is still desired
- then perform a manual Unity editor world-map visual open/reload check if Bob wants visual confirmation beyond the passing batch smoke path
