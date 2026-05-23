# TWB Trenchworks Command Plan Gate 10 Support Emplacement Report

Date: 2026-05-22
Worker: TWB Trenchworks standing worker
Scope: TWB Trenchworks standalone Unity project

## Summary

Gate 10 first support-emplacement brain pass is implemented and smoke-tested. Mortar pit, Aid/doctor point, Command dugout, and Supply cache/depot now expose support brain snapshots with crew, minimum crew, supply stock, selected need, fallback, state, and debug text. Light active effects are included where current systems can safely support them.

## What Changed

- Added `WarSupportEmplacementBrain.cs`:
  - `WarSupportEmplacementState`
  - `WarSupportEmplacementSnapshot`
- Added support emplacement tracking to `WarTeamSlice`.
- Added support emplacement snapshot building for:
  - `MortarPit`
  - `AidPost`
  - `CommandDugout`
  - `SupplyNiche`
- Added light support-emplacement effects:
  - Mortar pit can operate indirect fire using the current ammo/fire-support task effect.
  - Aid post can treat wounded through the current medical task effect.
  - Command dugout can relay command through the current command task effect.
  - Supply niche currently selects supply need and reports fallback/debug state; full depot transfer logic remains future.
- Added `WarSupportEmplacementBrainSmoke`.
- Wired the support brain smoke into `TWB Trenchworks/Run Command Plan Smoke Test`.
- Exposed support emplacement snapshots and diagnostics through `WarIntegrationFacade`.
- Added `WarTeamSlice.AddTeamForScenario(...)` to let smokes build planned/future squad roles without adding them to the live runtime roster.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarSupportEmplacementBrain.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarIntegrationFacade.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarSupportEmplacementBrainSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`

## Tests And Checks Run

- Unity batchmode compile:
  - Passed.
  - Log: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\codex-gate10-support-compile.log`
- Direct compiled-assembly command smoke set:
  - `WarCommandPlanDiagnosticsSmoke`: passed.
  - `WarCommandPlanRuntimeAliasSmoke`: passed.
  - `WarCommandPlanMissionProfileSmoke`: passed.
  - `WarMissionFamilyTaskCoverageSmoke`: passed.
  - `MemberTaskActiveSubsetSmoke`: passed.
  - `WarManEmplacementModeSmoke`: passed.
  - `WarSupportEmplacementBrainSmoke`: passed.

## Risks

- This is not the final support-emplacement AI. It exposes and lightly exercises brains, but target selection is still deliberately simple.
- Mortar support does not yet resolve blast damage, friendly-fire risk, or observer quality.
- Supply niche selects a need but does not yet transfer stock like a full depot.
- Aid post treats the owning team in this first pass; full casualty intake/evacuation queues remain future.

## Memory-Worthy Notes

- Gate 10 now has a visible debug surface for all four support emplacement categories requested by the implementation plan.
- The support brains are intentionally built on current task effects and snapshots, not a separate hidden AI stack.

## Follow-Up Recommendations

1. Expand support brains one by one, starting with supply cache transfer and AidPost casualty queue.
2. Add mortar target scoring only after observer/contact quality is explicit.
3. Keep `AddTeamForScenario(...)` scenario-only; do not use it for normal runtime spawning.
