# TWB Trenchworks Command System Gate 5 Progress Report

Date: 2026-05-22
Scope: TWB Trenchworks standalone Unity project
Worker: Bob / TWB Trenchworks standing worker

## Objective

Continue the command/tasking implementation plan with Gate 5: introduce command-side claim tracking without creating a second authority over existing front, support, or socket systems.

## What Changed

- Added an observing `CommandClaimRegistry`.
- The registry mirrors existing live claims from:
  - `WarFrontBlueprintClaim`
  - active `WarSupportRequest`
  - living member `ClaimedSocketId`
- `WarCommandDirector` now owns and clears the claim registry.
- `WarIntegrationFacade.Tick` now lets the command director observe the slice after the tactical slice tick.
- Command events now emit `ClaimCreated` when a source claim is first observed and `ClaimReleased` when the source claim disappears.
- War diagnostics now include compact active command-claim summaries.
- Added a dedicated `CommandClaimRegistrySmoke`.
- Updated the older command event-log smoke so it expects the new claim observer instead of a no-op tick layer.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\CommandClaimRegistry.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\CommandClaimRegistry.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\CommandClaimRegistrySmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\CommandClaimRegistrySmoke.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandDirector.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandEventLogSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarIntegrationFacade.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`

## Tests And Checks Run

- Temporary pure C# simulation smoke harness:
  - `WarCommandEventLogSmoke.RunPrototypeSmoke()` passed.
  - `WarSquadMissionControllerSmoke.RunPrototypeSmoke()` passed.
  - `CommandClaimRegistrySmoke.RunPrototypeSmoke()` passed.
  - Output included:
    - `command event log smoke passed=True`
    - `squad mission controller smoke passed=True`
    - `command claim registry smoke passed=True, event=True, active=True, diagnostics=True`
- `dotnet build TWB-TrenchWorks.sln --no-restore`
  - Result: passed, 0 warnings, 0 errors.
  - Note: solution build remains light/no-op; pure simulation harness is the stronger check.
- Unity editor log scan for `error CS`, `Compilation failed`, and `Scripts have compiler errors`
  - Result: no matching compile errors found.

## Cleanup Performed

- Removed temporary compile/smoke harness folder:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\CommandCompileSmoke`

## Risks

- The registry intentionally observes only. It does not yet deny, expire, or arbitrate claims beyond logging releases when source claims vanish.
- Claim-release paths are lightly covered by code shape, but the current smoke focuses on claim creation and diagnostics exposure.
- Command claim snapshots are currently diagnostics-only, not first-class snapshot DTOs.

## Memory-Worthy Notes

- The safest claim model is now established: existing tactical systems stay authoritative, command claims mirror them and provide debug visibility.
- Gate 6 retask logic should use this registry as evidence, not as a control surface yet.
- Do not let the command layer directly mutate `frontAssignments`, blueprint piece claims, support request assignment, or member socket claims until parity and release smokes are stronger.

## Follow-Up Recommendations

1. Add Gate 6 mission-retask detection based on repeated no-progress, released claims, unresolved support, or combat-ineffective teams.
2. Keep first retasks event-only or mission-state-only before changing tactical decisions.
3. Add a claim-release smoke once Gate 6 begins depending on claim lifecycle transitions.
