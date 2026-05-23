# TWB Trenchworks Research Catalog Data Implementation Report

Date: 2026-05-16
Worker: Hubble
Scope: The World Beneath / TWB Trenchworks standalone Unity 2D prototype

## What Changed

- Added compile-safe research catalog validation helpers for the Data/catalog lane.
- Added query/index helpers for research nodes and research-producing buildings.
- Kept all work data-only; no live simulation, UI, Production, War, or Research runtime integration was touched.

## Files Changed

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\ResearchValidation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\ResearchLookup.cs`

## Validation Coverage

`ResearchValidator` now checks:

- Research catalog and base Trenchworks catalog null safety.
- Unique research node ids and research building ids.
- Research node costs, display-name warnings, unlock presence, and unlock target ids.
- Research prerequisite ids exist.
- Recommended support ids reference either a research node or research building.
- Catalog unlock references exist for items, machines, transports, teams, fortifications, emplacements, and units.
- Placeholder, system, and next-tier unlock ids are allowed as intentional prototype/future references.
- Production and War each contain Tier 1, Tier 2, and Tier 3.
- Each domain/tier pair has exactly one capstone.
- Tier 1 and Tier 2 capstones unlock the expected next-tier marker.
- Research prerequisite cycles are rejected.
- Research building footprints are non-empty, dimensionally valid, and use valid inside cells or explicit edge connectors.
- Research building build costs and cycle inputs reference catalog items and use positive quantities.
- Research building cycle seconds and research points per cycle are positive.
- Research building required research ids exist.
- Research building access flags match footprint roles for worker, belt/loader, steam/underground pipe, and essence access.

`ResearchLookup` now supports:

- Lookup by research node id and research building id.
- Query research nodes by domain, tier, domain plus tier, prerequisite, unlock target, and capstone.
- Query research buildings by tier, required research id, steam/underground access, worker access, belt access, essence access, and consumed input item.

## Checks Run

- Unity Roslyn response-file compile using:
  - `Library\Bee\artifacts\1900b0aE.dag\Assembly-CSharp.rsp`
  - Data files only, including the new research files.
  - Result: passed.
- PowerShell smoke invocation:
  - Instantiated `TrenchworksCatalog.CreatePrototypeCatalog()`.
  - Instantiated `ResearchCatalog.CreatePrototypeResearchCatalog()`.
  - Ran `CatalogValidator.Validate(...)`.
  - Ran `PrototypeLayoutBlueprints.ValidateBlueprints(...)`.
  - Ran `ResearchValidator.Validate(...)`.
  - Built `ResearchLookup`.
  - Confirmed Production and War both expose Tier 1, Tier 2, Tier 3 and one capstone per tier.
  - Result: passed.

Smoke output:

```text
catalog_errors=0; catalog_warnings=0
blueprint_errors=0; blueprint_warnings=0
research_errors=0; research_warnings=0
research_nodes=44; research_buildings=6; capstones=6
prod_t3_nodes=7; war_t3_nodes=8
```

## Cleanup

- Removed temporary Roslyn output assemblies/PDBs from `%TEMP%` after compile.
- No scratch files, generated screenshots, or throwaway logs were created.

## Risks

- Research descriptors are still in-code prototype data, not ScriptableObjects or external balance sheets.
- Several future-facing unlocks intentionally remain `Placeholder` or `System` targets because the referenced simulation/UI features do not exist yet.
- Research buildings have footprints and costs, but are not integrated into placement UI, production runtime, or research runtime yet.

## Next Integration Recommendation

- Parent integration should wire `ResearchCatalog.CreatePrototypeResearchCatalog()`, `ResearchValidator`, and `ResearchLookup` into a single catalog smoke/bootstrap path before Descartes' runtime work consumes the data.
- Keep placeholder unlocks visible in debug tooling so future integration workers can distinguish deliberate future hooks from missing catalog references.
