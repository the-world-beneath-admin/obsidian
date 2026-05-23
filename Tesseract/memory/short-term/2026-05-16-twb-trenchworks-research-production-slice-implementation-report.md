# 2026-05-16 TWB Trenchworks Research Production Slice Implementation Report

## Scope

Standalone TWB-tagged game: TWB Trenchworks.

Active Unity project:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

This pass extended only the isolated Production module. It did not edit Data/catalog work, War/team work, `Simulation\Research`, `TrenchworksSimulation`, Unity bootstrap, editor setup, or permanent memory.

## What changed

- Added generic research-point production support inside `TWB.Trenchworks.Simulation.Production`.
- Added `ResearchPointLedger`:
  - available RP,
  - lifetime produced RP,
  - capacity,
  - spend/add/seed helpers.
- Added research-producing factory objects:
  - `ResearchProductionRecipe`
  - `ResearchProductionBuilding`
  - `ResearchProductionWorld`
- Research buildings now support:
  - multi-cell footprints,
  - worker access lane checks,
  - worker assignment/labour checks,
  - inventory inputs,
  - steam requirements through the existing `SteamNetwork`,
  - RP ledger output capacity checks,
  - consumed-input tracking for smoke reports.
- Extended shared production diagnostics with:
  - `OutputCapacity`
- Added deterministic research-production scenarios and smoke API:

```csharp
ResearchProductionScenarioFactory.RunDeterministicSmoke()
```

## Research buildings covered

- Hand Study Desk
  - Early hand-work research; consumes worker meals and planks.
- Draughting Office
  - Early office research; consumes worker meals, front rations, and planks.
- Steam Analysis Bench
  - Steam-powered research; consumes worker meals, steel plates, machine parts, and steam pipe parts, and requires underground steam connectivity.
- Essence Observatory
  - Essence-supported research; consumes worker meals, essence, and sandbags.

## Scenario coverage

The research smoke suite now runs 10 deterministic scenarios:

- `hand-study-desk-healthy`
- `draughting-office-healthy`
- `steam-analysis-bench-healthy`
- `essence-observatory-healthy`
- `no-worker-block`
- `no-food-materials-block`
- `essence-research-block`
- `steam-research-block`
- `output-capacity-block`
- `blocked-cramped-research-wing`

These cover healthy RP production and blockage from:

- no workers,
- no food,
- no materials,
- no essence,
- no steam,
- blocked access,
- cramped/overlapping footprints,
- insufficient RP output capacity.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Production\ProductionWorldSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Production\ProductionDiagnosticSummary.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Production\ResearchProductionSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Production\ResearchProductionScenarioFactory.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-research-production-slice-implementation-report.md`

## Checks run

- Read required context:
  - `memory\short-term\2026-05-16-twb-trenchworks-research-tree-design-report.md`
  - `memory\short-term\2026-05-16-twb-trenchworks-production-scenarios-validation-implementation-report.md`
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
  "/out:Temp\CodexResearchProductionCompile.dll" `
  "/refout:Temp\CodexResearchProductionCompile.ref.dll"
```

- Result: passed with exit code `0`.
- Ran pure C# research smoke:

```text
research production scenarios: 10 runs, totalRP=13, passed=True
hand-study-desk-healthy: ticks=7, rp=2, passed=True, diagnostics=no diagnostics
draughting-office-healthy: ticks=6, rp=2, passed=True, diagnostics=no diagnostics
steam-analysis-bench-healthy: ticks=8, rp=5, passed=True, diagnostics=no diagnostics
essence-observatory-healthy: ticks=6, rp=4, passed=True, diagnostics=no diagnostics
no-worker-block: ticks=2, rp=0, passed=True, diagnostics=MissingWorker=1
no-food-materials-block: ticks=4, rp=0, passed=True, diagnostics=MissingRecipeInput=1, WorkerHunger=2
essence-research-block: ticks=2, rp=0, passed=True, diagnostics=NoEssence=1
steam-research-block: ticks=2, rp=0, passed=True, diagnostics=NoSteam=2
output-capacity-block: ticks=3, rp=0, passed=True, diagnostics=OutputCapacity=1
blocked-cramped-research-wing: ticks=1, rp=0, passed=True, diagnostics=BlockedAccess=1, BlockedFootprint=1
```

- Re-ran prior production scenario smoke after the changes:

```text
production scenarios: 8 runs, passed=True
research production scenarios: 10 runs, totalRP=13, passed=True
```

## Cleanup performed

- Removed temporary Roslyn outputs:
  - `Temp\CodexResearchProductionCompile.dll`
  - `Temp\CodexResearchProductionCompile.ref.dll`
  - `Temp\CodexResearchProductionCompile.pdb` if present
- No screenshots, throwaway logs, scratch files, or generated source outside the owned Production folder were retained.

## Risks

- Research production is intentionally separate from `Simulation\Research`; spending RP on Production or War branches remains a parent/Descartes integration concern.
- Recipes are in-code prototypes and do not depend on Hubble's catalog work. Later integration should map these recipes to catalog ids rather than duplicating final definitions.
- Steam research uses the existing simple pressure/path model, not a full pressure allocation model.
- Output capacity is represented by the generic ledger capacity only. Later UI may want storage upgrades or a dedicated research archive building.

## Memory-worthy notes

- Generic RP can now be produced by grid buildings that consume real production inputs.
- Research production now competes with worker food, front rations, planks, steel plates, machine parts, steam pipe parts, essence, and factory space.
- The current smoke entry point for research production is `ResearchProductionScenarioFactory.RunDeterministicSmoke()`.
- Research-producing buildings do not unlock or spend research; they only create generic RP for later systems.

## Next integration recommendation

Parent integration should let Descartes own RP spending and tree state. Production should remain the RP source: expose `ResearchPointLedger.AvailableResearchPoints`, `LifetimeProducedResearchPoints`, consumed inputs, and diagnostics to future UI/tests, then let the research runtime decide how generic RP is spent.
