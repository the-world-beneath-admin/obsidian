# TWB Trenchworks Command System Gate 8 Progress Report

Date: 2026-05-22
Scope: TWB Trenchworks standalone Unity project
Worker: Bob / TWB Trenchworks standing worker

## Objective

Continue the command/tasking implementation plan with Gate 8: add squad-leader shadow member task assignment without changing physical member movement or combat behaviour.

## What Changed

- Added member task contracts:
  - `SquadLeaderTaskState`
  - `MemberTaskType`
  - `MemberTaskStatus`
  - `ReactionTrigger`
  - `ReactionPolicy`
  - `SquadBlackboard`
  - `MemberTask`
- Added `MemberTaskController` as a shadow-task creator.
- Added `MemberRoleActionCatalog` for bounded role/task compatibility.
- Added `SquadLeaderBrain`.
- `WarCommandDirector` now owns the squad leader brain and exposes `ShadowMemberTasks`.
- The squad leader brain now assigns role-appropriate shadow tasks for:
  - scout missions
  - engineer/build missions
  - supply missions
  - assault/hold missions
  - regroup/withdraw missions
  - leader-down fallback
- Shadow task assignments log `MemberTaskAssigned` command events when a member task changes.
- War diagnostics now include compact `member-tasks` and `member-task` rows.
- Added `SquadLeaderBrainSmoke`.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\MemberTaskController.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\MemberTaskController.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\MemberRoleActionCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\MemberRoleActionCatalog.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\SquadLeaderBrain.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\SquadLeaderBrain.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\SquadLeaderBrainSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\SquadLeaderBrainSmoke.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandDirector.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarIntegrationFacade.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`

## Tests And Checks Run

- Temporary pure C# simulation smoke harness:
  - prior command smokes passed
  - `SquadLeaderBrainSmoke.RunPrototypeSmoke()` passed
  - Output included:
    - `squad leader brain smoke passed=True, scout=True, engineer=True, supply=True, events=True, tasks=12`
- `dotnet build TWB-TrenchWorks.sln --no-restore`
  - Result: passed, 0 warnings, 0 errors.
- Unity editor log scan for `error CS`, `Compilation failed`, and `Scripts have compiler errors`
  - Result: no matching compile errors found.

## Cleanup Performed

- Removed temporary compile/smoke harness folder:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\CommandCompileSmoke`

## Risks

- Shadow tasks are diagnostics and command events only. They do not yet alter `WarSubUnit` movement, posture, combat, digging, or resupply behaviour.
- Role/action catalog is intentionally broad but shallow; it needs tuning once active task behaviour begins.
- Task events can increase command event volume. The event log ring buffer kept the smoke stable, but UI should show recent events only.

## Memory-Worthy Notes

- Squad leader tasking now exists as the middle layer between general missions and individual squad members.
- This preserves the intended command hierarchy: General assigns mission, SquadLeaderBrain assigns member tasks.
- Gate 9 can now activate a very small subset of member tasks safely because the shadow rows already exist.

## Follow-Up Recommendations

1. Gate 9 should activate only a tiny subset first: regroup/withdraw posture and low-risk observe/hold task effects.
2. Keep build/combat active task effects behind smokes until no task fights the existing `WarTeamSlice.ApplyDecision` logic.
3. Add selected-squad UI rows for current shadow tasks when touching UI next.
