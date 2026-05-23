# TWB Trenchworks Field Map Cache Performance Report

## Scope

Standalone Unity 2D TWB Trenchworks prototype under `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

This was step 7 of the current 8-step War Team Authority and Frontline Field Maps pass.

## What Changed

- Replaced repeated per-sample unit/contact scans in `SampleWarField()` with cached low-resolution influence maps.
- Added 8x8-tile influence buckets over the 800x600 war map, producing a 100x75 cache per faction.
- Rebuilds now happen once per strategic second and after immediate wave-drill spawning.
- Cached layers currently cover contact heat, danger, friendly support, and blob pressure.
- Precise per-cell cover, trench safety, and supply reach remain sampled directly from the cell so trench/supply behavior stays responsive.
- Added visible cache diagnostics to the active Unit Summary and War tracker panels.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`

## How To Run It In Unity Hub

1. Open Unity Hub.
2. Open project folder `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
3. Open scene `Assets\Scenes\TrenchworksPrototype.unity` if needed.
4. Press Play.
5. In war view, watch the Unit Summary header for:
   - influence cache size
   - rebuild count
   - field-map heat/danger/supply/trench/no-man readings

## Whether `prototype\My project` Was Involved

Not involved. The obsolete nested/default sample project under `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype\My project` was not touched.

## Tests / Checks Run

- Unity source compile through Unity 6000.3.8f1 Roslyn response files: passed.
- `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln`: passed with the known warning `Unable to find a project to restore`.

## Cleanup Performed

- No temporary files, screenshots, or scratch logs were created.

## Risks

- The dynamic field-map values are now bucketed, so danger/support/crowding are intentionally approximate inside each 8x8 tile region.
- The cache reduces repeated sampling cost but does not yet optimize every war-system hot path, such as individual movement scans, rendering, or local occupancy checks.
- This is source-level verified, not live Play Mode visually verified in the open editor.

## Memory-Worthy Notes

- Field-map influence now follows the recommended structure: broad battlefield pressure is shared and cached, while individual unit logic remains simpler.
- Current plan progress after this pass: 7 of 8 completed, 1 step left.

## Follow-Up Recommendations

- Proceed to step 8: live Play Mode verification and final report refresh.
- During live review, compare cache diagnostics and `FLD` layer target paths against visible squad behavior to confirm the approximation still feels tactically sensible.

## Anything Blocked

- Nothing blocked in this pass.
