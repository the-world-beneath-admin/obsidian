# 2026-05-16 TWB Trenchworks War Unlock Effects Implementation Report

## Scope

Standalone Unity 2D TWB Trenchworks prototype under The World Beneath umbrella.

Active project:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

This pass extended only the isolated War module under:

```text
Assets\Scripts\Simulation\War\
```

No live UI, `TrenchworksSimulation`, Data, Production, Research runtime, editor, bootstrap, permanent memory, wiki, index, hot, or log files were edited.

## Context read

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-research-tree-design-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-war-team-scenarios-diagnostics-implementation-report.md`
- Existing isolated module under `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\`

## What changed

- Added isolated war research/unlock helper models:
  - `WarUnlockState`
  - `WarResearchEffect`
  - `WarUnlockGate`
  - `WarUnlockEvaluator`
  - `WarTemplateAvailability`
  - `WarUpgradeSummary`
  - `WarUnlockDiagnostics`
- Added prototype research ids matching the war tree design report, including:
  - `war.t1.team_muster`
  - `war.t1.entry_lanes`
  - `war.t1.scout_patrols`
  - `war.t1.rifle_sections`
  - `war.t1.dig_in_crews`
  - `war.t1.porter_teams`
  - `war.t2.cover_posture`
  - `war.t2.fire_trenches`
  - `war.t2.supply_routes`
  - `war.t2.mg_nests`
  - `war.t2.observers`
  - `war.t3.trench_mortars`
  - `war.t3.field_guns`
  - `war.t3.base_bombardment`
  - `war.t3.enemy_base_breach`
- Added gates for:
  - team spawning
  - top/middle/bottom entry-lane use
  - scout, assault, fortify, and supply team templates
  - half/full cover and posture behavior
  - trench connection
  - light MG nests
  - artillery observers
  - mortar/field-gun emplacements
  - base bombardment readiness
  - enemy-base breach path
- Added pure helper methods future integration can call:
  - team template availability checks
  - entry lane availability checks
  - emplacement availability checks
  - decision score bonuses
  - cover danger reduction
  - trench connection eligibility
  - base bombardment readiness eligibility
  - diagnostic message generation
- Added deterministic unlock smoke API:
  - `WarUnlockSmoke.RunPrototypeSmoke()`
  - `WarUnlockSmokeResult`

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarUnlockEffects.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarUnlockEffects.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarUnlockSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarUnlockSmoke.cs.meta`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-war-unlock-effects-implementation-report.md`

## Tests/checks run

- Checked project status; target Unity project is not a git repository.
- Compiled with Unity's Roslyn response file plus the isolated War sources:

```powershell
mono.exe csc.exe @Library\Bee\artifacts\1900b0aE.dag\Assembly-CSharp.rsp Assets/Scripts/Simulation/War/WarTeamEntities.cs Assets/Scripts/Simulation/War/WarTeamSlice.cs Assets/Scripts/Simulation/War/WarTeamScenariosDiagnostics.cs Assets/Scripts/Simulation/War/WarUnlockEffects.cs Assets/Scripts/Simulation/War/WarUnlockSmoke.cs -out:Assets/Scripts/Simulation/War/CodexCompileCheck.dll -refout:Assets/Scripts/Simulation/War/CodexCompileCheck.ref.dll -pdb:Assets/Scripts/Simulation/War/CodexCompileCheck.pdb
```

Result: compile exited `0`.

The standalone response-file invocation emitted the same Unity source-generator analyzer load warnings seen in prior passes. No C# compile errors were reported.

- Ran a disposable smoke runner against `WarUnlockSmoke.RunPrototypeSmoke()`.

Smoke result summary:

```text
passed=True lockedTeam=True unlockedTeam=True lockedEmplacement=True unlockedEmplacement=True entryLane=True upgradedCoverTrench=True
locked team: locked: requires war.t1.team_muster
unlocked team: available: scout_patrol research complete
locked emplacement: locked: Light MG Nest requires war.t2.mg_nests
unlocked emplacement: available: war.t2.mg_nests complete
entry lane: available: war.t1.entry_lanes complete
upgrade summary: war upgrades: scout +0, assault +0, fortify +6, supply +6, half cover -6, full cover -16, trench speed +20, supply route +15, bombardment +25
trench connection: available for held contact
```

## Cleanup performed

- Removed temporary smoke runner source:

```text
Assets\Scripts\Simulation\War\CodexUnlockSmokeRunner.cs
```

- Removed temporary compile/smoke outputs:

```text
Assets\Scripts\Simulation\War\CodexUnlockSmokeRunner.exe
Assets\Scripts\Simulation\War\CodexUnlockSmokeRunner.pdb
Assets\Scripts\Simulation\War\CodexCompileCheck.dll
Assets\Scripts\Simulation\War\CodexCompileCheck.ref.dll
Assets\Scripts\Simulation\War\CodexCompileCheck.pdb
```

- Confirmed no `CodexUnlockSmokeRunner` or `CodexCompileCheck` artifacts remain under `Assets\Scripts\Simulation\War`.

## Risks

- This is an isolated helper layer. It does not yet consume Descartes' Research runtime state directly.
- Prototype effect magnitudes are intentionally simple and need balancing after live integration.
- The evaluator currently maps known template ids by string. This is suitable for the isolated module but should later align with Hubble's catalog ids.
- Base bombardment readiness is a pure eligibility helper here, not a live victory/damage system.

## Memory-worthy notes

- War systems now have a research-unlock helper surface that can be driven later by completed research ids without depending on Data, Production, or Research runtime types.
- The prototype war research ids should remain stable for integration with Descartes' research system.
- Future UI can use `WarTemplateAvailability`, `WarUnlockCheck`, `WarUpgradeSummary`, and `WarUnlockDiagnostics` to explain locked teams, lanes, emplacements, and upgrades.
- Cover/trench upgrades are exposed as pure summaries and helper values rather than hard-wired into the live team decision loop.

## Next integration recommendation

Parent integration should add a narrow adapter from the Research runtime's completed-id set into `WarUnlockState`, then use `WarUnlockEvaluator` only for display/gating first. Do not wire unlock effects into live combat balance until the editor smoke path can run `WarUnlockSmoke.RunPrototypeSmoke()` alongside the existing war-team scenario smokes.

## Anything blocked

Nothing blocked.
