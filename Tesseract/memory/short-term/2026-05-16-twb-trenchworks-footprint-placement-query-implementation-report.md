# 2026-05-16 TWB Trenchworks Footprint Placement Query Implementation Report

## Scope

Scope: standalone Unity 2D game, TWB Trenchworks grid/box prototype.

This pass stayed confined to Data/catalog helpers under:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\
```

No Production, War, live simulation, UI, editor setup, memory wiki, index, hot, or log files were edited.

## What changed

- Added catalog query/index helper:
  - `CatalogLookup`
- Added footprint placement helper types:
  - `FootprintRotation`
  - `FootprintPlacementIssueType`
  - `FootprintGridCell`
  - `FootprintOccupiedCell`
  - `FootprintPlacementRequest`
  - `FootprintPlacementIssue`
  - `FootprintPlacementResult`
  - `FootprintPlacementValidator`
  - `FootprintPlacementSamples`
- Added deterministic sample placement requests:
  - Valid shipping depot placement.
  - Cramped shipping depot failure with collision, bounds, and missing connector/access issues.

## Helper coverage

Catalog lookup coverage:

- Direct `TryGet` lookup for resources, items, recipes, machines, transports, teams, fortifications, and emplacements.
- Items by tier, category, and tag.
- Machines by tier, category, footprint size, worker access requirement, belt access requirement, and steam/underground pipe requirement.
- Machines consuming or producing an item via recipe indexes.
- Transports by tier, category, and layer.
- Recipes by machine, required input item, and produced output item.
- Teams by entry lane.
- Fortifications and emplacements by contact requirement.

Footprint placement coverage:

- Grid bounds checks.
- Surface placement collision checks.
- Movement-blocked worker access checks.
- Required connector checks for worker access, belt/loader access, and underground steam/pipe access.
- Optional required clearance cells.
- Transformed occupied placement cells and connector cells in placement results.
- Rotation support for 0, 90, 180, and 270 degrees.
- Mirroring support on X and Y axes before rotation.

Rotation/mirroring note:

- Rotation and mirroring were implemented now because the footprint model is pure data and the transform math is compact. Integration can choose whether the player is allowed to rotate or mirror particular buildables later.

## Files touched

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\CatalogLookup.cs
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\FootprintPlacement.cs
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-footprint-placement-query-implementation-report.md
```

## Tests/checks run

- Read required implementation plan:
  - `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-full-implementation-plan-and-wireframes.md`
- Read prior catalog foundation report:
  - `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-catalog-foundation-implementation-report.md`
- Read prior catalog validation/layout report:
  - `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-catalog-validation-layout-implementation-report.md`
- Inspected existing Data module:
  - `TrenchworksCatalog.cs`
  - `CatalogValidation.cs`
  - `PrototypeLayoutBlueprints.cs`
- Compiled with Unity's generated Roslyn response file plus all Data sources:
  - response file: `Library\Bee\artifacts\1900b0aE.dag\Assembly-CSharp.rsp`
  - compiler host: `C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Data\NetCoreRuntime\dotnet.exe`
  - compiler: `C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Data\DotNetSdkRoslyn\csc.dll`
  - result: passed
- Smoke invocation through PowerShell `Add-Type`:
  - Instantiated `TrenchworksCatalog.CreatePrototypeCatalog()`.
  - Built `CatalogLookup`.
  - Ran `CatalogValidator.Validate(catalog)`.
  - Instantiated and validated prototype blueprints.
  - Queried Tier 2 machines, steam machines, steam-producing recipes, and `worker_food` tagged items.
  - Ran valid footprint placement sample.
  - Ran invalid cramped footprint placement sample.

Smoke results:

- Catalog errors: 0
- Catalog warnings: 0
- Blueprint errors: 0
- Blueprint warnings: 0
- Tier 2 machines found: 2
- Steam machines found: 1
- Steam-producing recipes found: 1
- Worker-food tagged items found: 3
- Valid placement can place: true
- Valid placement issues: 0
- Invalid placement can place: false
- Invalid placement issues: 3
- Invalid first issue: `Collision: Footprint collides with sample.storage. at Surface 5,3`

## Cleanup performed

- Compiler check outputs were redirected to the system temp folder and removed after the check.
- No screenshots, throwaway logs, or project temp files were intentionally created.

## Risks

- Placement validation is intentionally data-only; it does not reserve cells, mutate grids, pathfind, or apply build costs.
- Connector semantics are strict by design. Integration workers should deliberately provide connector cells from belts, loaders, access lanes, and underground pipe networks.
- Underground steam placement currently does not block surface placement in this helper, matching the catalog layer intent. Integration should preserve that unless a future rule says otherwise.
- Sample grids are smoke fixtures and examples, not balance-approved starter layouts.

## Next integration recommendation

- Parent integration should create a `CatalogLookup` once per catalog and pass it to Production/UI systems instead of duplicating recipe and descriptor lookups.
- Production placement should use `FootprintPlacementValidator.Validate()` before accepting multi-cell machine or transport placement.
- UI should display `FootprintPlacementIssue` messages directly for blocked placement previews, then enrich copy later if needed.
