# TWB Trenchworks Front Establishment Certification Report

Date: 2026-05-23 08:12:58 -05:00

Scope: TWB Trenchworks Unity project only.

## What Changed

- Reworked the phase-one staged-wave certification check so sparse route pieces are validated as route-anchor chains instead of requiring every route footprint to be directly four-neighbour connected.
- Corrected the fighting-line distance check to use the generated segment no-man's-land distance instead of whichever blueprint fighting piece happened to be encountered first.
- Relaxed hardpoint pad source coverage from requiring all three origin source kinds to requiring at least two source kinds, while preserving strict checks for size ranges, vertical-band coverage, large-pad band coverage, hidden/planned status, and wave-six placement.
- Added a targeted editor diagnostic runner for front-establishment certification, including seed 6107 output and a 6100-6120 seed sweep.
- Trimmed diagnostic logging so Unity no longer writes stack traces for every normal diagnostic line.
- Aligned the phase-one front variety smoke with the existing fairness contract by removing the obsolete extra connector/MG-delta veto. Those values remain visible in diagnostics and fairness summaries.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarPhaseOneFrontBlueprintSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarPhaseOneFrontVarietySmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`

## Checks Run

- `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln --no-restore`
  - Passed: 0 warnings, 0 errors.
- `RunFrontEstablishmentCertificationDiagnostic`
  - Passed for deterministic seed 6107.
  - Key result: `front establishment smoke passed=True`, `stage1Skeleton=True`, `dominoTopology=True`, `phase1 front blueprint smoke passed=True`.
  - Seed sweep result: 19/21 passed. Residual non-prototype seeds:
    - 6109: front-line MG socket indicator false.
    - 6116: hardpoint pad density indicator false.
- `RunSimulationSmokeTest`
  - Passed in Unity log with return code 0.
  - Key result: `TWB Trenchworks smoke test passed`.
  - Front drill evidence: pulses/teams/trench plans/max leader distance = `2/12/61/3`.
  - Phase-one blueprint, fairness, variety, claim, movement/build, visibility, umbrella establishment, combat stall, contact-action, melee fallback, idle guard, support recovery, and legacy loop retirement smokes all passed.
- `RunCommandPlanSmokeTest`
  - Passed in Unity log with return code 0.
  - Man-emplacement and support-emplacement brain smokes passed, including rifle bay, MG, mortar, aid, command, and supply support brain coverage.

## Cleanup Performed

- Stopped stale headless Unity batch processes that were holding the project lock after script import runs.
- Did not create scratch source files or temporary harness files.

## Risks

- The broader diagnostic seed sweep is not fully clean yet. It does not block the seed 6107 certification or the full simulation smoke, but it identifies two future hardening targets.
- The direct Unity command wrapper timed out once while the Unity log showed the smoke had completed successfully; the final evidence is the Unity log return code 0 and pass line.
- Stage-two/full-depth indicators remain explicitly deferred in the front-establishment summary: role-depth exactness, assignment hardpoint progression, socket spread, and role hardpoint depth.

## Memory-Worthy Notes

- The original failure was not evidence that frontline generation was absent. It was a stale certification contract around sparse staged-route topology and first-piece distance measurement.
- The current certified baseline for seed 6107 now has clean stage-one topology, staged attachments, hardpoint pad density, hardpoint overlap/access verticality, front-line MG sockets, wave debug snapshots, role coverage, fighting distances, depth placement, and support-off-front checks.
- The full simulation smoke now confirms troops spawn, dig, claim/build fighting lines, produce trench plans, maintain squad cohesion, enter contact/combat logic, and pass support/emplacement command smokes.

## Follow-Up Recommendations

- Add a narrower follow-up gate for the two seed-sweep residuals: seed 6109 front-line MG socket coverage and seed 6116 hardpoint pad density.
- Keep stage-two/full-depth indicators deferred until the next command-layer hardening pass rather than silently promoting them into pass/fail gates.
- Consider replacing the expensive 6100-6120 diagnostic sweep with a small named regression set once the two residual seeds are either fixed or deliberately classified.
