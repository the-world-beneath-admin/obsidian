# TWB Trenchworks Cover-Bound Scouting Report

Date: 2026-05-16

Scope: standalone TWB Trenchworks Unity 2D prototype at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

This pass did not touch the main TWB Unity project, Glassroot Garden, Alchemy Lab, marketing, shared-platform, or sprite-sheet lanes.

## What changed

- Diagnosed the visible straight-line problem after map props were added:
  - terrain was present;
  - cover/concealment had mechanical effects;
  - scout movement still scored raw forward motion too strongly.
- Added cover-bound scouting for squad leaders:
  - leaders choose a forward cover target;
  - they move toward that target instead of only scoring the next adjacent cell;
  - full cover is preferred;
  - closer half cover can win when it is a more practical bound;
  - after reaching cover, leaders pause briefly and then select the next forward cover target.
- Reduced straight-ahead scoring and added stronger lateral probe scoring.
- Added route lookahead so cover/concealment ahead influences the next step.
- Followers keep squad cohesion as before and follow the commander’s cover-bound movement.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-cover-bound-scouting-report.md`

## Tests/checks run

- Unity/Roslyn runtime source compile using the project `Assembly-CSharp.rsp`: passed.
- Unity/Roslyn editor source compile using `Assembly-CSharp-Editor.rsp` with the temporary runtime reference: passed.
- No-window deterministic cover-bound scouting smoke: passed.
  - `maxYDelta=88`
  - `coverPauses=7652`
  - `leadersInCover=13659`
  - `playerLeaderX=66.8`
  - `enemyLeaderX=940.9`
  - `pulses=12`

## Cleanup performed

- Removed temporary compile/smoke harness under `Temp\CodexCompileCheck`.
- Did not write to Obsidian wiki/index/hot/log.

## Risks

- The route is still local/scored movement, not a full pathfinder.
- Cover pauses may need visual tuning in Play Mode if squads look too cautious.
- The smoke proves lateral/cover use, but live aesthetics remain the deciding test.
- Long-term smooth movement still needs render interpolation between grid cells.

## Memory-worthy notes

- Fact - Squad leaders now scout by bounding from cover point to cover point.
- Fact - Full cover is preferred, but closer half cover can be selected when it is the better forward bound.
- Fact - Straight-line forward marching has been deliberately de-weighted for scouting.

## Follow-up recommendations

- Watch the live drill and decide whether the cover pause should be shorter or longer.
- Add debug visualization for the selected cover target if the movement remains hard to interpret.
- Later, replace local cover targeting with route planning once larger terrain and command objectives stabilize.

## Anything blocked

Full Unity batchmode/editor automation was not launched because the live Unity editor is already open on the project. Source-level runtime/editor compiles and deterministic cover-bound smoke passed.

## Addendum - Forward Pressure Rebalance

### What changed

- Rebalanced cover-bound scouting after live review showed squads lingering too close to the starting edge.
- Forward cover target search now looks farther ahead and prefers practical medium-range bounds instead of tiny nearby cover steps.
- Cover pauses are shorter:
  - full cover pauses briefly;
  - half cover no longer causes a stop.
- Squad leaders now only wait for followers when they are genuinely beyond the cohesion radius, not merely close to the edge of it.
- Wave-drill scout movement increased from 2 to 3 scouting steps per strategic second to restore forward pressure.

### Tests/checks run

- Unity/Roslyn runtime source compile using the project `Assembly-CSharp.rsp`: passed.
- Unity/Roslyn editor source compile using `Assembly-CSharp-Editor.rsp` with the temporary runtime reference: passed.
- No-window deterministic forward-bound smoke: passed.
  - `playerLeaderX=107.5`
  - `enemyLeaderX=869.4`
  - `maxYDelta=51`
  - `coverEvents=3880`
  - `leadersInCover=5614`
  - `pulses=9`

### Risk update

- This should no longer camp the first nearby cover patch, but live tuning may still need one more pass if squads now advance too quickly through sparse cover.

## Addendum - Unit Readability And Straight-Line Blip Fix

### What changed

- Diagnosed the "two random squares" live-test symptom as the war supply-layer pulse placeholders, not actual soldiers.
- Suppressed those supply pulse markers during the combat wave drill so they no longer masquerade as units.
- Added larger far-zoom unit markers with command-unit labels so the live drill reads as squads even when the full 1000 x 600 war map is visible.
- Added lateral scoring to forward cover target selection so leaders prefer a practical covered bound with some side movement instead of a straight lane march.
- Added diagonal neighbor movement so squads can make smoother bounds toward cover targets rather than stepping in hard right angles.

### Tests/checks run

- `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln`: passed, but the generated solution currently contains no projects to restore/compile.
- Source-level runtime compile using Roslyn with Unity references: passed.
- Reflection smoke against the compiled runtime assembly: passed.
  - `alive P/E=132/132`
  - `playerLeaders=33`
  - `avgLeaderX=171.4`
  - `leaderXRange=17-505`
  - `leaderYRange=74-548`
  - `leadersOut=30`
  - `lateralRecent=33`
  - `contacts=1`
  - `trenches=2`
  - `pulses=11`
- Live Unity `Editor.log` tail check: no `error CS`, compilation failure, or common runtime exception found after the patch.

### Risk update

- The units are still grid-square proxies, not finished sprites, but they should now visibly read as many role-marked units instead of two stray supply blips.
- Diagonal movement affects all local war movement that uses `NeighborOffsets`; smoke looked healthy, but live combat feel should be watched for speed and spacing.
