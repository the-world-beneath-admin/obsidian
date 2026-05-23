# TWB Trenchworks Fog Of War Removal Report

Date: 2026-05-16
Scope: TWB Trenchworks standalone Unity 2D prototype.

## What Changed

- Removed the visible fog-of-war presentation from the war map.
- War map background now draws as no-man's-land instead of an unseen fog layer.
- Removed remembered/scouted ground drawing and its coarse far-zoom fog renderer.
- Enemy units, enemy integrated teams, contacts, trench plans, terrain, and trenches are no longer hidden by player visibility.
- Fog tinting functions now return original colors, so terrain and contact colors are not dimmed by fog.
- Wave-drill status text now says the full field is visible instead of showing sight/known-cell counts.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-fog-of-war-removal-report.md`

## Tests And Checks

- `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln`
  - Passed, but this is still a weak check because Unity's generated solution reports no standard project to restore.
- Checked the Unity editor log tail for compiler errors after changes.
  - No current `CS` compiler errors were found in the checked tail.

## Cleanup Performed

- Removed unused fog color constants and dead remembered-ground rendering methods from `PrototypeBootstrap.cs`.
- No temporary files or screenshots were created.

## Risks

- The simulation still maintains player scouted/visible bookkeeping internally because scouting state is also used by current movement scoring. This pass removes the visible fog, not every internal scouting variable.
- With the full battlefield visible, map rendering may show more units and overlays at once. The next optimization pass should focus on spatial indexing, UI-summary caching, and replacing IMGUI map rendering with a more scalable draw path.

## Memory-Worthy Notes

- Current direction: no fog-of-war visuals for the Trenchworks wave-drill prototype.
- Future optimization should not rely on hiding battlefield information behind fog.
- The preferred optimization path is simulation/render structure: spatial buckets, visual interpolation, cached UI grouping, and non-IMGUI battlefield rendering.

## Follow-Up Recommendations

- Live Play Mode review to confirm the battlefield is fully visible and more readable.
- Start the next performance pass with `WarSpatialIndex` and cached unit-summary/squad rendering.
- Consider a simple LOD renderer that groups far-zoom squads without hiding them.

## Blocked

- No live Play Mode visual confirmation was performed in this pass.
