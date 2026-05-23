# TWB Trenchworks Command Plan Gate 7 Progress Report

Date: 2026-05-22
Scope: TWB Trenchworks standalone Unity 2D game
Plan: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\implementation-packets\command-system-2026-05-22\19_twb_plan_fit_audit_and_tailored_implementation.md`
Gate: 7 - First Emplacement Proof: Rifle Bay And MG Point

## What Changed

- Added a thin `ManEmplacementMode` runtime layer derived from existing trench/front data.
- Implemented Gate 7 only for:
  - `rifle-firing-bay` -> `WarFrontAnchorKind.RiflePosition`
  - `front-line-empty-mg-point` -> `WarFrontAnchorKind.FrontLineEmptyMachineGunPoint`
- Added per-tick emplacement snapshots with visible states:
  - `Unmanned`
  - `Manned`
  - `LowAmmo`
  - `CrewLoss`
  - `Overrun`
  - `Abandoned`
- Rifle bays now provide a defensive rifle-range and hit-chance bonus when a squad is seated in completed rifle fire-step sockets.
- Front-line empty MG points now apply bounded forward-arc suppression from the correct facing.
- MG point suppression does not fire backwards into the trench/rear side.
- Command/debug snapshots now expose emplacement state and diagnostic lines.
- Added a focused Gate 7 smoke test and wired it into the command-plan smoke menu path.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarManEmplacementMode.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarIntegrationFacade.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarManEmplacementModeSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`

Unity generated `.meta` files for the two new scripts.

## Verification

- `dotnet build .\TWB-TrenchWorks.sln --no-restore`
  - Passed, but this solution currently has no project entries, so it is not a meaningful Unity compile proof.
- Unity batchmode command-plan run:
  - First run compiled and executed, then failed on the new smoke before the MG fallback-operator correction.
  - Later batchmode runs compiled successfully but did not re-enter `executeMethod`; this was recorded as inconclusive, not counted as a pass.
- Direct compiled-assembly command-plan smoke set:
  - Passed:
    - `WarCommandPlanDiagnosticsSmoke`
    - `WarCommandPlanRuntimeAliasSmoke`
    - `WarCommandPlanMissionProfileSmoke`
    - `WarMissionFamilyTaskCoverageSmoke`
    - `WarManEmplacementModeSmoke`

Gate 7 smoke proof:

```text
man emplacement mode smoke passed=True, mapping=True, rifleManned=True, rifleBonus=True, mgManned=True, mgFacing=True, states=True, claims=True
rifleChance=38->46
moraleForward=100->88
moraleRear=100->100
lowAmmo=True, crewLoss=True, overrun=True, abandoned=True, claims=True
```

## Cleanup

- No scratch source files were created.
- Unity generated script `.meta` files were kept because they belong with the new Unity scripts.
- No git staging or commits were performed.

## Risks

- Runtime MG squads are still not a full promoted playable template set; the Gate 7 proof allows current prototype-capable soldiers to operate the empty MG socket until the full roster promotion reaches that gate.
- The emplacement brain is intentionally thin. It proves rifle bay and MG point behavior, but it does not implement mortar, aid, command, supply, relief crew, repair crew, or full emplacement logistics.
- Unity batchmode `executeMethod` behaved inconsistently after the first failure. The pure simulation smoke passed against the compiled Unity assembly, but a fresh Unity menu pass should be retried before calling the whole command-system plan finished.

## Memory-Worthy Notes

- Gate 7 is implemented in scoped form.
- The correct architectural bridge is now in place: hardpoint family -> front blueprint piece/trench plan -> socket claims -> derived emplacement state -> tactical effect.
- MG facing is proved by forward morale loss with unchanged rear morale in the smoke.

## Follow-Up

- Next gate is Gate 8: catalog-driven Tier 1/2/3 UI tree.
- Gate 8 should only enable runnable squads and should label data-covered/future/placeholder squads plainly.
- Do not expand support emplacement brains until Gate 10; Gate 7 should remain limited to rifle bay and front-line empty MG point.
