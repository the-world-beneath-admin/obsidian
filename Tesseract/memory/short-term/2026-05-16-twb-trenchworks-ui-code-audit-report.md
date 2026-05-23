# TWB Trenchworks UI Code Audit Report

Date: 2026-05-16
Worker: bounded TWB Trenchworks UI code-audit worker
Scope: Standalone TWB-tagged Unity 2D game under The World Beneath umbrella
Project inspected: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

## Summary

The current prototype has a functional IMGUI bottom rail, but it is still organized around low-level debug controls rather than player-meaningful build categories. The richer data/catalog layer already contains most of the future taxonomy: machines, transports, research buildings, research unlocks, teams, fortifications, emplacements, tiers, layers, and access flags. The implementation plan should therefore avoid a pure UI-only reshuffle that invents names disconnected from data.

Recommended direction: add a small category/tab layer to the bottom rail, then show category-specific actions. Keep the current simple `ToolType` placement path for the first pass, but label/group it through categories. In the next pass, bridge category entries to catalog IDs and facade commands where those commands already exist.

## Files Inspected

- `Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `Assets\Scripts\Simulation\IntegratedPrototypeSystems.cs`
- `Assets\Scripts\Data\TrenchworksCatalog.cs`
- `Assets\Scripts\Data\CatalogIntegrationContracts.cs`
- `Assets\Scripts\Data\CatalogLookup.cs`
- `Assets\Scripts\Data\ResearchCatalog.cs`
- `Assets\Scripts\Data\ResearchLookup.cs`
- `Assets\Scripts\Simulation\Production\ProductionIntegrationFacade.cs`
- `Assets\Scripts\Simulation\Research\ResearchIntegrationFacade.cs`
- `Assets\Scripts\Simulation\War\WarIntegrationFacade.cs`
- Memory orientation read-only:
  - `memory\hot.md`
  - `memory\index.md`
  - `memory\wiki\game-dev\project-hierarchy.md`
  - `memory\briefs\current-twb-trenchworks-task.md`
  - `memory\wiki\twb-trenchworks\overview.md`
  - `memory\wiki\twb-trenchworks\architecture.md`

No source files were edited.

## Current Constraints

1. The visible Unity UI is implemented in `PrototypeBootstrap.cs` with immediate-mode `OnGUI`.
2. `DrawBottomRail` currently chooses between `DrawFactoryBottomButtons` and `DrawWarBottomButtons`, then always draws pause/speed/reset system buttons.
3. The factory bottom row is flat:
   - `EXT`
   - `BELT`
   - `ASM`
   - `STORE`
   - `DEPOT`
   - `ERASE`
   - four directions
   - four assembler recipes
4. The war bottom row is also flat:
   - doctrine buttons
   - entry-lane buttons
   - team spawn buttons
   - war-layer buttons
5. Factory placement currently calls `simulation.Factory.PlaceEntity(x, y, selectedTool, selectedDirection, selectedRecipe)`.
6. The live factory placement model only supports `ToolType` values:
   - `Extractor`
   - `Belt`
   - `Assembler`
   - `Storage`
   - `ShippingDepot`
   - `Erase`
7. The current direct factory simulation does not yet place catalog machines or transports by catalog ID.
8. The integrated production facade does expose build commands:
   - `BuildProductionSite(string siteKind, int x, int y)`
   - `BuildResearchSite(string buildingKind, int x, int y)`
   But the facade uses prototype strings such as `basic_conveyor`, `draughting_office`, `hand_study_desk`, `steam_analysis_bench`, and `essence_observatory`, not the full catalog IDs.
9. The catalog layer is richer than the playable factory UI:
   - machines: extractor, mudbed farm, field kitchen, small boiler, workshop, conveyor workshop, sawmill, storage, shipping depot
   - transports: basic conveyor, loader, underground steam pipe, depot access lane
   - research buildings: drafting desk, field records office, prototype bench, survey/signals room, steam test lab, essence analysis cell
   - war entries: teams, fortifications, emplacements
10. Research is already clickable in the right tracker, but only Tier 1 quick lists are shown.
11. War team buttons already gate availability through `WarSnapshot.TeamAvailability`, which is useful and should be preserved.
12. Bottom rail height is fixed at `94f`. A category system with many controls risks overflow on narrower screens unless it uses two-stage selection or compact paging.
13. Current project guidance says this is still prototype/debug UI; do not overbuild a polished UI system before the loop is proven.

## Proposed Category Taxonomy

Use these as bottom-row categories, not necessarily all as always-visible action buttons.

### 1. Belts / Transport

Purpose: move goods through the factory and between buildings.

Initial entries:

- Basic belt: current `ToolType.Belt`
- Direction controls: up/right/down/left
- Loader: catalog `transport.loader`, future facade bridge
- Depot access lane: catalog `transport.depot_access_lane`, future facade bridge
- Underground steam pipe: catalog `transport.underground_steam_pipe`, future layer-aware bridge

Rationale: direction belongs with transport, not as a permanently exposed global cluster.

### 2. Machine Production

Purpose: core productive machinery that converts or processes inputs.

Initial entries:

- Extractor: current `ToolType.Extractor`
- Assembler: current `ToolType.Assembler`
- Workshop: catalog `machine.workshop`, future facade bridge
- Conveyor workshop: catalog `machine.conveyor_workshop`, future facade bridge

Rationale: this is where the player expects generic machines and line-building production.

### 3. Energy / Steam

Purpose: power, steam production, and steam routing.

Initial entries:

- Small boiler: catalog `machine.small_boiler`
- Underground steam pipe: catalog `transport.underground_steam_pipe`
- Steam test lab: research building `research_building.steam_test_lab`
- War-layer or factory-layer toggle may eventually live here for steam/underground views.

Rationale: steam is already a tier/layer/access concept in data but not a playable bottom-row category.

### 4. Base Material Production

Purpose: raw-to-basic-material chains and early survival logistics.

Initial entries:

- Extractor: current `ToolType.Extractor`
- Mudbed farm: catalog `machine.mudbed_farm`
- Sawmill: catalog `machine.sawmill`
- Field kitchen: catalog `machine.field_kitchen`
- Recipe shortcuts:
  - rations
  - trench materials
  - ammo
  - medical supplies

Rationale: the flat `ASM` plus recipe buttons hides the actual production fantasy. Early material chains should be legible as a category.

### 5. Assemblers / Processors

Purpose: choose processing recipe or production output for assembly-style machines.

Initial entries:

- Current assembler recipes:
  - ammo
  - trench materials
  - rations
  - medical supplies
- Workshop and conveyor workshop later, once catalog/facade build paths are unified.

Rationale: recipes should not consume permanent rail space unless the player is in a processing category or has selected an assembler.

### 6. Research

Purpose: research buildings and research purchases/focus.

Initial entries:

- Open/select right tracker Research mode
- Production focus
- War focus
- Drafting desk: catalog `research_building.drafting_desk`, facade equivalent likely `hand_study_desk`
- Field records office: catalog `research_building.field_records_office`, facade equivalent likely `draughting_office`
- Prototype bench, survey/signals room, steam test lab, essence analysis cell as future entries after mapping cleanup

Rationale: research is currently tucked into the right panel, while research-point production is in the integrated production facade. The player needs a rail category to build research infrastructure and inspect unlocks.

### 7. Logistics / Shipping

Purpose: storage, depot, supply export, and shipment diagnostics.

Initial entries:

- Storage: current `ToolType.Storage`
- Shipping depot: current `ToolType.ShippingDepot`
- Logistics tracker shortcut
- Supply category inspection:
  - ammo
  - trench materials
  - rations
  - medical supplies
- Future: porter/hauler diagnostics after facade/data path catches up.

Rationale: storage and depot are currently beside basic machines, but they are conceptually shipping/logistics endpoints.

### 8. War / Team Controls

Purpose: war view controls, doctrine, lane, teams, and war layers.

Initial entries:

- Toggle War/Build view
- Doctrine:
  - balanced
  - assault
  - entrench
  - bombardment
- Entry lane:
  - top
  - middle
  - bottom
- Team spawns:
  - scout
  - assault
  - engineer/fortify
  - supply/logistics
- Layer:
  - surface
  - tunnel
  - supply
  - all

Rationale: all existing war buttons fit here. The category name should make clear these are command controls, not hand-control of units.

### 9. Edit / System

Purpose: non-build utility controls.

Initial entries:

- Erase
- Pause/play
- Speed
- Reset

Rationale: erase is currently mixed with build tools. It is an editing mode and deserves separation to reduce accidental deletion.

## Recommended Bottom Rail Layout

Use a two-stage rail:

1. Left cluster: view/context toggle and category buttons.
2. Middle cluster: selected category actions.
3. Right cluster: persistent system controls.

Suggested first visible category buttons:

- Transport
- Machines
- Materials
- Process
- Research
- Logistics
- War
- Edit

When `showWarView` is true, default selected category should become `War`, but the player should still be able to access Research and Logistics. When `showWarView` is false, default selected category should become `Transport` or the last used factory category.

Do not show all category actions at once. The current 94px rail will not tolerate every future button unless the UI becomes a crowded parade of tiny biscuits.

## Exact Likely File Changes

### `Assets\Scripts\Unity\PrototypeBootstrap.cs`

Likely changes:

1. Add a new enum near `TrackerMode` and `WarLayer`:

```csharp
private enum BuildCategory
{
    Transport,
    Machines,
    Materials,
    Processors,
    Energy,
    Research,
    Logistics,
    War,
    Edit
}
```

2. Add state fields:

```csharp
private BuildCategory selectedBuildCategory = BuildCategory.Transport;
private BuildCategory lastFactoryCategory = BuildCategory.Transport;
```

Optionally add a selected catalog/build ID later:

```csharp
private string selectedCatalogBuildId;
private string selectedResearchBuildingId;
```

3. Replace `DrawFactoryBottomButtons` and `DrawWarBottomButtons` with category-aware methods:

- `DrawBottomCategoryButtons(Rect rail)`
- `DrawSelectedCategoryActions(Rect rail, BuildCategory category)`
- `DrawTransportActions(Rect rail, ref float x)`
- `DrawMachineActions(Rect rail, ref float x)`
- `DrawMaterialActions(Rect rail, ref float x)`
- `DrawProcessorActions(Rect rail, ref float x)`
- `DrawEnergyActions(Rect rail, ref float x)`
- `DrawResearchActions(Rect rail, ref float x)`
- `DrawLogisticsActions(Rect rail, ref float x)`
- `DrawWarActions(Rect rail, ref float x)`
- `DrawEditActions(Rect rail, ref float x)`

4. Preserve existing helper methods where possible:

- `DrawToolCircle`
- `DrawDirectionCircle`
- `DrawRecipeCircle`
- `DrawDoctrineCircle`
- `DrawEntryZoneCircle`
- `DrawWarTeamSpawnCircle`
- `DrawWarLayerCircle`
- `DrawTrackerCircle`
- `DrawCircleButton`

5. Re-home existing controls:

- `ToolType.Belt` and direction buttons -> Transport
- `ToolType.Extractor` and `ToolType.Assembler` -> Machines or Materials, depending on action naming
- recipe buttons -> Processors or Materials
- `ToolType.Storage` and `ToolType.ShippingDepot` -> Logistics
- `ToolType.Erase` -> Edit
- doctrine, lane, team spawn, and war layers -> War
- research tracker shortcut and research building commands -> Research

6. Add shortcut actions:

- Research category can set `trackerMode = TrackerMode.Research`.
- Logistics category can set `trackerMode = TrackerMode.Logistics`.
- War category can set `trackerMode = TrackerMode.War` and optionally `showWarView = true`.

7. Add optional facade build buttons for integrated prototype-only commands:

```csharp
simulation.Integrated.BuildProductionSite("basic_conveyor", x, y);
simulation.Integrated.BuildResearchSite("hand_study_desk", x, y);
simulation.Integrated.BuildResearchSite("draughting_office", x, y);
```

Do not wire these directly to map placement until their coordinate space and visible result are clear. They currently affect the integrated facade snapshot, not the visible factory map.

8. Add compact labels or hover/status text:

- Because circular buttons truncate badly, the selected category should be stated in the right tracker or small rail label.
- Avoid long labels inside 54px circles; use `TRN`, `MAC`, `MAT`, `PRC`, `STM`, `RES`, `LOG`, `WAR`, `EDT`.

### `Assets\Scripts\Simulation\TrenchworksSimulation.cs`

Likely changes after the first UI-only category pass:

1. Add a placement abstraction if catalog-backed build placement becomes real:

```csharp
public bool PlaceFactoryBuildCommand(int x, int y, FactoryBuildSelection selection)
```

2. Keep `PlaceEntity` for current enum-backed prototype tools.

3. Add a small mapping layer from UI action to current `ToolType` until catalog placement exists.

Risk: changing this too early would blur the working factory map with integrated facade-only data. Leave it alone for the first rail reorganization unless a build action genuinely needs simulation support.

### `Assets\Scripts\Data\CatalogIntegrationContracts.cs`

Likely future change:

1. Add UI grouping metadata only if the UI becomes data-driven:

```csharp
public enum BuildUiCategory
{
    Transport,
    MachineProduction,
    EnergySteam,
    BaseMaterials,
    Processors,
    Research,
    LogisticsShipping,
    WarTeamControls
}
```

2. Add mapping helpers from known catalog IDs to UI category.

Recommendation: do not add this yet unless `PrototypeBootstrap` starts consuming catalog descriptors directly. A local UI mapping table in `PrototypeBootstrap.cs` is smaller and safer for the next pass.

### `Assets\Scripts\Data\CatalogLookup.cs`

Likely future change:

Add convenience queries only if the UI becomes catalog-driven:

- `MachinesByUiCategory(...)`
- `TransportsByUiCategory(...)`
- `BuildablesByTierAndUnlockState(...)`

Current lookup already supports machines by category, transports by category/layer, machines requiring steam, and transport by layer. That is enough for a first category-backed UI.

### `Assets\Scripts\Data\ResearchLookup.cs`

Likely future change:

Add a helper to get unlock availability for UI action badges if needed. Current lookup already supports:

- nodes by domain/tier
- nodes unlocking target
- buildings by required research
- steam/worker/belt/essence building filters

### `Assets\Scripts\Simulation\IntegratedPrototypeSystems.cs`

Likely changes when rail buttons begin using facades:

1. Add explicit UI-facing build wrappers with stable names:

```csharp
public ProductionCommandResult BuildPrototypeConveyor(int x, int y)
public ProductionCommandResult BuildPrototypeResearchDesk(int x, int y)
```

2. Or add a mapper from catalog IDs to current facade site IDs:

```csharp
private static bool TryMapCatalogBuildIdToProductionFacadeKind(string catalogId, out string facadeKind)
```

3. Consider logging failed facade build attempts into `EventLog` with enough UI context.

### `Assets\Scripts\Simulation\Production\ProductionIntegrationFacade.cs`

Likely future changes:

1. Normalize facade build IDs against catalog IDs.
2. Replace prototype-only IDs like `basic_conveyor`, `draughting_office`, and `hand_study_desk` with constants or a mapping table.
3. Expose available buildables snapshot if the UI needs lock/availability state.

### `Assets\Scripts\Simulation\Research\ResearchIntegrationFacade.cs`

Likely future changes:

1. No immediate change required for bottom rail category reorganization.
2. Later, expose clearer availability summaries for category badges: available research count, blocked by RP count, completed count.

### `Assets\Scripts\Simulation\War\WarIntegrationFacade.cs`

Likely future changes:

1. No immediate change required.
2. Existing `TeamAvailability`, `EntryLanes`, and command diagnostics are already suitable for the War category.
3. Later, expose war action groups if fortifications/emplacements become placeable from the rail.

## Risks

1. Rail overflow: the current `BottomRailHeight = 94f` and circular button style cannot support every category and action at once.
2. Confusing dual factory systems: the visible `FactoryWorld` and integrated `ProductionIntegrationFacade` are separate enough that facade build commands may not visibly place things on the current factory map.
3. Catalog/facade ID mismatch: catalog IDs use strings such as `transport.basic_conveyor` and `research_building.drafting_desk`, while facade build requests currently use strings such as `basic_conveyor` and `hand_study_desk`.
4. Premature data-driven UI risk: moving all rail controls to catalog descriptors now would be attractive but wasteful unless visible placement uses the same IDs.
5. War availability must remain gated. Do not make team buttons look enabled when `WarSnapshot.TeamAvailability` says they are locked.
6. Research buttons are currently in the right tracker, not bottom rail. Moving all research into the bottom rail could crowd the primary build controls. Better: bottom rail opens/filters research; detailed purchases stay in the tracker until a proper panel exists.
7. Erase risk: keeping erase among build tools invites accidental clearing. It should move to Edit/System.
8. Naming risk: "Machine Production" and "Base Material Production" overlap. The UI should test labels quickly; if too muddy, use `Machines` and `Materials` in the rail, with longer names in status text.

## Small Implementation Sequence

1. UI-only category pass in `PrototypeBootstrap.cs`.
   - Add `BuildCategory`.
   - Add selected category state.
   - Add category buttons.
   - Move current existing buttons into category-specific action groups.
   - Do not change simulation behavior.

2. Preserve current functionality.
   - Confirm all existing actions still work:
     - place extractor, belt, assembler, storage, depot
     - erase
     - set direction
     - select assembler recipe
     - toggle war/build view
     - set doctrine
     - select entry lane
     - spawn available teams
     - switch war layers
     - pause/speed/reset

3. Add tracker shortcuts.
   - Research category sets/shows `TrackerMode.Research`.
   - Logistics category sets/shows `TrackerMode.Logistics`.
   - War category sets/shows `TrackerMode.War`.

4. Add minimal category status text.
   - Show selected category and selected action in the overview tracker or a small label on the rail.
   - Keep labels short inside circular controls.

5. Add optional facade-only research/production build actions only after the category UI is stable.
   - Use clear labels such as `DESK`, `OFFC`, `CONV`.
   - If they do not visibly affect the factory map, report through `EventLog` and tracker text rather than pretending they are map placements.

6. Second pass: catalog/facade mapping.
   - Add a small mapping table between catalog IDs and facade/current prototype actions.
   - Only then consider data-driven lists from `CatalogLookup` and `ResearchLookup`.

7. Verification.
   - Run Unity compile/import check if available for this project.
   - Run any existing smoke/check entry points if exposed in editor setup.
   - Manually Play Mode smoke:
     - factory view opens
     - category buttons switch action groups
     - original factory placement still works
     - war category still spawns/gates teams
     - research purchases still work in the tracker
     - no bottom rail overlap at a common desktop resolution

## Memory-Worthy Notes

- The bottom rail should become category-first, action-second.
- First pass should be UI-only and preserve the current `ToolType` placement path.
- Catalog data already supports the desired long-term taxonomy, but visible placement is not yet catalog-driven.
- The main blocker to a fully data-driven bottom rail is the mismatch between catalog IDs and current facade/prototype build IDs.
- Research and war controls should remain partly panel-driven; the bottom rail should route/trigger them, not contain every research node.

## Cleanup Performed

No temporary files, screenshots, logs, or source edits were created during this audit.
