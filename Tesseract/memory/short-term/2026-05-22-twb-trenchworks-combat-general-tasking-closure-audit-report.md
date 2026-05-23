# TWB Trenchworks Combat / General / Squad Tasking Closure Audit

Date: 2026-05-22
Scope: TWB Trenchworks standalone Unity project.
Worker: Bob, TWB Trenchworks standing worker.

## Task

Audit and close the current command/general/combat/squad-tasking loops before returning to art production. Focus areas:

- Player and enemy general mission assignment.
- Squad mission hints and retasking.
- Soldier contact detection, engagement, ammo use, and unsafe charge prevention.
- Member task effects for rifle/MG/combat tasks.
- Rifle/MG/support emplacement readiness and firing/support behavior.

## Findings

The live combat slice already had functional squad contact detection, rifle exchanges, ammo consumption, damage, support requests, rifle-bay bonuses, and MG emplacement effects.

The audit found and fixed three closure gaps:

1. Enemy general missions were assigned but not steering live enemy decisions. `WarCommandDirector.TryGetDecisionHint` only exposed hints for player missions.
2. Empty-ammo open-ground melee fallback could still become a long visible-enemy charge. It now only triggers at true close-assault range and only when the local combat edge is acceptable.
3. Member tasking labelled `FireAtContact`, `SuppressContact`, and `OperateMachineGun`, but those tasks did not affect live ammo/action state. They now spend task fire through the team only when a recent combat signal exists, with cadence protection so one squad does not dump ammo multiple times in the same tick.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandDirector.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamEntities.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\MemberTaskController.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarSquadMissionControllerSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\MemberTaskActiveSubsetSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarFrontCombatStallSmoke.cs`

## Checks Run

Unity batch compile:

```powershell
& 'C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Unity.exe' -batchmode -quit -projectPath 'C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks' -logFile 'C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\codex-combat-tasking-audit-compile.log'
```

Result: passed; final compile log contained no `error CS` or `Scripts have compiler errors`.

Direct compiled-assembly smoke harness:

- `WarFrontCombatStallSmoke` passed.
- `WarOpenGroundMeleeFallbackSmoke` passed.
- `WarOpenGroundIdleGuardSmoke` passed.
- `WarRangeSpottingPostureSmoke` passed.
- `WarSupportRecoverySmoke` passed.
- `WarSquadMissionControllerSmoke` passed, including enemy mission hint exposure.
- `WarMissionRetaskSmoke` passed.
- `SquadLeaderBrainSmoke` passed.
- `MemberTaskActiveSubsetSmoke` passed, including combat task effects.
- `WarManEmplacementModeSmoke` passed, including rifle bay and MG facing/effect states.
- `WarSupportEmplacementBrainSmoke` passed.
- `WarMissionFamilyTaskCoverageSmoke` passed.
- `WarCommandPlanMissionProfileSmoke` passed.
- `EnemyGeneralBudgetDifficultySmoke` passed.

## Current Verdict

The current prototype loop is closed enough to return to art work:

- Squads detect enemy squads.
- Rifle combat spends ammo and applies damage.
- Low-ammo squads avoid haphazard open-ground charges.
- Player and enemy general missions now both provide decision hints.
- Combat-ineffective squads retask toward regroup/withdraw.
- Rifle/MG member task labels now have live ammo/action effects when combat is actually signalled.
- Rifle bays are manned and improve rifle fire.
- MG emplacements face forward, spend ammo, suppress/pin/damage targets in their arc.
- Support emplacements activate and perform first-pass support effects.

## Remaining Risks

- Mortar support still records fire support and spends ammo, but does not yet resolve full blast-area battlefield damage. That is acceptable for the current closure pass, but should become its own dedicated combat-effects gate later.
- Rifle bays still primarily boost squad rifle combat rather than having a separate independent rifle-bay brain. This is acceptable because the squad combat loop is the actual firing loop.
- Unity Play Mode was not run manually; this pass used batch compile plus direct simulation smokes.

## Cleanup

- No temporary source harness files were created.
- No Git operations were performed.
- The read-only child audit was reviewed and incorporated.

## Memory-Worthy Notes

- Enemy missions must always be checked at both layers: assignment/event log and `TryGetDecisionHint` exposure. Assignment alone can look correct while the live squad brain ignores the order.
- Member tasking should reinforce the live combat system, not duplicate it. The current bridge only spends combat-task ammo when the team already has a recent combat signal.
- Keep the next art pass unblocked, but schedule a later mortar/fire-support damage-resolution gate before treating support weapons as fully simulated.
