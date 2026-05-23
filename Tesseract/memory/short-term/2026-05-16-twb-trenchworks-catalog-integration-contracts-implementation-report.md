# TWB Trenchworks Catalog Integration Contracts Implementation Report

Date: 2026-05-16
Worker: Hubble
Scope: The World Beneath / TWB Trenchworks standalone Unity 2D prototype

## What Changed

- Added Data-side integration contracts for stable catalog/research ids.
- Added a prototype integration manifest that maps Data ids to future Production, War, and Research integration concepts.
- Added contract validation so parent integration can verify stable ids before wiring facades/runtime systems.
- Added compact mapping DTOs and helpers for machine build contracts, war team templates, research buildings, and research unlocks.
- No live simulation, UI, Production, War, or Research runtime code was touched.

## Files Changed

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\CatalogIntegrationContracts.cs`

## Helper Coverage

`CatalogIds` now groups stable ids for:

- Tags
- Resources
- Items
- Machines
- Transports
- Units
- Teams
- Fortifications
- Emplacements
- Research capstones and next-tier unlock ids
- Research buildings
- System unlock ids
- Layer ids

`CatalogIntegrationManifest` now exposes:

- Production mappings for first-slice resources, construction goods, machines, transports, steam, storage, and depot concepts.
- War mappings for team templates, fortifications, emplacements, and legacy supply crate concepts.
- Research mappings for capstones, research buildings, and next-tier unlock ids.
- First-slice id list.
- Capstone id list.
- Compact `CatalogIntegrationSummary` with counts and missing mapping/id lists.

`CatalogIntegrationMapper` now exposes:

- Machine id to `MachineBuildContract` with build costs, footprint size, access flags, and recipe ids.
- Team id to `TeamTemplateContract` with leader, members, lane use, supplies, and default order.
- Research building id to `ResearchBuildingContract` with footprint size, build costs, inputs, RP cycle data, and access flags.
- Research node id to unlock contract summaries.

`CatalogIntegrationContractValidator` now checks:

- Manifest required mappings point at existing catalog, research, known system, known layer, or known research unlock ids.
- First-slice ids exist in the catalog/research data or known contract id sets.
- Capstone ids exist and are marked as capstones.
- Tier 1 and Tier 2 capstones expose the expected next-tier unlock ids.

## Checks Run

- Unity Roslyn response-file compile using:
  - `Library\Bee\artifacts\1900b0aE.dag\Assembly-CSharp.rsp`
  - Data files only, including `CatalogIntegrationContracts.cs`.
  - Result: passed.
- PowerShell smoke invocation:
  - Instantiated `TrenchworksCatalog.CreatePrototypeCatalog()`.
  - Instantiated `ResearchCatalog.CreatePrototypeResearchCatalog()`.
  - Ran `CatalogValidator.Validate(...)`.
  - Ran `PrototypeLayoutBlueprints.ValidateBlueprints(...)`.
  - Ran `ResearchValidator.Validate(...)`.
  - Built `CatalogIntegrationManifest.CreatePrototypeManifest()`.
  - Ran `CatalogIntegrationContractValidator.Validate(...)`.
  - Built manifest summary and confirmed zero missing required mappings and zero missing first-slice ids.
  - Resolved sample machine, team, research building, and research unlock contracts.
  - Result: passed.

Smoke output:

```text
catalog_errors=0; blueprint_errors=0; research_errors=0; integration_errors=0
manifest_mappings=58; first_slice_ids=69; capstones=6
missing_required_mappings=0; missing_first_slice_ids=0; ready=True
machine_contract=machine.shipping_depot:3x3; team_contract=team.scout_patrol:4; research_building_contract=research_building.steam_test_lab:4x3; unlock_contracts=1
```

## Cleanup

- Temporary Roslyn output assemblies/PDBs were removed from `%TEMP%`.
- No scratch files, generated screenshots, or throwaway logs were created.

## Risks

- Integration concepts are intentionally string-only contracts; they do not bind directly to Ptolemy, Cicero, or Descartes runtime classes yet.
- Placeholder/future research unlocks remain permitted where the catalog deliberately points beyond the current prototype slice.
- `CatalogIds` should be treated as the stable public contract. Future id renames should be migration decisions, not casual string edits.

## Next Integration Recommendation

- Parent integration should run the catalog, blueprint, research, and integration contract validators together in one bootstrap/smoke path.
- Production, War, and Research adapters should consume `CatalogIds`, `CatalogIntegrationManifest`, and `CatalogIntegrationMapper` rather than embedding raw strings.
- Add adapter-level tests that assert each facade concept resolves through the manifest before any live runtime state is mutated.
