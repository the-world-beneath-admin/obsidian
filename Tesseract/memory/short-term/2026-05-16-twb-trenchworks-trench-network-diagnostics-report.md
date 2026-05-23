# TWB Trenchworks Trench Network Diagnostics Report

## Scope

Standalone Unity 2D TWB Trenchworks prototype under `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

This was step 5 of the current 8-step War Team Authority and Frontline Field Maps pass.

## What Changed

- Added trench-network validation counters to the visible `WarWorld` simulation.
- Added player/enemy network totals, supplied network totals, isolated network totals, supply-connected trench cell totals, unsupported trench cell totals, and contested trench cell totals.
- Added right-hand war tracker diagnostics so Play Mode can show whether trenches are becoming supplied networks or isolated pockets.
- Preserved the fully visible battlefield direction; no fog-of-war visuals were reintroduced.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`

## How To Run It In Unity Hub

1. Open Unity Hub.
2. Open project folder `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
3. Open scene `Assets\Scenes\TrenchworksPrototype.unity` if it is not already open.
4. Press Play.
5. In the right-hand War tracker, check:
   - `Networks: P supplied/total | E supplied/total`
   - `Unsupported cells: P / E | contested`

## Whether `prototype\My project` Was Involved

Not involved. The obsolete nested/default sample project under `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype\My project` was not touched.

## Tests / Checks Run

- Unity source compile through Unity 6000.3.8f1 Roslyn response files: passed.
- `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln`: passed with the known warning `Unable to find a project to restore`.

## Cleanup Performed

- No temporary files, screenshots, or scratch logs were created.

## Risks

- The diagnostics count active trench cells only. That matches current simulation bookkeeping, but if a future trench ever stops being an active cell, it would disappear from the counter.
- Network supply is still a binary connected/not-connected signal. It does not yet express weak supply, contested supply, or throughput.
- This is source-level verified, not live Play Mode visually verified in the open editor.

## Memory-Worthy Notes

- The visible war tracker now exposes whether trenches are connected and supplied, which should make the next trench-network behavior tests less guesswork-heavy.
- Current plan progress after this pass: 5 of 8 completed, 3 steps left.

## Follow-Up Recommendations

- Proceed to step 6: add field-map debug overlay/counters for tuning squad decisions.
- During live Play Mode review, watch whether unsupported player trench cells eventually trigger `ConnectSupply`, `Regroup`, or stabilized supplied-network behavior.

## Anything Blocked

- Nothing blocked in this pass.
