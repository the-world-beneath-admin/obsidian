# 2026-05-16 TWB Trenchworks War Team Scenarios Diagnostics Implementation Report

## Scope

Standalone Unity 2D TWB Trenchworks prototype under The World Beneath umbrella.

Active project:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

This pass extended only the isolated war-team foundation under:

```text
Assets\Scripts\Simulation\War\
```

No live UI, `TrenchworksSimulation`, Data, Production, editor, bootstrap, permanent memory, wiki, index, hot, or log files were edited.

## Context read

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-full-implementation-plan-and-wireframes.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-war-team-ai-foundation-implementation-report.md`
- Existing isolated module under `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\`

## What changed

- Added `WarTeamScenarioBlueprint` and related blueprint records for:
  - spawns
  - contact markers
  - cover markers
  - trench values
  - supply overrides
- Added `WarTeamScenarioFactory` with five deterministic prototype scenarios:
  - `scout_probe`
  - `assault_no_mans_land`
  - `fortify_after_contact`
  - `supply_under_pressure`
  - `trench_connect_back_to_base`
- Added `WarTeamValidator` and `WarTeamValidationResult` for:
  - template member counts
  - template id uniqueness
  - leader role presence
  - supply-category sanity
  - entry lane anchors on the `1000 x 600` map
  - unique team ids
  - unique sub-unit ids
  - one-square occupancy for alive sub-units
  - valid member positions
- Added diagnostic aggregation:
  - `WarTeamDiagnosticSummary`
  - decision counts by `TeamDecisionKind`
  - diagnostic counts by severity
  - selected reason strings for UI/debug panels
- Added lightweight influence summaries:
  - `WarInfluenceSampleSummary`
  - aggregates only the local samples already attached to team decisions
  - does not scan the full `1000 x 600` map
- Added deterministic smoke API:
  - `WarTeamSmoke.RunSmoke(...)`
  - `WarTeamSmoke.RunAllPrototypeSmokes()`
  - returns `WarTeamSmokeResult` with validation, counts, decisions, diagnostics, and influence sample counts.
- Extended `WarTeamSlice` with scenario setup hooks for controlled blueprints:
  - forward deploy a team formation
  - set scenario contact
  - set scenario cover
  - set scenario trench value
  - add scenario diagnostic
- Improved team movement and supply behaviour after validation caught one-square occupancy failures:
  - members now preserve distinct formation cells after leader movement
  - supply teams stop adjacent to a target team instead of entering its occupied squares
  - repeated same-lane spawns now offset inside the lane to avoid immediate overlaps

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamScenariosDiagnostics.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamScenariosDiagnostics.cs.meta`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-war-team-scenarios-diagnostics-implementation-report.md`

## Tests/checks run

- Checked project status; target Unity project is not a git repository.
- Compiled with Unity's Roslyn response file plus the new isolated War source:

```powershell
mono.exe csc.exe @Library\Bee\artifacts\1900b0aE.dag\Assembly-CSharp.rsp Assets/Scripts/Simulation/War/WarTeamEntities.cs Assets/Scripts/Simulation/War/WarTeamSlice.cs Assets/Scripts/Simulation/War/WarTeamScenariosDiagnostics.cs -out:Assets/Scripts/Simulation/War/CodexCompileCheck.dll -refout:Assets/Scripts/Simulation/War/CodexCompileCheck.ref.dll -pdb:Assets/Scripts/Simulation/War/CodexCompileCheck.pdb
```

Result: compile exited `0`.

The standalone response-file invocation emitted Unity source-generator analyzer load warnings, as in the prior pass. No C# compile errors were reported.

- Ran a disposable smoke runner against `WarTeamSmoke.RunAllPrototypeSmokes()`.

Smoke result summary:

```text
scout_probe passed=True ticks=6 teams=2 decisions=2 diagnostics=4 samples=2
assault_no_mans_land passed=True ticks=6 teams=2 decisions=2 diagnostics=4 samples=2
fortify_after_contact passed=True ticks=8 teams=2 decisions=2 diagnostics=12 samples=2
supply_under_pressure passed=True ticks=8 teams=3 decisions=3 diagnostics=11 samples=3
trench_connect_back_to_base passed=True ticks=10 teams=3 decisions=3 diagnostics=14 samples=3
```

## Cleanup performed

- Removed temporary smoke runner source:

```text
Assets\Scripts\Simulation\War\CodexSmokeRunner.cs
```

- Removed temporary smoke/compile outputs:

```text
Assets\Scripts\Simulation\War\CodexSmokeRunner.exe
Assets\Scripts\Simulation\War\CodexSmokeRunner.pdb
Assets\Scripts\Simulation\War\CodexCompileCheck.dll
Assets\Scripts\Simulation\War\CodexCompileCheck.ref.dll
Assets\Scripts\Simulation\War\CodexCompileCheck.pdb
```

- Confirmed no `CodexSmokeRunner` or `CodexCompileCheck` artifacts remain under `Assets\Scripts\Simulation\War`.

## Risks

- The scenario blueprints are implementation fixtures, not balanced gameplay scenarios.
- Validation currently checks local structural sanity. It does not yet prove route quality, combat balance, or long-run trench-network correctness.
- The smoke API is pure C# and not yet attached to the Unity editor smoke menu.
- The Unity response file may remain stale until Unity imports the new file; compile checks explicitly included the new War sources.

## Memory-worthy notes

- The isolated war-team module now has deterministic scenarios suitable for future editor smoke tests and UI tracker work.
- One-square occupancy validation exposed and fixed two important movement/logistics issues:
  - formation members could collapse into the leader cell;
  - supply teams could walk into the target team's formation instead of stopping adjacent.
- Diagnostic aggregation is ready for a future right-side war tracker without requiring full-map scans.
- Future integration should surface `WarTeamSmokeResult`, `WarTeamDiagnosticSummary`, and `WarInfluenceSampleSummary` before adding heavier AI.

## Next integration recommendation

Parent integration should keep this module read-only at first and add a narrow editor smoke method that calls `WarTeamSmoke.RunAllPrototypeSmokes()`, reports failed validation errors, and leaves live `TrenchworksSimulation` behaviour unchanged.

## Anything blocked

Nothing blocked.
