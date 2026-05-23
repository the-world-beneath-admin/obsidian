# TWB Trenchworks Worker Report - Unit Buttons And Enemy General

Date: 2026-05-22 10:41
Worker: TWB Trenchworks standing worker
Scope: TWB Trenchworks standalone Unity project only

## What Changed

- Wired the active WAR tray unit buttons (`SCT`, `ASL`, `ENG`, `LOG`) through a dedicated playtest spawn path instead of the old direct integrated call.
- Each button now spawns one integrated squad/team immediately in the selected lane without using factory resources.
- Added a first enemy-general director slice in `TrenchworksSimulation`.
  - Successful player button spawns queue enemy responses.
  - Enemy responses mirror the player pressure lane, use simple scout/assault response mapping, respect the existing 24-team per-faction cap, and spawn after a short delay rather than instantly.
- Kept the F8 manual front-pair harness as a fallback/debug tool, but the interface buttons are now the intended playtest path.
- Confirmed the current MG nest and rifleman emplacement runtime mapping is already wired to the directional ProceduralV1 assets:
  - Player uses east-facing assets.
  - Enemy uses west-facing assets.
  - Both MG and rifleman front-assignment paths resolve through the same directional helpers.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-104151-trenchworks-unit-buttons-enemy-general.md`

## Checks Run

- `dotnet build "TWB-TrenchWorks.sln" --no-restore`
  - Result: passed with 0 warnings and 0 errors.
- Verified the ProceduralV1 emplacement asset roots contain 20 PNGs under `Assets\Art` and 20 PNGs under `Assets\Resources`.
- Verified code references for the directional emplacement mapping and runtime validator expectations.

## Child Subagent Review

- Child subagent `019e5054-4ccf-7c82-a030-f23f629d3b69` performed a read-only code investigation.
- Findings matched the implementation route:
  - Active unit buttons are the four WAR tray buttons.
  - Integrated spawn has no factory-resource cost.
  - Current system is team/squad based, not true single-soldier based.
  - Enemy responses should use the existing faction-aware integrated spawn path.
- The child made no file edits.

## Cleanup Performed

- Deleted the 2-minute heartbeat automation after implementation and report completion.
- Closed the child subagent after reviewing its findings.
- No scratch files or temporary generated artifacts were created.

## Risks

- "Spawn 1 unit" currently means one war squad/team button press, because `WarTeamTemplate` creates a leader plus members. True one-soldier spawning would require a new template/model decision.
- Enemy general is intentionally first-slice logic: reactive pressure, lane mirroring, simple response mapping, and caps. It does not yet evaluate front health, stalls, trench possession, supply state, or difficulty.
- Unity menu smoke/asset validators were not run from the editor in this pass; the C# solution build passed.

## Memory-Worthy Notes

- For Trenchworks single-player, the enemy should be treated as a war director that spawns pressure at the front, not as a fake factory/economy.
- The interface spawn controls should remain the primary playtest path; F8 can remain a debug fallback only.
- If Bob wants literal individual soldier spawning later, that is a simulation-template change rather than a UI wiring change.

## Follow-Up Recommendations

- Add an enemy-general HUD line showing pending response count, next response timer, and spawned/skipped counts.
- Add difficulty knobs: response delay, cap, pressure ratio, lane bias, and maximum unanswered player advantage.
- Move the enemy-general director into a standalone simulation class once its rules mature beyond this first playtest slice.
