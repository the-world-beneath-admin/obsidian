# TWB Trenchworks Front Establishment Certification Plan Report

Date: 2026-05-23
Scope: TWB Trenchworks standalone Unity project, war-side front-establishment certification gap.

## What Changed

Created a detailed project-local plan to test and fix the gap where Play Mode front-line generation appears functional but `WarFrontEstablishmentSmoke.RunPrototypeSmoke()` fails on deterministic seed `6107`.

Plan file:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\implementation-packets\front-establishment-certification-2026-05-23\01_front_establishment_certification_test_and_fix_plan.md
```

## Core Plan

The plan separates:

- visible live gameplay readiness, where spawned squads can move, dig, and fight;
- stricter certification readiness, where deterministic topology, role-depth placement, hardpoint progress, socket spread, and depth rules must pass or be re-scoped.

The first implementation gate is to add a targeted diagnostic runner that prints all existing `WarFrontEstablishmentSmokeResult.Diagnostics`, primary/repeat assignment summaries, and exact failed predicate details before making any logic changes.

## Files Touched

- Added `docs\implementation-packets\front-establishment-certification-2026-05-23\01_front_establishment_certification_test_and_fix_plan.md`
- Added this short-term report.

## Checks Run

No code or Unity smoke tests were run for this planning pass. This was a plan-only task based on the previous readiness audit, current memory context, and source inspection.

## Risks

- The smoke may be stale, but weakening it without diagnostics could hide a real topology defect.
- The front system may work for current four runtime squads while still failing future aid/mortar/MG role-depth guarantees.
- Stage 2 deferred checks currently read like failures, which can confuse readiness decisions.

## Recommended Next Gate

Implement Gate 1 from the plan: add `RunFrontEstablishmentCertificationDiagnostic` to `TrenchworksProjectSetup.cs`, run it in Unity batchmode, and classify each failing predicate before modifying the generator, assignment planner, or smoke expectations.
