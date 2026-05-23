# TWB Unity Worker Report - 2026-05-13 - Node Dungeon Summary Scroll Controls

## Task

Main game / The World Beneath. Shorten the node dungeon summary card tabs and add a minimalist scrollbar with up/down buttons so the trace list can be navigated without a mouse wheel.

## Result

Shortened the dungeon trace rows and reserved a slim right-side rail for explicit scroll controls. The existing three-visible-row masked `ScrollRect` remains, with a minimalist vertical scrollbar, handle, and `^` / `v` buttons that step through hidden rows.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-unity-node-dungeon-summary-scroll-controls-report.md`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` - passed with two existing CS0649 warnings.
- `git diff --check -- "Assets/_TWB/Scripts/UnityBridge/UI/Builders/WorldMapSurfaceBuilder.cs"` - passed.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile` - returned `probably-clean`, `UnityExitCode: 0`, `ErrorSignals: 0`; automation noted the editor project was already open and aborted batchmode.

## Cleanup performed

No temporary files were created by this pass.

## Risks

The visual fit should be checked in the open Unity editor because the automation could not open a second batchmode editor while the project was already open.

## Memory-worthy notes

Node dungeon summary rows now support explicit non-wheel scrolling through a slim in-panel control rail.

## Do not promote to memory

This is a small UI polish implementation detail unless the scrollbar pattern becomes a broader UI convention.

## Next recommended gate

Visually confirm the summary window at 3, 4, and 5+ folded dungeon traces, then continue only with focused UI polish or test-console fallout that appears from this surface.
