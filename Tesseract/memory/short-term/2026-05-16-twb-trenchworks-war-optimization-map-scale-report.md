# TWB Trenchworks War Optimization And Map Scale Report

## What changed

- Reduced the war map length from `1000 x 600` to `800 x 600`.
- Kept the factory map unchanged.
- Updated both the visible legacy war simulation and the integrated war-team slice to use the shorter 800-cell war width.
- Added a wave-drill live-unit cap of 96 units per side so the Play Mode drill does not stack unlimited squads before contact.
- Reduced random terrain density so the map still has cover/concealment variety without flooding the renderer.
- Replaced full-map active-cell rebuilding with an active-cell list that is marked when obstacles, trenches, or contacts appear.
- Changed crowding checks to inspect nearby occupied grid cells instead of scanning every unit on the map.
- Reduced wave-drill influence overlay rendering so non-command, non-contact scouting units do not each paint a large extra overlay every frame.
- Added far-zoom terrain sampling so obstacle-only terrain is thinned visually at full-map zoom while trenches and contacts still render in full detail.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-war-optimization-map-scale-report.md`

## How to run it in Unity Hub

- Open `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks` in Unity Hub.
- Let Unity recompile after the changed scripts import.
- Open `Assets\Scenes\TrenchworksPrototype.unity` if it is not already open.
- Press Play. The wave drill should now use the shorter 800-cell war map and should reach contact sooner.

## Whether `prototype\My project` was involved

- Not involved.
- This work was done only in the current canonical project: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

## Tests/checks run

- Source-level runtime compile using Roslyn with Unity references: passed.
- Optimized war smoke against the compiled runtime assembly: passed.
  - `mapWidth=800`
  - `alive P/E=95/95`
  - `pulses=11`
  - `contacts=5`
  - `trenches=23`
  - `activeCells=23176`
  - `maxPlayerX=383`
  - `minEnemyX=299`
- Prior same-pass smoke before active-cell/render thinning reached `contacts=14`, `trenches=57`, and `activeCells=40474`; the later pass reduced active terrain substantially while preserving contact.
- Live Unity `Editor.log` tail check found no `error CS`, compilation failure, or common runtime exception after the patch.

## Cleanup performed

- Removed temporary compile/smoke files under `Temp\CodexCompileCheck`.
- Did not write to Obsidian wiki, index, hot, or log.

## Risks

- This is still immediate-mode Unity GUI rendering; the far-zoom terrain sampling is a prototype optimization, not a final renderer.
- The 96-per-side drill cap is appropriate for Play Mode testing, but the final game will need proper unit pooling, spatial partitioning, and scenario pacing.
- The integrated war-team map width now matches the legacy visible war width, but any future design docs that still say `1000 x 600` should be treated as superseded for the current prototype test.
- Direct Unity Play Mode visual verification is still required because the user reported slowdown in the live editor.

## Memory-worthy notes

- Fact - Current Trenchworks war prototype map is now `800 x 600`.
- Fact - The Play Mode wave drill now caps live units at 96 per side.
- Fact - Terrain density and far-zoom rendering were reduced for performance while preserving cover/contact/trench behavior.
- Warning - Rendering thousands of terrain cells through `OnGUI` is not scalable; future work should move the war map renderer to meshes, tilemaps, or cached textures.

## Follow-up recommendations

- Live-test at 1x and 5x/6x speed and watch Unity Stats/frame rate once contact begins.
- If slowdown remains, the next pass should add a spatial index for enemy-range checks and move terrain rendering out of `OnGUI`.
- Consider a debug toggle for terrain detail so playtests can choose readability or performance.

## Anything blocked

- Unity batchmode/editor automation was not launched because the live Unity editor is already open on the project.
- Exact in-editor FPS still needs user-side visual confirmation.
