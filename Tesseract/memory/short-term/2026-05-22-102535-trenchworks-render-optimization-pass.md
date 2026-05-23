# TWB Trenchworks Render Optimization Pass

Date: 2026-05-22
Worker: TWB Trenchworks standing worker
Scope: TWB Trenchworks standalone Unity project only.

## What Changed

- Investigated the post-trench-build drag in the new art/rendering system with child subagent `019e5045-28ec-7b43-90a2-3193472fe6c7`.
- Confirmed the primary drag source is the war `OnGUI` trench renderer rebuilding and drawing merged integrated blueprint trench art too aggressively after trench networks exist.
- Reused merged blueprint trench render dictionaries instead of allocating fresh dictionaries every repaint.
- Culled off-screen integrated blueprint pieces before expanding centerline cells into the 3x3 trench footprint.
- Added a maximum merged blueprint cell draw budget per frame.
- Added low-detail merged trench rendering below close zoom so distant trenches use cheap fills instead of multi-pass composite texture art.
- Changed wide-bottom trench atlas mask caches to be keyed by atlas path, preventing cache thrash when mixed trench tiers are visible.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-102535-trenchworks-render-optimization-pass.md`

## Tests And Checks Run

- `dotnet build "TWB-TrenchWorks.sln" --no-restore` from `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`
  - Result: passed, 0 warnings, 0 errors.
- Unity batch smoke command attempted:
  - `Unity.exe -batchmode -quit -projectPath ... -executeMethod TWB.Trenchworks.Editor.TrenchworksProjectSetup.RunSimulationSmokeTest`
  - Result: blocked because another Unity instance already has this project open.

## Cleanup Performed

- Closed child subagent after reviewing its read-only findings.
- Deleted the 2-minute heartbeat automation `twb-trenchworks-optimization-heartbeat`.
- No raw GPT Pro/Obsidian package files were modified.
- No permanent Obsidian memory files were modified.

## Risks

- This is a targeted code-level optimization, not a measured profiler run. The next best check is to play the current Unity scene and compare drag before/after after a trench network is built.
- Low-detail trench art now applies below `warCamera.CellSize < 3.25f`; if that threshold feels too aggressive visually, adjust it downward.
- The legacy trench network draw and integrated merged blueprint art may still both contribute work in some views. The next optimization pass should decide which layer owns completed trenches at each zoom level.

## Memory-Worthy Notes

- The expensive path is `DrawMergedIntegratedBlueprintTrenchArt` / `BuildIntegratedBlueprintTrenchRenderCells` in `PrototypeBootstrap.cs`.
- The previous renderer rebuilt merged trench render dictionaries every repaint, expanded each centerline trench cell into a 3x3 footprint, checked eight neighbours per rendered cell, and drew composite trench textures even when zoomed out.
- Wide-bottom trench atlas caches were effectively single-style caches. Mixed tier trench visibility could cause cache clearing and repeated atlas slicing.

## Follow-Up Recommendations

- Run an in-editor profiler capture after a completed trench network exists and compare `TWB.Trenchworks.WarMapDraw` before/after.
- Cache merged trench cells by a war blueprint visibility/version value if the simulation exposes one later.
- Reuse the battlefield snapshot across war map and right panel repaint paths.
- Replace remaining hot-path LINQ allocations in war `OnGUI`, especially the debug `Where/Take`, contact `Take`, and right-panel summary sorts if profiler data still shows UI drag.
