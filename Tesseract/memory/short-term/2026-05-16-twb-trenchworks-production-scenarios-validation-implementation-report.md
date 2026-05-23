# 2026-05-16 TWB Trenchworks Production Scenarios Validation Implementation Report

## Scope

Standalone TWB-tagged game: TWB Trenchworks.

Active Unity project:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

This pass extended only the isolated production module under `Assets\Scripts\Simulation\Production`. No live UI, `TrenchworksSimulation`, Data/catalog, War/team, Unity bootstrap, editor setup, or permanent memory files were edited.

## What changed

- Added deterministic production scenario blueprints and smoke-suite helpers:
  - `ProductionScenarioBlueprint`
  - `ProductionScenarioFactory`
  - `ProductionScenarioRunResult`
  - `ProductionScenarioSuiteResult`
- Added validation helpers:
  - `ProductionValidator`
  - `ProductionValidationResult`
  - `ProductionValidationIssue`
  - `ProductionValidationRule`
- Added diagnostic aggregation:
  - `ProductionDiagnosticSummary`
  - grouped stall reasons by diagnostic category,
  - validation-to-diagnostic category mapping for later tracker/UI surfaces.
- Extended `ProductionWorldSlice` with:
  - `NoWater` diagnostic category,
  - `NoCarrierCapacity` diagnostic category,
  - read-only access-lane exposure for validation,
  - steam node lookup/link/path helpers,
  - water-specific boiler and recipe diagnostics.
- Added boiler worker assignment in the deterministic healthy scenario so validation can report a clean baseline.

## Deterministic scenario coverage

The scenario factory now creates eight deterministic blueprints:

- `healthy-smoke`
  - Clean baseline for worker food, essence farm, boiler, underground pipes, and powered canning.
- `tier1-hand-food-block`
  - Workers have no meals/raw food buffer; produces worker hunger and missing input diagnostics.
- `boiler-pipe-block`
  - Powered machine has no underground steam-pipe path to a boiler; produces no-steam diagnostics and validation errors.
- `water-starved-boiler`
  - Boiler has coal but no water; produces no-water and no-steam diagnostics.
- `essence-farm-block`
  - Mudbed farm has loam, water, and labour but no essence; produces no-essence diagnostics.
- `construction-material-shortage`
  - Conveyor build attempted without conveyor parts; produces missing construction goods diagnostic.
- `blocked-access-transport`
  - Site has no access lane and no porter/conveyor transport fallback; produces blocked-access and no-carrier-capacity diagnostics.
- `cramped-footprint-routing`
  - Overlapping footprint attempt proves cramped routing/footprint pressure diagnostics.

## Validation coverage

`ProductionValidator.Validate(world)` now checks:

- world bounds,
- access lane presence and bounds,
- site footprint bounds,
- overlapping footprints,
- site-to-access-lane adjacency,
- worker role counts and assignments,
- worker/front food buffers,
- coal demand,
- water demand,
- essence demand,
- steam node bounds,
- steam links to existing nodes,
- machine-to-boiler underground steam paths,
- required build cost definitions,
- build-cost material validity,
- transport fallback through porters or conveyor parts.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Production\ProductionWorldSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Production\ProductionDiagnosticSummary.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Production\ProductionValidator.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Production\ProductionScenarioFactory.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-production-scenarios-validation-implementation-report.md`

## Checks run

- Read required context:
  - `memory\short-term\2026-05-16-twb-trenchworks-full-implementation-plan-and-wireframes.md`
  - `memory\short-term\2026-05-16-twb-trenchworks-production-first-slice-implementation-report.md`
  - existing production module under `Assets\Scripts\Simulation\Production`
- Compiled with Unity Roslyn using the available response file plus production sources:

```powershell
dotnet exec "C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Data\DotNetSdkRoslyn\csc.dll" `
  "@Library\Bee\artifacts\1900b0aE.dag\Assembly-CSharp.rsp" `
  "Assets\Scripts\Simulation\Production\ProductionWorldSlice.cs" `
  "Assets\Scripts\Simulation\Production\ProductionDiagnosticSummary.cs" `
  "Assets\Scripts\Simulation\Production\ProductionValidator.cs" `
  "Assets\Scripts\Simulation\Production\ProductionScenarioFactory.cs" `
  "/out:Temp\CodexProductionValidationCompile.dll" `
  "/refout:Temp\CodexProductionValidationCompile.ref.dll"
```

- Result: passed with exit code `0`.
- Ran pure C# deterministic smoke invocation:

```powershell
[TWB.Trenchworks.Simulation.Production.ProductionScenarioFactory]::RunDeterministicSmoke()
```

- Result summary:

```text
production scenarios: 8 runs, passed=True
healthy-smoke: ticks=12, passed=True, validation=valid, diagnostics=no diagnostics
tier1-hand-food-block: ticks=4, passed=True, validation=0 errors, 1 warnings, diagnostics=MissingRecipeInput=1, WorkerHunger=2
boiler-pipe-block: ticks=1, passed=True, validation=2 errors, 0 warnings, diagnostics=NoSteam=4
water-starved-boiler: ticks=1, passed=True, validation=0 errors, 1 warnings, diagnostics=NoSteam=2, NoWater=4
essence-farm-block: ticks=1, passed=True, validation=0 errors, 1 warnings, diagnostics=NoEssence=2
construction-material-shortage: ticks=0, passed=True, validation=valid, diagnostics=MissingConstructionGoods=1
blocked-access-transport: ticks=1, passed=True, validation=2 errors, 2 warnings, diagnostics=BlockedAccess=3, NoCarrierCapacity=1, WorkerHunger=1
cramped-footprint-routing: ticks=0, passed=True, validation=0 errors, 2 warnings, diagnostics=BlockedFootprint=1, NoCarrierCapacity=1, WorkerHunger=1
```

## Cleanup performed

- Removed temporary Roslyn outputs:
  - `Temp\CodexProductionValidationCompile.dll`
  - `Temp\CodexProductionValidationCompile.ref.dll`
  - `Temp\CodexProductionValidationCompile.pdb` if present
- No screenshots, throwaway logs, scratch files, or generated source outside the owned Production folder were retained.

## Risks

- The helpers are still pure C# and isolated. They are ready for edit-mode tests or parent integration, but not yet surfaced in the UI.
- Scenario validation intentionally reports errors for blocked scenarios. The smoke-suite expectation logic treats those as passing only when the blueprint declares them intentional.
- Diagnostic counts include both runtime diagnostics and validation-derived categories where useful for UI aggregation. Integration should decide whether to show these together or in separate panels.
- Transport capacity is still abstract: porters and conveyor parts stand in for a future real route/carry system.

## Memory-worthy notes

- Production now has deterministic scenario coverage for food, coal, water, essence, steam pathing, construction materials, access lanes, transport capacity, and cramped footprint pressure.
- `ProductionScenarioFactory.RunDeterministicSmoke()` is the recommended future editor smoke-test entry point for this isolated slice.
- `ProductionValidator.Validate(world)` can be used by future UI/integration code before placing buildings or loading scenarios.
- `ProductionDiagnosticSummary` gives tracker-ready bottleneck categories without needing to parse diagnostic strings.

## Next integration recommendation

Parent integration should add Unity edit-mode tests around `ProductionScenarioFactory.RunDeterministicSmoke()` before wiring the slice into live UI or `TrenchworksSimulation`. After Hubble's catalog work returns, map catalog ids to the current `ProductionItemIds` constants rather than replacing this slice wholesale.
