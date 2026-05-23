# TWB Unity Worker Report - 2026-05-12 - Worldmap SystemConsole Decommission

## Task

Main game / The World Beneath. Clear the remaining 22 TWB SystemConsole failures after the Peggy and Stanly starter guardian cleanup. If failures belonged to decommissioned world-map systems, decommission the tests instead of restoring retired systems.

## Result

The remaining 22 failures were all stale world-map tests for retired map-pack, no-label, styled-raster, vector-tile, hosted-lane, render-prereq, and source-switch contracts. Those tests were removed from `WorldMapActivityTests.cs`, and their explicit registry entries were removed from `SystemConsoleTestRegistry.cs`.

The current C# solution build passes. A fresh full SystemConsole batch run could not start because the Unity editor already has `TWB_Phase1_IdlePrototype` open.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\WorldMapActivityTests.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\SystemConsoleTestRegistry.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-12-twb-unity-worldmap-systemconsole-decommission-worker-report.md`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` - passed, 0 warnings, 0 errors.
- `rg` sweep for the 22 retired world-map test class names and fail IDs under SystemConsole source folders - no matches.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` - reported failed because the editor log still contains stale pre-registry-cleanup compile errors.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-systemconsole` - blocked before test execution because another Unity instance has this project open. Latest run directory: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\artifacts\unity-automation\20260512-102623`.

## Cleanup performed

No throwaway scratch files were created. Automation logs were retained as verification evidence.

## Risks

Full SystemConsole verification is still pending until the open Unity editor is closed or the tests are run from inside the active editor. The source-level build and registry sweep are clean, but the full runner has not produced a post-decommission pass/fail count.

The Unity editor log status is polluted by stale compile errors from the short window after the obsolete test classes were removed and before their registry entries were cleaned.

## Memory-worthy notes

The removed failures guarded decommissioned world-map infrastructure rather than current ops-table world-map behavior. The living ops-table world-map checks from the earlier cleanup remained source-present; only stale no-label/styled/vector/render/tooling contracts were removed.

## Do not promote to memory

Do not promote the transient editor-log error count as a current failure state. It reflects stale log content, not the current `dotnet build` result.

## Next recommended gate

Close the active Unity editor instance for `TWB_Phase1_IdlePrototype`, then run:

`powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-systemconsole`

If that passes, follow with:

`powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile`
