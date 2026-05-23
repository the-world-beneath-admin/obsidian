# TWB Unity Worker Report - 2026-05-13 - Run Tracker UI

## Task

Clean up the main-game world map Run Tracker window after the screenshot showed overlapping chrome, cramped header controls, and lower action content colliding with the frame.

## Result

The Run Tracker window was tightened into a simpler subwindow panel, with the header, Refresh/Back controls, column strip, visible run rows, and selected-run action box repositioned inside the frame. The visible list now uses fewer, taller rows so text and controls do not crowd the lower frame.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-unity-run-tracker-ui-worker-report.md`

## Checks run

- `git diff --check -- Assets/_TWB/Scripts/UnityBridge/UI/Builders/WorldMapSurfaceBuilder.cs`
- Unity response-file compiler invocation for `TWB.UnityBridge`
- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore`

## Cleanup performed

No temporary files or screenshots were created for this slice.

## Risks

This was a layout-only code pass. The open Unity editor was not driven manually during this slice, so visual confirmation should be done in Play Mode after reload.

## Memory-worthy notes

The Run Tracker should remain a compact utility window, but it needs a simpler chrome treatment than the full animated plate style used on larger world map panels.

## Do not promote to memory

Do not promote this report as a final design decision. Treat it as a short-term UI polish implementation note until Bob/orchestrator reviews the in-editor result.

## Next recommended gate

Reload the Unity UI, open the Run Tracker, and visually confirm that the header, three-row list, selected-run details, and action button sit inside the panel without overlap.
