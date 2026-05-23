# TWB Trenchworks Command Plan Gate 3 Progress Report

Date: 2026-05-22
Scope: Standalone TWB-tagged Unity 2D game - TWB Trenchworks.

## What Changed

- Implemented Gate 3 mission-family profiles on top of the existing Gate 0-2 compatibility layer.
- Extended `WarTemplateMissionProfile` with:
  - required role families,
  - relevant hardpoint family coverage,
  - support/combat contact rule,
  - profile implementation status,
  - primary and fallback live `WarSquadMissionType` targets,
  - locked/future visibility.
- Added profile lookup by planned id or runtime prototype id so current prototype squads resolve to their planned profile.
- Updated `PlayerGeneral` so runnable squads choose from their mission profile first, then fall back to the old kind/order assignment if the profile target is not executable for that team kind.
- Preserved current tactical behaviour. The profile layer biases initial mission assignment only; it does not replace `WarTeamSlice` combat, contact, suppression, movement, digging, or safety logic.
- Added Gate 3 smoke coverage and included it in the Unity command-plan menu smoke.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandPlanCompatibilityCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\PlayerGeneral.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandDirector.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandPlanMissionProfileSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandPlanMissionProfileSmoke.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`

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

## Cleanup Performed

- No source files, user files, raw evidence, or reports were deleted.
- Unity generated the `.meta` file for the new smoke script during the batch smoke.
- The Unity smoke log remains at:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\codex-command-plan-gate3-smoke.log`

## Risks

- Gate 3 is complete in scoped form, but the whole command-plan implementation is not complete.
- `PlayerGeneral` profile scoring is still deliberately simple. Gate 4 still needs real score inputs such as pressure, contact, trench/front state, supply pressure, casualty pressure, hardpoint availability, and retask cooldown.
- Enemy squads still receive `NoActiveMission`; that remains Gate 5.
- Emplacement brains and `ManEmplacementMode` are still future gates.

## Memory-Worthy Notes

- The current safe bridge is profile-first assignment for runnable squads with old kind/order fallback.
- All 50 planned squads now produce Gate 3-complete profiles, while only the 4 prototype-alias runnable squads can spawn.
- Unsupported/planned-only squads are profile-covered and visibly locked/future rather than silently implied runnable.

## Follow-Up Recommendations

1. Gate 4 should add real `PlayerGeneral` scoring for the runnable squads without expanding runtime spawning beyond the alias-backed set.
2. Gate 5 should route enemy spawns through a real enemy mission assignment path so enemy squads no longer default to `NoActiveMission`.
3. Gate 7 should remain the first emplacement proof for rifle bay and MG point only; do not build every emplacement brain at once.
