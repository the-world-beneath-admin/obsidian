# TWB Trenchworks Visual LOD Rendering Report

Date: 2026-05-16
Worker: Bob / Codex
Scope: TWB Trenchworks standalone Unity prototype.

## What Changed

- Added war-map visual LOD thresholds in `PrototypeBootstrap`.
- War grid lines now draw at coarser intervals and lower opacity when zoomed out.
- War-unit rendering now aggregates squads into one representative marker below the strategic zoom threshold.
- Aggregated squad markers draw an alive-member count badge above the marker.
- Enemy squad counts only include members currently visible through player fog of war.
- Integrated war-team overlay now uses the same aggregate-at-distance behavior so it does not leave a second swarm of individual member squares behind.
- Updated the in-map hint text to call out that zooming out groups squads.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-visual-lod-rendering-report.md`

## How To Run It In Unity Hub

1. Open `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks` in Unity Hub.
2. Open `Assets\Scenes\TrenchworksPrototype.unity` if Unity does not load it automatically.
3. Press Play.
4. Use mouse wheel to zoom the war map. At far zoom, squads should collapse into leader-style markers with count badges; at closer zoom, individual units return.

## Research Notes

- Unity's LOD guidance supports reducing rendered detail when objects occupy less screen space: https://docs.unity3d.com/Manual/class-LODGroup.html
- Unity's draw-call guidance supports reducing the number of things submitted for rendering when there are many objects: https://docs.unity3d.com/Manual/optimizing-draw-calls.html
- This prototype is IMGUI-based; Unity notes that `OnGUI()` is called every frame, so reducing per-frame GUI rectangles and labels is directly useful here: https://docs.unity3d.com/Manual/gui-Basics.html

## Tests And Checks Run

- `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln`
  - Passed, but the Unity-generated solution currently has no projects to restore/build, so this is only a weak check.
- Source-level C# compile against Unity 6000.3.8f1 UnityEngine modules and non-editor scripts.
  - Passed.
- Live Unity editor script compile from `Editor.log`.
  - Passed: `Tundra build success`, Assembly-CSharp and Assembly-CSharp-Editor rebuilt.

## Cleanup Performed

- Removed temporary source-check response and output files from `%TEMP%`.
- No source, asset, or user files were deleted.

## Risks

- This is still IMGUI drawing, so it reduces immediate draw volume but does not replace the renderer with a proper tile/mesh batching system.
- Aggregated markers may still visually overlap in dense spawn areas; that is better than individual-unit clutter, but not final UI polish.
- The integrated team overlay and legacy war-unit overlay are both still present. They are now aggregated at far zoom, but the longer-term clean fix may be choosing one canonical combat rendering layer.

## Memory-Worthy Notes

- Keep simulation and rendering LOD separate: full simulation may continue while far-zoom rendering collapses grid detail and unit detail.
- For fog fairness, enemy squad count badges should not reveal hidden enemy members.
- At strategic zoom, the user wants to read squads/teams, not individual soldiers.

## Follow-Up Recommendations

- Add a proper render mode toggle or debug overlay showing current visual LOD level, draw counts, active simulation units, and static fog units.
- Consider a future non-IMGUI map renderer for the war field if the prototype keeps scaling.
- Decide whether the legacy `WarUnit` layer or integrated `WarTeam` layer should become the canonical frontline display.

## Anything Blocked

- No blocker for this pass.
- Unity batchmode automation is not present in this live Trenchworks folder, and the editor is already open, but the live editor compile succeeded.
