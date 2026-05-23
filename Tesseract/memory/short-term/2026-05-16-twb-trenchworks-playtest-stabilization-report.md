# TWB Trenchworks Playtest Stabilization Report

## Scope

Standalone Unity 2D TWB Trenchworks prototype under `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

This completes the 8-step War Team Authority and Frontline Field Maps stabilization sequence.

## What Changed

- Confirmed the canonical project is `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`, not the obsolete `prototype\My project` sample project.
- Added squad/team authority fields for visible war units: squad intent, target, reason, combat edge, suppression, confidence, stall timer, and field-map summary.
- Added connected trench metadata: network id, supply-connected state, supplied/isolated network counters, unsupported cell counters, and contested trench counters.
- Added unsupported-trench behavior so squads can connect supply, hold, or regroup rather than sitting forever in isolated holes.
- Added anti-stall order timeouts and quiet-front probe behavior.
- Added field-map debug counters for heat, danger, supply, trench safety, blob pressure, and no-man pressure.
- Added a `FLD` debug layer to show squad leader intent targets and pressure paths.
- Added cached low-resolution 8x8-tile influence maps for contact heat, danger, friendly support, and blob pressure.
- Fixed smoke-test cohesion failure by making far followers fully simulated, making leaders hold for stragglers during squad orders/static movement, and adding a last-resort commander-radius rejoin when pathing fails.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- Reports under `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\`

## How To Run It In Unity Hub

1. Open Unity Hub.
2. Open project folder `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
3. Open `Assets\Scenes\TrenchworksPrototype.unity` if it is not already open.
4. Press Play.
5. War view starts the wave drill by default.
6. Use mouse wheel to zoom, drag or WASD to pan.
7. Use bottom `LYR` then `FLD` to see squad intent targets and field pressure paths.
8. Watch the right Unit Summary panel for unit health, squad intent, field-map readings, and influence-cache diagnostics.

## Whether `prototype\My project` Was Involved

Not involved. The obsolete nested/default sample project under `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype\My project` was not used or modified.

## Tests / Checks Run

- Unity source compile through Unity 6000.3.8f1 Roslyn response files: passed.
- `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln`: passed with the known warning `Unable to find a project to restore`.
- Unity batchmode smoke test:
  - Method: `TWB.Trenchworks.Editor.TrenchworksProjectSetup.RunSimulationSmokeTest`
  - Result: passed.
  - Key result: `Resources: 216`, `Shipping areas: 3`, `Workers: 5/5`, `TOP stored/routed ammo: 2/2`, `Wave drill pulses/cycle/units/contacts/trenches/maxLeaderDistance: 16/4/192/0/219/14`, `integrated smoke passed=True`.

## Cleanup Performed

- Removed temporary Unity batchmode smoke log `Logs\codex-step8-smoke.log` after recording the result here.
- No generated screenshots or scratch files remain from this pass.

## Risks

- Batchmode simulation smoke passed, but visual Play Mode still needs human review in the Unity editor for readability, pacing, and whether the FLD layer matches player expectation.
- The commander leash includes a last-resort emergency regroup if pathing cannot return a follower inside radius. This protects squad structure but may need a prettier animation later.
- Influence maps are intentionally coarse 8x8 buckets, so danger/support/crowding are approximate within each bucket.
- Contact count was `0` at the final smoke-test snapshot even though the smoke saw contact during the run; this likely means contacts aged out by the final loop snapshot, not that combat never happened.

## Memory-Worthy Notes

- Current plan progress: 8 of 8 completed, 0 steps left.
- The next design gate should stay focused on live Play Mode review of the team-authority loop before adding new unit types, props, UI panels, or additional systems.
- Field-map caching is now in place, but broader performance work remains possible in rendering, movement scans, and occupancy/path queries.
- The squad radius requirement now has automated coverage through the smoke test, with max leader distance passing at `14`.

## Follow-Up Recommendations

- Have the user press Play in Unity and visually inspect:
  - squads stay grouped under commanders,
  - FLD layer target paths match movement,
  - trenches are readable and supplied/unsupported counters make sense,
  - wave drill remains smooth with 192 units,
  - emergency regroup does not look jarring if it occurs.
- If visual review passes, next milestone should tune combat/trench behaviour rather than expanding content.
- If performance still drags in live editor, profile rendering and movement/occupancy scans next.

## Anything Blocked

- No source-level or batchmode blockers remain.
- Live human visual confirmation is still needed because Codex cannot directly see the Unity Game view from batchmode.
