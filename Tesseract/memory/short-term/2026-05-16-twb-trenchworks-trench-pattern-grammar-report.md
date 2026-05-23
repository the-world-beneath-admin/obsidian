# TWB Trenchworks Trench Pattern Grammar Report

Date: 2026-05-16
Worker: Bob / Trenchworks playtest stabilization
Scope: TWB Trenchworks standalone Unity 2D prototype

## What Changed

- Spawned and decommissioned one research subagent to study WW1 trench layout patterns for grid translation.
- Added trench metadata for roles: fire line, communication trench, traverse, sap, and emplacement.
- Added trench fortification-slot metadata for future equipment placement: rifle step, machine-gun nest, mortar pit, artillery pocket, dugout, ammo dump, aid post, observation post, and listening post.
- Added new trench pattern kinds: diagonal and traverse.
- Changed first trench seeding so main/fire trenches begin north-south instead of automatically running straight toward the enemy.
- Kept side connectors available so supply/communication trenches can grow east-west from the north-south line.
- Changed trench stamping from broad overlapping 3x3 blobs to a cleaner width brush:
  - front/fire-line pieces average 4 tiles wide
  - communication, diagonal, and traverse pieces are 3 tiles wide
- Added visible slot markers on trench cells, with labels such as `MG`, `M`, `D`, `+`, and `O` at readable zoom.
- Updated the in-map legend to call out 3-4 wide trenches and slot markers.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-trench-pattern-grammar-report.md`

## How To Run It In Unity Hub

Open:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

Open scene:

`Assets\Scenes\TrenchworksPrototype.unity`

Press Play. In the wave drill, trenches should now appear as wider, more structured north-south fire-line pieces with east-west connector growth and visible slot markers for future equipment positions.

## Whether `prototype\My project` Was Involved

No. This pass touched only the new canonical project:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

## Tests And Checks Run

- Unity Roslyn direct compile for `Assembly-CSharp` completed with exit code 0 and no compiler output.
- `dotnet build TWB-TrenchWorks.sln` reported success, with the known warning that the solution has no project to restore.
- `rg` source checks confirmed the new trench roles, slot enums, width helper, slot helper, and render hooks.
- Unity Editor log still showed the previous stale compile error from before the earlier switch-expression fix; direct Roslyn compile confirms the current source parses.

## Research Sources Used

- [William H. Waldron, *Elements of Trench Warfare*](https://www.gutenberg.org/files/61330/old/61330-h/61330-h.htm)
- [Britannica - Trench Warfare](https://www.britannica.com/topic/trench-warfare)
- [National WWI Museum and Memorial - Trench Warfare](https://www.theworldwar.org/learn/about-wwi/trench-warfare)
- [World History Encyclopedia - Trench Warfare on WWI's Western Front](https://www.worldhistory.org/article/2820/trench-warfare-on-wwis-western-front/)
- [Notes on the use of machine guns in trench warfare](https://upload.wikimedia.org/wikipedia/commons/f/fe/Notes_on_the_use_of_machine_guns_in_trench_warfare_and_on_the_training_of_machine_gun_units_compiled_from_foreign_reports_%28IA_notesonuseofmach00armyiala%29.pdf)
- [NM Archive WW1 trench glossary](https://www.nmarchive.com/learn-about-ww1)

## Cleanup Performed

- Closed the trench-pattern research subagent after its report completed.
- No scratch files, screenshots, or generated temporary artifacts were left behind.

## Risks

- Fortification slots are metadata and visual markers only. They do not yet spawn usable machine guns, mortars, artillery, or supply structures.
- The current generator is still unit-driven and incremental; it is not yet a full planned three-band trench system with support/reserve lines.
- The user should visually test whether 3-4 tile trench widths feel right with 2x2 soldiers and 2x4 command units. If too wide, preserve 4-tile rooms/slots but narrow ordinary communication trenches later.
- The open Unity Editor may need a Play stop/restart or script reimport before its log stops showing the old stale compile error.

## Memory-Worthy Notes

- Trenchworks should treat WW1 trench layouts as a shape grammar: front/fire lines, communication lines, traverses, saps, and strongpoint slots.
- Main/front trenches should trend north-south relative to the current left-right battlefield.
- Supply/communication trenches should run east-west, connecting the front back toward entry/base zones.
- Trench cells now have explicit role and fortification-slot metadata, which can later drive AI behavior, equipment placement, and supply rules.

## Follow-Up Recommendations

- Add a second pass that creates support and reserve trench bands behind the first fire line.
- Make slot markers influence squad AI: machine-gun slots attract suppressive teams, mortar slots attract indirect fire teams, aid/dugout slots attract wounded and retreating units.
- Add a validation pass for trench generation: no long straight exposed lanes, every fire-line cluster has an east-west communication connector, and slots are not overpacked.
- Build actual emplacement entities only after the visual trench grammar survives playtesting.

## Anything Blocked

- Nothing source-level is blocked.
- Full confirmation is blocked on live Unity Play Mode review after the editor reloads the latest scripts.
