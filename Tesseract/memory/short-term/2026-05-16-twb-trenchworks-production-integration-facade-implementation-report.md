# 2026-05-16 TWB Trenchworks Production Integration Facade Implementation Report

## Scope

Standalone TWB-tagged game: TWB Trenchworks.

Active Unity project:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

This pass extended only the isolated Production module. It did not edit Data/catalog work, War/team work, Research runtime work, `TrenchworksSimulation`, Unity bootstrap, editor setup, or permanent memory.

## What changed

- Added `ProductionIntegrationFacade` as a stable pure-C# adapter over:
  - `ProductionWorldSlice`
  - `ResearchProductionWorld`
- Added save-friendly/plain DTO-style objects:
  - `ProductionSubsystemConfig`
  - `ProductionSubsystemState`
  - `ProductionSubsystemSnapshot`
  - `ProductionInventorySnapshot`
  - `ProductionWorkerSnapshot`
  - `ProductionSiteSnapshot`
  - `ProductionTickResult`
- Added command/result objects:
  - `ProductionCommand`
  - `ProductionBuildRequest`
  - `ProductionResearchBuildingRequest`
  - `ProductionCommandResult`
- Added facade smoke result:
  - `ProductionFacadeSmokeResult`
- Added stable smoke API:

```csharp
ProductionIntegrationFacade.RunDeterministicSmoke()
```

## Facade capabilities

- Creates a prototype production + research-production state.
- Applies build commands by string id without depending on Data/catalog classes.
- Applies research-building commands by string id without depending on `Simulation\Research`.
- Ticks production and research-production together.
- Returns snapshot aggregates for:
  - combined worker counts,
  - worker hunger and fatigue,
  - front food,
  - coal,
  - water,
  - essence,
  - steam,
  - factory construction goods,
  - research points available and lifetime produced,
  - active diagnostics,
  - diagnostic summaries,
  - blocked building count,
  - footprint/access failure count.
- Returns tick deltas for:
  - steam produced,
  - steam consumed placeholder through inventory delta,
  - coal consumed,
  - water consumed,
  - essence consumed,
  - research points generated.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Production\ProductionIntegrationFacade.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-production-integration-facade-implementation-report.md`

## Checks run

- Read required context:
  - `memory\short-term\2026-05-16-twb-trenchworks-full-implementation-plan-and-wireframes.md`
  - `memory\short-term\2026-05-16-twb-trenchworks-production-scenarios-validation-implementation-report.md`
  - `memory\short-term\2026-05-16-twb-trenchworks-research-production-slice-implementation-report.md`
  - existing Production module under `Assets\Scripts\Simulation\Production`
- Compiled with Unity Roslyn using the available response file plus Production sources:

```powershell
dotnet exec "C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Data\DotNetSdkRoslyn\csc.dll" `
  "@Library\Bee\artifacts\1900b0aE.dag\Assembly-CSharp.rsp" `
  "Assets\Scripts\Simulation\Production\ProductionWorldSlice.cs" `
  "Assets\Scripts\Simulation\Production\ProductionDiagnosticSummary.cs" `
  "Assets\Scripts\Simulation\Production\ProductionValidator.cs" `
  "Assets\Scripts\Simulation\Production\ProductionScenarioFactory.cs" `
  "Assets\Scripts\Simulation\Production\ResearchProductionSlice.cs" `
  "Assets\Scripts\Simulation\Production\ResearchProductionScenarioFactory.cs" `
  "Assets\Scripts\Simulation\Production\ProductionIntegrationFacade.cs" `
  "/out:Temp\CodexProductionFacadeCompile.dll" `
  "/refout:Temp\CodexProductionFacadeCompile.ref.dll"
```

- Result: passed with exit code `0`.
- Re-ran existing production scenario smoke:

```text
production scenarios: 8 runs, passed=True
```

- Re-ran existing research-production scenario smoke:

```text
research production scenarios: 10 runs, totalRP=13, passed=True
```

- Ran new facade smoke:

```text
facade smoke passed=True, build=True, researchBuild=True, ticks=8, rpGenerated=6, diagnostics=no diagnostics
snapshot ticks=8/8 workers=13 rp=6 blocked=0 footprintAccess=0
```

## Cleanup performed

- Removed temporary Roslyn outputs:
  - `Temp\CodexProductionFacadeCompile.dll`
  - `Temp\CodexProductionFacadeCompile.ref.dll`
  - `Temp\CodexProductionFacadeCompile.pdb` if present
- No screenshots, throwaway logs, scratch files, or generated source outside the owned Production folder were retained.

## Risks

- The facade is intentionally an adapter, not live integration. The parent still needs to decide when and how to tick it from `TrenchworksSimulation`.
- Build commands currently validate and consume build costs through the existing first-slice `TryBuild`; they do not yet place live production sites for every buildable.
- Research-building commands support local prototype ids only:
  - `hand_study_desk`
  - `draughting_office`
  - `steam_analysis_bench`
  - `essence_observatory`
- Steam consumed is reported as an inventory delta placeholder because the current steam network produces pressure/steam but does not yet model steam drawdown as inventory consumption.
- Snapshot DTOs use simple classes rather than C# records for Unity/Roslyn compatibility.

## Memory-worthy notes

- The parent integration worker can now call `ProductionIntegrationFacade.CreatePrototype()`, `ApplyCommand(...)`, `Tick(...)`, and `CreateSnapshot()` without directly managing internal slice classes.
- `ProductionSubsystemSnapshot` is the recommended UI/tracker surface for early integration.
- `ProductionIntegrationFacade.RunDeterministicSmoke()` is the recommended narrow editor smoke entry point for the adapter layer.
- Production remains independent of Hubble's catalog, Cicero's war/team systems, and Descartes' research runtime.

## Next integration recommendation

Parent integration should add an edit-mode smoke around `ProductionIntegrationFacade.RunDeterministicSmoke()` first. After that, wire the facade into `TrenchworksSimulation` behind a compatibility flag or adapter field, then expose only `ProductionSubsystemSnapshot` data to the UI tracker before attempting interactive placement.
