# TWB Trenchworks War Command UI Spawn Tree Report

Date: 2026-05-22 11:03

## Scope

Standalone TWB-tagged game: TWB Trenchworks only.

## What Changed

- Replaced the war-mode bottom rail/category clutter with a focused war command surface.
- Added a `RES` button that selects the research tracker as a placeholder for the future research panel.
- Added a `UNITS` button that opens a tiered unit request tree.
- Added Tier 1, Tier 2, and Tier 3 selectors.
- Wired Tier 1 to the four currently live spawnable squad templates:
  - `scout_patrol`
  - `assault_section`
  - `fortify_engineers`
  - `supply_team`
- Left Tier 2 and Tier 3 visibly empty until real runtime spawn templates exist.
- Changed UI squad requests so the player general chooses the entry lane rather than the player selecting `TOP/MID/BOT`.
- Added a first-pass player-general lane scoring rule:
  - supply favors lanes with friendly teams
  - scout/fortify favor under-covered lanes
  - assault favors lanes with enemy pressure
  - middle lane wins ties

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-110339-trenchworks-war-command-ui-spawn-tree-report.md`

## Child Subagent

- Child explorer `019e5069-35ff-70b1-ae61-623296d4f471` inspected the current war bottom rail and spawn route.
- It confirmed the live templates and warned not to wire planned catalog-only unit IDs into spawning yet.
- A 2-minute heartbeat was set during child work and deleted after completion.

## Checks Run

From `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`:

```powershell
dotnet build "TWB-TrenchWorks.sln" --no-restore
```

Result: passed, 0 warnings, 0 errors.

## Cleanup Performed

- Deleted the temporary heartbeat automation after child work completed.
- No generated scratch files were created.
- No raw GPT Pro package files were modified.
- No staging, commit, reset, or broad cleanup was performed.

## Risks

- Unity Play Mode visual behavior was not re-verified in-editor during this pass.
- Tier 2 and Tier 3 intentionally show no spawnable units until runtime templates are implemented.
- The player-general lane choice is a simple first-pass scoring rule, not the full command-tasking system.
- The research button is a placeholder that selects the research tracker; the dedicated research panel remains to be implemented.

## Memory-Worthy Notes

- War-mode spawning is now moving toward "player requests units, general routes and tasks them" rather than manual lane picking.
- Do not connect planned `planned_*` squad catalog entries to live spawn buttons until their runtime templates and roles are actually implemented.

## Follow-Up Recommendations

- Add real Tier 2 and Tier 3 runtime squad templates before exposing their unit buttons.
- Implement the proper research panel behind the `RES` button.
- Fold the player-general lane scorer into the larger mission/tasking system once GPT Pro's command-system plan is reviewed.
- Run a Unity Play Mode check to confirm the new rail layout reads cleanly at 1920x1080.
