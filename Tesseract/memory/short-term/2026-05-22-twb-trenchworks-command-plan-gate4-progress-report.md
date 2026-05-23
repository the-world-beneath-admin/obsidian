# TWB Trenchworks Command Plan Gate 4 Progress Report

Date: 2026-05-22
Scope: Standalone TWB-tagged Unity 2D game - TWB Trenchworks.

## What Changed

- Implemented the first scoped Gate 4 Player General scoring pass for the four runnable alias-backed squads:
  - Scout Patrol.
  - Assault Section.
  - Fortify Engineer Crew.
  - Porter/Supply Team.
- Added a small read-only `PlayerGeneralAssignmentContext` built from live `WarTeamSlice` state after spawn.
- Scoring context currently includes:
  - target sector/piece hint,
  - lane pressure,
  - known contact pressure,
  - trench/front need,
  - supply pressure,
  - casualty pressure,
  - hardpoint claim availability,
  - retask cooldown pressure placeholder.
- Updated `PlayerGeneral` to score legal mission candidates from the Gate 3 mission profile, then fall back to the old kind/order assignment if no legal profile mission is available.
- `WarSquadMission` now records the assigned target sector hint and score.
- Command-plan smoke now verifies that runnable profile assignments expose both profile data and scoring context in mission summaries.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\PlayerGeneral.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandDirector.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandTypes.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandPlanMissionProfileSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarIntegrationFacade.cs`

## Checks Run

- `dotnet build .\TWB-TrenchWorks.sln --no-restore`
  - Passed with 0 warnings and 0 errors.
- Unity batch menu smoke:
  - `TWB.Trenchworks.Editor.TrenchworksProjectSetup.RunCommandPlanSmokeTest`
  - Passed.
  - Result summary:
    - compatibility passed `True`
    - aliases `4/True`
    - mission families `32/True`
    - template profiles `50/True`
    - runnable profiles `4`
    - placeholders `13`
    - Gate 3 profiles `True`
    - runtime alias smoke passed `True`
    - mission profile smoke passed `True`
    - scoring context `True`

## Cleanup Performed

- No source files, user files, raw evidence, or reports were deleted.
- Unity smoke log remains at:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\codex-command-plan-gate4-smoke.log`

## Risks

- Gate 4 is complete in scoped form for the current four runnable squads only. The full 50-template roster remains locked/future until later gates promote runtime templates.
- Retask cooldown pressure is recorded as a scoring-context field but not yet a meaningful input for first-spawn assignment. Retask behaviour itself still uses the existing command director path.
- The scoring context is intentionally aggregate and conservative; it does not expose private tactical blackboard/contact-map internals.
- Enemy squads still receive `NoActiveMission`; that remains Gate 5.

## Memory-Worthy Notes

- The safe Gate 4 pattern is: runtime alias -> planned mission profile -> read-only live context -> legal candidate scoring -> old fallback.
- Scoring is now visible in mission debug text and general dispatch paths because it is part of the real `WarSquadMission` snapshot.

## Follow-Up Recommendations

1. Gate 5 should give enemy response spawns real missions using the same profile vocabulary and legal mission checks.
2. Do not tune enemy difficulty until enemy missions are active; otherwise the difficulty knobs tune unassigned squads.
3. Keep Gate 6 focused on squad-leader/member-task coverage rather than expanding runtime templates prematurely.
