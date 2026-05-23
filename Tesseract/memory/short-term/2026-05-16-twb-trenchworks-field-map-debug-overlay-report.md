# TWB Trenchworks Field Map Debug Overlay Report

## Scope

Standalone Unity 2D TWB Trenchworks prototype under `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

This was step 6 of the current 8-step War Team Authority and Frontline Field Maps pass.

## What Changed

- Added leader-sampled field-map debug counters to `WarWorld`.
- Field-map counters now average player and enemy squad-leader readings for contact heat, danger, supply reach, trench safety, blob penalty, and no-man pressure.
- Added the field-map values to the active war Unit Summary panel so they are visible during the current Play Mode war view.
- Added the same field-map values to the War tracker page for non-war tracker review.
- Added a `FLD` war layer button that draws squad leader target markers and leader-to-target pressure paths.
- Updated the map legend when `FLD` or `ALL` is active.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`

## How To Run It In Unity Hub

1. Open Unity Hub.
2. Open project folder `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
3. Open scene `Assets\Scenes\TrenchworksPrototype.unity` if needed.
4. Press Play.
5. In war view, watch the Unit Summary header for field-map averages.
6. Use the bottom `LYR` category, then `FLD`, to show squad intent targets and pressure paths on the map.

## Whether `prototype\My project` Was Involved

Not involved. The obsolete nested/default sample project under `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype\My project` was not touched.

## Tests / Checks Run

- Unity source compile through Unity 6000.3.8f1 Roslyn response files: passed.
- `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln`: passed with the known warning `Unable to find a project to restore`.

## Cleanup Performed

- No temporary files, screenshots, or scratch logs were created.

## Risks

- The field-map averages are sampled from squad leaders only. This is intentional for team-authority tuning, but it does not describe every individual soldier's local pressure.
- The `FLD` layer draws debug pressure paths, not final art.
- This is source-level verified, not live Play Mode visually verified in the open editor.

## Memory-Worthy Notes

- The active war screen now exposes what the squad-level AI thinks about battlefield pressure: heat, danger, supply, trench safety, blob pressure, and no-man pressure.
- Current plan progress after this pass: 6 of 8 completed, 2 steps left.

## Follow-Up Recommendations

- Proceed to step 7: performance pass for cached low-resolution influence maps.
- During live Play Mode review, compare the `FLD` target markers against visible squad movement to catch bad scoring or stalled orders.

## Anything Blocked

- Nothing blocked in this pass.
