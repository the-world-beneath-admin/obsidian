# TWB Trenchworks Command Plan Gate 0/1 Progress Report

Date: 2026-05-22
Worker: TWB Trenchworks standing worker
Scope: TWB Trenchworks standalone Unity 2D game

## What Changed

Implemented the first no-behavior-change bridge from `19_twb_plan_fit_audit_and_tailored_implementation.md`:

- Gate 0: command-plan compatibility vocabulary.
- Gate 1: data coverage diagnostics and smoke hook.

This does not switch runtime spawning to all 50 planned templates and does not alter combat behavior. It adds validation scaffolding so later gates can fail loudly instead of silently pretending that planned squads and missions are runnable.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandPlanCompatibilityCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandPlanDiagnosticsSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-twb-trenchworks-command-plan-gate0-gate1-progress-report.md`

## Implementation Details

Added `WarCommandPlanCompatibilityCatalog` with:

- Prototype-template aliases:
  - `scout_patrol` -> `planned_scout_patrol`
  - `assault_section` -> `planned_assault_section`
  - `fortify_engineers` -> `planned_fortify_engineer_crew`
  - `supply_team` -> `planned_porter_team`, with `planned_ammunition_relay_team` recorded as alternate future mapping
- Packet mission-family mappings to current live `WarSquadMissionType` values.
- Explicit placeholder status for future/unsupported packet mission families.
- Planned-template mission profile generation.
- Runnable-now flagging for prototype-backed planned templates.
- Hardpoint-family anchor coverage diagnostics.
- Safe role fallback diagnostics across all `WarMemberRole` values.

Added `WarCommandPlanDiagnosticsSmoke`, a pure read-only smoke wrapper around the compatibility diagnostics.

Wired `WarCommandPlanDiagnosticsSmoke.RunPrototypeSmoke()` into `TrenchworksProjectSetup.RunSimulationSmokeTest()` immediately after `WarFutureTeamHardpointGateSmoke`.

## Checks Run

Ran:

```powershell
dotnet build TWB-TrenchWorks.sln --no-restore
```

Result:

- Build succeeded.
- 0 warnings.
- 0 errors.

Also confirmed the new smoke is referenced by source search and the child subagent found the same canonical Unity menu smoke hook.

## Checks Not Run

Unity editor menu smoke was not executed in this turn. The project docs do not provide a project-local Unity automation wrapper, and the existing instruction is not to claim Unity/Play Mode validation unless it is actually run.

The next operator can run:

`TWB Trenchworks > Run Simulation Smoke Test`

from the Unity editor to execute the newly wired command-plan diagnostics inside the full smoke runner.

## Risks

- The diagnostics compile, but the Unity menu smoke should still be run to prove the editor smoke path accepts the new diagnostic.
- This is only Gate 0/1. Runtime alias spawning, mission-profile scoring, enemy mission assignment, man-emplacement mode, and tier UI remain unimplemented.
- Mission-family profile resolution is intentionally conservative and may need tuning once Gate 2/3 begin.

## Memory-Worthy Notes

- The plan implementation has begun with a no-behavior-change compatibility layer.
- The live prototype still spawns only four runtime ids; this pass records aliases but does not change spawning.
- The normal Unity simulation smoke now includes command-plan diagnostics.
- The next implementation gate is Gate 2: runtime alias layer, preserving old prototype ids while allowing planned ids to resolve safely.

## Follow-Up Recommendations

1. Run the Unity menu smoke to validate the new diagnostic inside the editor.
2. Implement Gate 2 runtime alias support without removing `scout_patrol`, `assault_section`, `fortify_engineers`, or `supply_team`.
3. After Gate 2, add mission-profile debug exposure before changing Player General scoring.
