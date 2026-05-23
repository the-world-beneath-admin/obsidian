# TWB Trenchworks Fog Readability And Reveal Report

Date: 2026-05-16
Worker: Bob / Codex
Scope: Standalone TWB-tagged Unity 2D game, TWB Trenchworks
Project path: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

## What Changed

- Changed war fog colors so unseen fog starts as readable grey instead of near-black.
- Made remembered and actively visible ground brighter and more distinct.
- Changed war-known ground rendering to fill the full cell instead of drawing tiny inset cells. This makes scouting visibly uncover ground rather than leaving reveal patches hidden between grid lines.
- Increased war-unit vision radius to suit the 800 x 600 battlefield scale:
  - Command: 18 cells
  - Rifle/default: 15 cells
  - Engineer/Sapper: 14 cells
  - Medic: 10 cells

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-fog-readability-reveal-report.md`

## How To Run It In Unity Hub

1. Open `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks` in Unity Hub.
2. Open `Assets\Scenes\TrenchworksPrototype.unity`.
3. Press Play.
4. The battlefield should now start under grey fog, while squads carve visibly brighter scouting patches as they move.

## Whether `prototype\My project` Was Involved

No. This pass only touched the current `TWB-TrenchWorks` project.

## Tests / Checks Run

- Runtime source compile against Unity 6000.3.8f1 UnityEngine assemblies: passed.
- Fog reveal smoke test:
  - Initial known/visible cells: 2532 / 2241
  - After 600 ticks: 22283 / 10025
  - Result: scouting visibility and remembered map knowledge both grew.
- Unity editor log tail was reviewed after script reload; no compile errors were present.

## Cleanup Performed

- Removed temporary compile artifacts from `Temp\CodexCompileCheck`.

## Risks

- Larger vision radii make fog easier to read but reveal more territory per squad. This is acceptable for current playtesting; later balance can tune vision by squad type and research.
- Full-cell visibility drawing is clearer, but the war map may need a dedicated fog overlay renderer later if OnGUI performance becomes a bottleneck.

## Memory-Worthy Notes

- Current war fog visual states:
  - grey = unseen,
  - warmer grey = remembered/scouted,
  - brighter ground = active sight.
- Reveal readability is now a rendering concern and a vision-radius concern; both were adjusted.

## Follow-Up Recommendations

- Add a proper fog legend to the right-side tracker once the UI has settled.
- Later, make scout squads/research affect vision radius while heavier attack teams reveal less.

## Anything Blocked

- Nothing blocked.
