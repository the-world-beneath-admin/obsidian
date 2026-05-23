# 2026-05-16 TWB Trenchworks Catalog Validation Layout Implementation Report

## Scope

Scope: standalone Unity 2D game, TWB Trenchworks grid/box prototype.

This pass stayed confined to Data/catalog helpers under:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\
```

No Production, War, live simulation, UI, editor setup, memory wiki, index, hot, or log files were edited.

## What changed

- Added catalog validation helpers:
  - `CatalogValidationSeverity`
  - `CatalogValidationIssue`
  - `CatalogValidationResult`
  - `CatalogValidator`
- Added prototype layout blueprint helpers:
  - `LayoutPlacementKind`
  - `LayoutPlacementDescriptor`
  - `PrototypeLayoutBlueprint`
  - `PrototypeLayoutBlueprints`
- Added five prototype layout blueprints:
  - Tier 1 hand-work food block
  - Tier 2 conveyor workshop block
  - Boiler plus underground steam pipe block
  - Depot/loading block
  - Cramped footprint/routing pressure block
- Tightened the existing catalog so validation passes:
  - Added `item.fiber_reed`.
  - Added `item.stone_clay`.
  - Added explicit edge connector/access footprint cells for extractor, workshop, and storage descriptors.

## Validation coverage

Catalog validation checks:

- Unique ids inside each descriptor collection.
- Resource default item references.
- Recipe machine references.
- Recipe input/output item references.
- Recipe output presence and positive work seconds.
- Machine build-cost item references.
- Machine required node resource references.
- Machine recipe references and reverse recipe-machine consistency.
- Machine footprint access claims for belt, worker, and underground pipe access.
- Transport build-cost item references, footprint validity, throughput, and underground steam role consistency.
- Team leader reference, member references, leader included exactly once, one leader plus at least three sub-units, formation footprint, and supply item references.
- Fortification footprints, build costs, trench-connection requirements, and build-cost references.
- Emplacement footprints, build costs, supply needs, required crew unit reference, and trench-connection requirements.
- Footprint dimensions, non-empty cells, duplicate cells by layer, inside-bounds cells, and explicit one-cell edge connectors for access/pipe/belt style roles.

Blueprint validation checks:

- Blueprint id uniqueness.
- Surface and underground row counts and row widths.
- Placement bounds.
- Machine, transport, and resource placement references back to the catalog.

## Files touched

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\TrenchworksCatalog.cs
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\CatalogValidation.cs
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\PrototypeLayoutBlueprints.cs
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-catalog-validation-layout-implementation-report.md
```

## Tests/checks run

- Read required implementation plan:
  - `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-full-implementation-plan-and-wireframes.md`
- Read prior catalog implementation report:
  - `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-catalog-foundation-implementation-report.md`
- Read current catalog source:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\TrenchworksCatalog.cs`
- Compiled with Unity's generated Roslyn response file plus all Data sources:
  - response file: `Library\Bee\artifacts\1900b0aE.dag\Assembly-CSharp.rsp`
  - compiler host: `C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Data\NetCoreRuntime\dotnet.exe`
  - compiler: `C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Data\DotNetSdkRoslyn\csc.dll`
  - result: passed
- Smoke invocation through PowerShell `Add-Type`:
  - Instantiated `TrenchworksCatalog.CreatePrototypeCatalog()`.
  - Ran `CatalogValidator.Validate(catalog)`.
  - Instantiated `PrototypeLayoutBlueprints.CreatePrototypeBlueprints()`.
  - Ran `PrototypeLayoutBlueprints.ValidateBlueprints(catalog, blueprints)`.
  - Catalog errors: 0
  - Catalog warnings: 0
  - Blueprint errors: 0
  - Blueprint warnings: 0
  - Blueprint count: 5
  - Catalog item count after fixes: 24

## Cleanup performed

- Compiler check outputs were redirected to the system temp folder and removed after the check.
- No screenshots, throwaway logs, or project temp files were intentionally created.

## Risks

- Blueprint placements are intentionally lightweight seeds, not authoritative construction plans.
- Blueprint row strings are for quick visual/layout reference; integration should still use catalog descriptor footprints for placement rules.
- Edge connector semantics are validation-side conventions for now. Integration should decide whether edge connectors become formal placement ports or remain catalog metadata.
- Catalog quantities and build costs remain first-pass placeholders for dependency and layout pressure, not balance.

## Next integration recommendation

- Parent integration should run `CatalogValidator.Validate()` before using catalog content and fail fast on errors.
- Production integration should use machine and transport footprints as source of truth for placement bounds, collision, worker lanes, belt/loader ports, and underground steam connectivity.
- UI/integration workers can use prototype blueprints as seed layouts or smoke-test diagrams, but should not hard-code live behavior from the row strings.
