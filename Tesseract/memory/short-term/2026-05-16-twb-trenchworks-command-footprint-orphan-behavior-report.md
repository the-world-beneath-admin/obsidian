# TWB Trenchworks Command Footprint And Orphan Behavior Report

Date: 2026-05-16
Scope: TWB Trenchworks standalone Unity 2D prototype.

## What Changed

- Command units now use a 2-cell vertical footprint in simulation occupancy.
- Command units now render as taller 2-cell markers on the war map.
- Command unit map tags now read `C2` so they visually differ from one-square unit tags.
- Non-command units now detect when their assigned commander is dead or unavailable.
- Orphaned non-command units now:
  - seek the nearest living friendly command unit within command-search range;
  - attach to that replacement commander if they get close enough;
  - return to their base for recycling if they stay commanderless too long.
- Recycled soldiers are removed from the live field without being counted as combat casualties.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-command-footprint-orphan-behavior-report.md`

## Tests And Checks

- `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln`
  - Passed, but this Unity-generated solution still reports no standard project to restore, so it is a weak check.
- Unity editor log reviewed after script refresh.
  - Changed scripts compiled and assembly reload completed.
  - No `CS` compiler errors were found in the latest checked editor-log slice.

## Cleanup Performed

- No temporary files, screenshots, or scratch artifacts were created.

## Risks

- Two-cell command occupancy touches core movement/collision, so live Play Mode should confirm command units do not snag too often at obstacles or crowded spawn exits.
- Orphan recycling currently removes units when they return to base, but does not yet refund or create a formal manpower/resource pool.
- Command replacement is intentionally simple: nearest living friendly command unit, not a full platoon hierarchy.

## Memory-Worthy Notes

- Command units are now true battlefield anchors, not just a label on a normal square.
- The war simulation now has a first morale/command-structure failure behavior: units can lose command, seek command, or leave the front.
- Future unit AI should treat command footprint, command radius, and command loss as core squad behavior.

## Follow-Up Recommendations

- Live test by killing or isolating command units and watching whether soldiers enter `SeekingCommand` and `Recycling`.
- Add a small right-panel count for seeking/recycling units if this behavior needs easier visual review.
- Later, tie recycling into manpower, wounded recovery, or replacement squads rather than simply deleting the unit.

## Blocked

- No live Play Mode visual confirmation was performed in this pass.
