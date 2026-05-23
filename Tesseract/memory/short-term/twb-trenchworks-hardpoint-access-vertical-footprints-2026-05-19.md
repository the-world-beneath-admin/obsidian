# TWB Trenchworks Hardpoint Access Vertical Footprints

Scope: TWB Trenchworks only.

## What Changed

- Fixed hardpoint access route piece selection so vertical hardpoint access trunks use the vertical utility-line pattern instead of stamping horizontal utility pieces.
- Exposed/used `tw_utility_line_vertical` through `WarFrontBlueprintPatternIds.UtilityLineVertical`.
- Confirmed the vertical utility pattern is present in the Gate 1 trench blueprint pattern catalog and required validation list.
- Strengthened the hardpoint access smoke check so the terminal access footprint must touch the owning hardpoint pad mouth/edge footprint, not merely sit near the pad anchor.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarFrontPlan.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTrenchBlueprintPatterns.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarPhaseOneFrontBlueprintSmoke.cs`

## Tests And Checks

- `dotnet build TWB-TrenchWorks.sln --no-restore` passed with 0 warnings and 0 errors.
- Unity batchmode smoke was attempted by the child subagent, but Unity refused because the project was already open in another Unity instance.

## Cleanup

- Child subagent was closed after completion.
- Temporary smoke log from the blocked Unity attempt was removed by the child.
- No permanent Obsidian memory was updated.

## Risks

- Live Unity Play Mode + F9 visual verification is still required.
- The expected visual result is that hardpoint access trunks now appear as vertical trench pieces and terminate into the pad edge/mouth instead of lying beside the pad as horizontal bars.

## Follow-Up Recommendation

Use Play Mode with `F5`, `F6`, or `F7` to regenerate a fresh biome map, toggle `F9`, and inspect several hardpoints across both factions. The access trunks should now visually line up as vertical paths into the hardpoint pads.
