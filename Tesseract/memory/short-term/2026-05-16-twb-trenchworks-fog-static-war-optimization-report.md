# TWB Trenchworks Fog Static War Optimization Report

## What changed

- Added a prototype fog/static simulation layer for the war drill.
- Player units remain fully simulated because they define player influence.
- Enemy units outside player influence and active contact are hidden and moved through a cheap coarse formation march instead of running the full scouting/combat logic.
- Enemy units wake back into full simulation when they get near player units or recent contact.
- Added `ActiveSimulationUnits` and `StaticSimulationUnits` counters to the war model.
- Added those active/static counts to the wave drill status text.
- Hid far enemy units while they are static in fog.
- Hid unscouted terrain details in fog, leaving the map in a semi-static undisclosed state until player scouting reveals it.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-fog-static-war-optimization-report.md`

## How to run it in Unity Hub

- Open `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks` in Unity Hub.
- Let Unity recompile.
- Press Play in `Assets\Scenes\TrenchworksPrototype.unity`.
- Watch the right-side wave drill status line for `active X static Y`.

## Whether `prototype\My project` was involved

- Not involved.
- This work was done in the current canonical project at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

## Tests/checks run

- Source-level runtime compile using Roslyn with Unity references: passed.
- Fog/static war smoke against the compiled runtime assembly: passed.
  - `mapWidth=800`
  - `elapsedMs=22023`
  - `alive P/E=96/96`
  - `active/static=104/88`
  - `simActiveProps=104/88`
  - `pulses=11`
  - `contacts=1`
  - `trenches=5`
  - `maxPlayerX=441`
  - `minEnemyX=427`
  - `activeCells=23113`
- Live Unity `Editor.log` tail check found no `error CS`, compilation failure, or common runtime exception after the patch.

## Cleanup performed

- Removed temporary compile/smoke files under `Temp\CodexCompileCheck`.
- Did not write to Obsidian wiki, index, hot, or log.

## Risks

- This is a prototype fog/sleep model, not a final RTS fog-of-war system.
- Coarse enemy movement may make far enemy squads feel slightly less organic until they enter the active zone.
- Active distance is currently a hard radius around player influence/contact and may need tuning after live playtest.
- The final scalable path is still spatial partitioning plus a renderer that is not immediate-mode `OnGUI`.

## Memory-worthy notes

- Fact - War drill now supports active/static unit counts.
- Fact - Enemy units outside player influence can be hidden and coarse-simulated.
- Fact - Fog now hides unscouted terrain details rather than rendering all terrain information immediately.
- Warning - Hidden/static simulation must preserve contact pressure; if the front feels too empty, increase fog activation range or coarse march speed.

## Follow-up recommendations

- Live-test at `5x` and watch whether `static` stays meaningfully above zero before contact.
- If contact feels delayed, increase `FogCoarseStepsPerSecond` or reduce the activation radius only after checking frame rate.
- Later, replace the hard radius with squad-level fronts, communication trenches, and scouting reports.

## Anything blocked

- Unity batchmode/editor automation was not launched because the live Unity editor is already open on the project.
- Exact live FPS remains a user-side Play Mode check.
