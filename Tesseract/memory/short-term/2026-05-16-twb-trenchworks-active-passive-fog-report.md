# TWB Trenchworks Active/Passive Fog Report

Date: 2026-05-16
Worker: Bob / Codex
Scope: Standalone TWB-tagged Unity 2D game, TWB Trenchworks
Project path: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

## What Changed

- Added a separate active player visibility state on war cells.
- Kept previous scouting as remembered map knowledge, while active visibility now refreshes from live player units every strategic second.
- Added player-known and player-visible cell lists/counters for rendering and diagnostics.
- Changed war map rendering so:
  - never-seen ground is very dark,
  - remembered ground is dim,
  - actively visible ground remains clear,
  - terrain, trenches, and contact marks in remembered areas render dimmed,
  - enemy units are hidden unless they are inside current player sight.
- Updated the wave drill status line to show `sight visible/known` counts.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-active-passive-fog-report.md`

## How To Run It In Unity Hub

1. Open Unity Hub.
2. Open project folder: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
3. Open scene: `Assets\Scenes\TrenchworksPrototype.unity`.
4. Press Play.
5. In the war drill, bright ground is actively visible, dim ground is remembered, and black/dark ground has not been scouted.

## Whether `prototype\My project` Was Involved

No. This pass only used the current project home:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

The obsolete `prototype\My project` path was not touched.

## Tests / Checks Run

- Runtime source compile using Roslyn against Unity 6000.3.8f1 UnityEngine runtime assemblies: passed.
- Reflection smoke test against `CreateWarWaveDrillScenario()` for 1800 simulation ticks: passed.
  - Player known cells: 37035
  - Player visible cells: 6134
  - Hidden enemy units outside active sight: 96
  - Visible enemy units at that smoke-test moment: 0
  - Active/static simulation split: 97 active / 95 static
  - Alive units: 96 player / 96 enemy
- Unity editor log tail check for `error CS`, exceptions, or touched script errors: no matching issues found.

## Cleanup Performed

- Removed temporary compile artifacts under `Temp\CodexCompileCheck` after validation.

## Risks

- Remembered fog currently remembers the live cell state, not a frozen historical snapshot. If an enemy trench changes after the player leaves, the terrain state may still update in a remembered area. This is acceptable for the prototype pass but should become a proper last-known snapshot later.
- Remembered ground is sampled at very far zoom to protect frame rate, so it may look slightly textured instead of perfectly smooth when zoomed way out.
- The enemy base markers are still shown as strategic known objectives. This matches the current prototype readability, but a later pass can hide or stylize enemy-base intelligence if desired.

## Memory-Worthy Notes

- Active/passive fog is now part of the war prototype: current sight is distinct from remembered scouting.
- Enemy troop rendering is tied to current player visibility, not merely to whether the unit is fully simulated.
- The top HUD now exposes fog diagnostics with visible/known cell counts.

## Follow-Up Recommendations

- Add a proper last-known terrain snapshot for trenches, obstacles, and contacts if the player should not receive out-of-sight construction updates.
- Add a small fog legend or right-panel diagnostic once the UI settles, but avoid cluttering the playfield.
- Consider tying fog reveal radius to scout/team type once the squad research tree and team spawning UI are wired in.

## Anything Blocked

- No blocker for this fog pass.
- A live Unity Play Mode visual check is still recommended because this validation was source-level plus simulation smoke, not an automated screenshot capture from the open editor.
