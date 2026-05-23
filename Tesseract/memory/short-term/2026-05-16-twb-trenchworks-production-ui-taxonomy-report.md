# 2026-05-16 TWB Trenchworks Production UI Taxonomy Report

## Scope

Standalone TWB-tagged game: **TWB Trenchworks**.

Active Unity project inspected:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

This worker mapped the planned production, crafting, research, transport, steam, and logistics system into UI build categories and subcategories for a modern factory-builder style interface. No Unity source files were edited. No permanent memory files were edited.

## Source docs inspected

Project orientation:

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md`

Recent Trenchworks reports:

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-crafting-logistics-design-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-factory-construction-materials-addendum.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-worker-food-coal-essence-addendum.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-production-military-system-consolidated-design.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-catalog-foundation-implementation-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-production-first-slice-implementation-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-research-tree-design-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-research-catalog-data-implementation-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-production-integration-facade-implementation-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-live-integration-pass-report.md`

Current catalog/data/runtime scripts inspected:

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\TrenchworksCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\ResearchCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\ResearchLookup.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\ResearchValidation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Production\ProductionWorldSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Production\ProductionIntegrationFacade.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Research\ResearchTreeFactory.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\IntegratedPrototypeSystems.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`

## Taxonomy principle

Use two related UI axes:

- Build menu axis: things the player places or commands: materials, transport, machines, steam, assemblers, research, logistics, overlays.
- Supply/tracker axis: what the factory produces and allocates: worker food, front food, factory construction, trench construction, reserve crafting, research, command, bombardment.

Pushback: do not make the build menu directly mirror every war-supply bucket. Players place machines, belts, pipes, depots, and labs; they track ammo, rations, steam, research, and shortages elsewhere. A build bar that contains "Food", "Ammunition", "Medical", "Command", and "Bombardment" as primary tabs will quickly become a muddy ledger instead of a factory-builder interface.

## Recommended build categories

| Category | Button label | Short | Icon cue | Purpose |
|---|---|---:|---|---|
| Base Materials | Materials | MAT | resource node / ore chunk | Raw nodes, extractors, first material processors, basic conversion chains. |
| Conveyors / Transport | Transport | MOV | belt arrow | Belts, loaders, depot lanes, carts, later bulk freight. |
| Machines / Processors | Machines | MAC | gear | Farms, kitchens, sawmills, workshops, presses, canners, mills, vats. |
| Energy / Steam / Underground Pipes | Steam | STM | pressure gauge / pipe | Boilers, underground steam pipes, steam ports, pressure layer, powered machine routing. |
| Assemblers | Assembly | ASM | wrench plus box | Build-kit makers, conveyor workshop, machine shop, boiler workshop, pipe workshop, conduit bench. |
| Research Buildings | Research | RES | drafting compass / flask | Drafting Desk, records office, prototype bench, steam lab, essence lab. |
| Logistics / Storage / Shipping | Logistics | LOG | crate / depot | Storage, shipping depot, allocation controls, front/reserve/factory routing. |
| Overlays / Layers | Layers | LYR | stacked layers | Surface, underground steam, access lanes, ports, shortages, supply routes, contact/trench eligibility. |

### Category order

Bottom build bar order should be:

```text
MAT | MOV | MAC | STM | ASM | RES | LOG | LYR
```

This is deliberately not alphabetical. It follows the player's mental flow: get materials, move them, process them, power them, assemble advanced parts, research, ship, inspect.

## Detailed categories and subcategories

### 1. Base Materials

Button label: `Materials`
Short name: `MAT`
Icon cue: ore/resource node.

Subcategories:

- `Nodes`: Fungal Loam, Coal Seam, Water Spring, Essence Seep, Timber Stand, Heavy Scrap, Fiber Reed, Stone Clay.
- `Extract`: Extractor, Essence Tap, Coal Yard placeholder.
- `Basic Goods`: Raw Food, Timber, Heavy Scrap, Fiber, Stone Clay, Water, Essence, Coal.
- `Trench Basics`: Planks, Sandbags.
- `Metal Basics`: Steel Plate.

Current catalog/data support:

- Resources exist for `resource.fungal_loam`, `resource.coal`, `resource.water`, `resource.essence`, `resource.timber`, `resource.heavy_scrap`, `resource.fiber_reed`, `resource.stone_clay`.
- Items exist for raw food, worker meal, front rations, planks, sandbags, steel plate, machine part, conveyor part, boiler part, steam pipe part.
- Recipes exist for raw food, worker meals, front rations, steam, planks, steel plate, machine parts, conveyor parts, and sandbags.

Recommended buttons now:

| Label | Short | Icon cue | Gating |
|---|---:|---|---|
| Extractor | EXT | pick / drill | T1 visible immediately or after Worker Muster Rolls. |
| Mudbed Farm | FARM | sprout / trough | `prod.t1.mudbed_agronomy`. |
| Sawmill | SAW | saw blade | `prod.t1.timber_and_sand`. |
| Sandbags | BAG | stacked bags | `prod.t1.timber_and_sand`. |
| Scrap Press | PRESS | press / plate | `prod.t1.scrap_pressing`. |

### 2. Conveyors / Transport

Button label: `Transport`
Short name: `MOV`
Icon cue: belt arrow.

Subcategories:

- `Manual`: Depot Access Lane, porter route marker, worker access lane.
- `Belt`: Basic Conveyor.
- `Transfer`: Loader.
- `Depot Interface`: Storage access, shipping depot ports.
- `Steam Local`: Steam Cart placeholder.
- `Bulk`: Bulk Hauler Dock, Cable-Haul Skid, Crawl-Hauler, Overhead Chainway placeholders.
- `Late Sealed`: Pneumatic Vault Tube and Aether-Lift Gantry placeholders.

Current catalog/data support:

- `transport.depot_access_lane` exists as Tier 1 manual access.
- `transport.basic_conveyor` exists as Tier 2 belted transport.
- `transport.loader` exists as Tier 2 transfer.
- `transport.underground_steam_pipe` exists, but belongs visually under Steam rather than ordinary transport.

Recommended buttons now:

| Label | Short | Icon cue | Gating |
|---|---:|---|---|
| Access Lane | LANE | walking path | `prod.t1.manual_haulage`. |
| Basic Belt | BELT | arrow belt | `prod.t2.basic_conveyors`. |
| Loader | LOAD | grabber arm | `prod.t2.loaders_storage`. |
| Bulk Dock | BULK | cargo hook | Placeholder after `prod.t3.bulk_handling_studies`; hide until system exists. |

### 3. Machines / Processors

Button label: `Machines`
Short name: `MAC`
Icon cue: gear.

Subcategories:

- `Food`: Mudbed Farm, Field Kitchen, Ration Canner.
- `Wood / Trench`: Sawmill, Sandbag Station, future Wire Twister.
- `Metal`: Workshop, Metal Press, future Steel Yard.
- `Steam Users`: Ration Canner, powered press, chemical vat placeholders.
- `Essence`: Essence Tap, future Aether Condenser, Warded Storage.
- `War Goods`: ammo crate, trench material crate, medical crate legacy compatibility chains.

Current catalog/data support:

- `machine.extractor`
- `machine.mudbed_farm`
- `machine.field_kitchen`
- `machine.small_boiler`
- `machine.workshop`
- `machine.conveyor_workshop`
- `machine.sawmill`
- `machine.storage`
- `machine.shipping_depot`

Recommended buttons now:

| Label | Short | Icon cue | Gating |
|---|---:|---|---|
| Field Kitchen | KIT | pot / ladle | `prod.t1.field_kitchens`. |
| Workshop | SHOP | gear | `prod.t1.scrap_pressing` or `prod.t2.machine_parts`, depending on whether build costs are enforced. |
| Sawmill | SAW | saw | `prod.t1.timber_and_sand`. |
| Ration Canner | CAN | can / press | `prod.t2.ration_canning`; currently production slice supports canner as a first-slice site, catalog has it as placeholder. |
| Small Boiler | BOIL | gauge | Show under Steam category, not here, though it is a machine internally. |

### 4. Energy / Steam / Underground Pipes

Button label: `Steam`
Short name: `STM`
Icon cue: pressure gauge / pipe.

Subcategories:

- `Fuel`: Coal, coal handling, coal yard placeholder.
- `Boilers`: Small Boiler, future Steam Engine House.
- `Underground Pipes`: Underground Steam Pipe, junction, valve, gauge placeholders.
- `Powered Machines`: steam requirement indicators, powered conveyor drives, powered loaders.
- `Steam Diagnostics`: pressure, disconnected machines, leaks placeholder, low coal/water warnings.
- `Magic Energy`: Essence conduit parts should be nearby but not mixed into steam routing; put Essence under Machines or a later `Essence` subtab if it grows.

Current catalog/data support:

- `machine.small_boiler` exists.
- `transport.underground_steam_pipe` exists.
- `item.steam`, `item.boiler_part`, and `item.steam_pipe_part` exist.
- Production first slice has a simple underground steam network and diagnostics for no coal, no water, no steam, low steam pressure, disconnected/blocked access.

Recommended buttons now:

| Label | Short | Icon cue | Gating |
|---|---:|---|---|
| Small Boiler | BOIL | gauge | `prod.t3.coal_boilers`. |
| Steam Pipe | PIPE | underground pipe | `prod.t3.underground_steam`. |
| Steam Layer | LYR | layers | Available as overlay once `prod.t3.underground_steam` is visible. |
| Powered Machine View | PWR | plug/gauge | `prod.t3.steam_machines`; overlay first, buildables later. |

### 5. Assemblers

Button label: `Assembly`
Short name: `ASM`
Icon cue: wrench plus box.

Subcategories:

- `Machine Kits`: Machine Parts, Boiler Parts, Factory Foundations, Hand Tools.
- `Transport Kits`: Conveyor Parts, Steam Pipe Parts, future rollers/gears/loader arms.
- `Steam Kits`: Boiler Part, Steam Pipe Part.
- `Essence Kits`: Essence Conduit Parts, future Ward Plates, Stabilizers.
- `War Assembly`: future ammo, medical, shell, command, and bombardment kit assemblers.

Current runtime support:

- Production slice tracks Machine Parts, Conveyor Parts, Boiler Parts, Underground Steam Pipe Parts, Essence Conduit Parts, Factory Foundations, Hand Tools, Wire Coils, Aether Charge.
- Catalog currently has Machine Part, Conveyor Part, Boiler Part, Steam Pipe Part; Essence Conduit Parts and some construction goods exist in production slice but not fully in the catalog item list yet.

Recommended buttons now:

| Label | Short | Icon cue | Gating |
|---|---:|---|---|
| Conveyor Workshop | BELT KIT | belt + wrench | `prod.t2.basic_conveyors`. |
| Machine Shop | PARTS | gear + box | `prod.t2.machine_parts`. |
| Boiler Workshop | BOILER KIT | gauge + wrench | `prod.t3.steel_yard`. |
| Pipe Workshop | PIPE KIT | pipe + wrench | `prod.t3.steel_yard` and `prod.t3.underground_steam`. |
| Conduit Bench | CONDUIT | spark + wire | Future Essence/magic infra; hide or debug-only until catalog catches up. |

### 6. Research Buildings

Button label: `Research`
Short name: `RES`
Icon cue: drafting compass / flask.

Subcategories:

- `Tier 1`: Drafting Desk, Field Records Office.
- `Tier 2`: Prototype Bench, Survey/Signals Room.
- `Tier 3`: Steam Test Lab, Essence Analysis Cell.
- `Research Tree`: Production branch, War branch, capstones, locked items.

Current catalog/data support:

- Research catalog has 44 nodes and 6 research buildings.
- Research buildings: Drafting Desk, Field Records Office, Prototype Bench, Survey/Signals Room, Steam Test Lab, Essence Analysis Cell.
- Live integration exposes Tier 1 production and war research purchase buttons in the right-side tracker.

Recommended buttons now:

| Label | Short | Icon cue | Gating |
|---|---:|---|---|
| Drafting Desk | DESK | drafting compass | `prod.t1.worker_muster`. Can be placeable now if placement UI is extended. |
| Records Office | REC | ledger | `war.t1.entry_lanes`. |
| Prototype Bench | PROTO | wrench/flask | `prod.t2.machine_parts`. |
| Signals Room | SIG | antenna/flag | `war.t2.observers`. |
| Steam Test Lab | ST LAB | gauge/flask | `prod.t3.underground_steam`. |
| Essence Cell | ESS LAB | crystal/flask | `prod.t3.steam_machines` per current data; consider changing later to an essence-specific prerequisite. |

### 7. Logistics / Storage / Shipping

Button label: `Logistics`
Short name: `LOG`
Icon cue: crate / depot.

Subcategories:

- `Storage`: Storage.
- `Shipping`: Shipping Depot.
- `Allocation`: Front / Reserve / Factory, worker/front/reserve food split.
- `War Supply`: Ammo, Front Rations, Trench Materials, Medical, later Command, Energy, Shells.
- `Factory Supply`: Steel Plate, Machine Part, Conveyor Part, Boiler Part, Steam Pipe Part, Essence Conduit Part, Foundations.
- `Requests`: blocked builds, front shortages, idle machines, route warnings.

Current catalog/data support:

- `machine.storage` and `machine.shipping_depot` exist.
- Live integration exposes production diagnostics in `LOGI` and integration event log in `LOG`.
- Production first slice has worker/front food split and build-cost failure diagnostics.

Recommended buttons now:

| Label | Short | Icon cue | Gating |
|---|---:|---|---|
| Storage | STORE | crate | `prod.t1.timber_and_sand` or visible from start. |
| Shipping Depot | DEPOT | depot crate | T1 visible; current catalog has it. |
| Allocate | SPLIT | three-way fork | `prod.t1.capstone` for Front / Reserve / Factory. Food split can appear earlier after `prod.t1.field_kitchens`. |
| Request Tracker | REQ | warning list | Always visible as diagnostics, not necessarily a placeable. |

### 8. Overlays / Layers

Button label: `Layers`
Short name: `LYR`
Icon cue: stacked layers.

Subcategories:

- `Surface Grid`: body cells, blocked cells, machine footprints.
- `Access`: worker access lanes, porters, depot lanes.
- `Belt`: belt paths, loader ports, blocked outputs.
- `Underground Steam`: pipes, boiler output, pressure, disconnected machines.
- `Essence`: essence taps, conduit/ward placeholders, instability later.
- `Logistics`: front/reserve/factory allocation, shipping routes, storage saturation.
- `Research`: locked/unlocked buildables by research prerequisite.
- `War`: contacts, supply routes, fortification eligibility, trench network, team positions.

Current support:

- Catalog footprints already encode body cells, worker access, belt access, loader ports, steam ports, underground pipe cells, depot bays, entry lane markers, crew access, firing arcs, and trench connections.
- Live integration renders team members, contacts, and trench-network plans.
- Production slice can explain blocked footprint/access, no steam, missing construction goods, and missing recipe input.

Recommended buttons now:

| Label | Short | Icon cue | Gating |
|---|---:|---|---|
| Access | ACCESS | walking path | Available once access lanes matter. |
| Belts | BELTS | belt arrow | `prod.t2.basic_conveyors`. |
| Steam | STEAM | pipe/gauge | `prod.t3.underground_steam`. |
| Shortages | WARN | warning triangle | Always visible. |
| Research Locks | LOCKS | lock | Visible once Research UI is exposed. |
| War Supply | FRONT | flag/crate | Visible in War view. |

## Tier gating suggestions

### Tier 1: Hand War Economy

Show:

- Materials: Extractor, Mudbed Farm, Field Kitchen, Sawmill, Workshop, Storage, Shipping Depot.
- Transport: Access Lane / Depot Access Lane only.
- Logistics: Worker Food / Front Food split after Field Kitchens.
- Research: Drafting Desk and Field Records Office when their research prerequisites are met.
- Overlays: resource nodes, access lanes, blocked builds, worker hunger, missing inputs.

Hide or lock:

- Conveyors, loaders, steam pipes, powered machines, bulk transport.

Recommended first player-facing unlock order:

```text
Worker Muster Rolls
  -> Mudbed Agronomy
  -> Field Kitchens
  -> Porter Haulage
  -> Timber and Sandbag Works
  -> Scrap Sorting and Crude Pressing
  -> Quartermaster Workshop Charter
```

### Tier 2: Belted Workshop Line

Show:

- Transport: Basic Belt, Loader.
- Machines: Conveyor Workshop, expanded Workshop, Ration Canner if catalog/UI supports it.
- Assembly: Conveyor Parts, Machine Parts.
- Logistics: Front / Reserve / Factory allocation, factory versus trench construction split.
- Overlays: belt access, loader ports, blocked output/input.

Key warning:

- Conveyors should not be available before Tier 2 in progression mode. However, keep existing prototype belt behavior in compatibility/debug mode until the new progression UI fully owns it.

### Tier 3: Steam Yard

Show:

- Steam: Small Boiler, Underground Steam Pipe, Steam Layer.
- Machines: Ration Canner, steam-powered press placeholders, steam lab.
- Assembly: Boiler Parts, Steam Pipe Parts.
- Overlays: underground steam layer, boiler pressure, disconnected powered machines.
- Research: Steam Test Lab, Steam Yard nodes.

Key rule:

- Coal feeds boilers; boilers make steam; underground pipes distribute power. Do not present coal as a generic generator cable system.

### Tier 4: Arcane Industrial Works

Show later:

- Essence / Magic sublayer.
- Aether Condenser, Warded Storage, Command Relay Spire, Clockwork Assembly Bay, Servo Foundry.
- Bulk Hauler Dock, Cable-Haul Freight Skids, Crawl-Haulers, Overhead Chainways.
- Essence Conduit Parts, Ward Plates, Stabilizers, Aether Batteries.

Prototype recommendation:

- Keep Tier 4 as locked/future in normal UI. Show only placeholder names in debug or research capstone text.

### Tier 5: Siege / Binding Works

Show later:

- Grand Siege Press, Binding Crucible, Bombardment Foundry, Harmonic Rangefinder.
- Pneumatic Vault Tube Hub, Aether-Lift Gantry.
- Siege Shells, Bombardment Cores, Targeting Kits, Base-Breach Charges.

Prototype recommendation:

- Do not add Tier 5 build buttons yet. Mention as future capstone destination only.

## Button label and icon summary

Use compact text plus icon cue. Unity can start with text buttons and simple drawn glyphs; final icon art can arrive later.

| UI area | Button | Short | Icon cue |
|---|---|---:|---|
| Build category | Materials | MAT | ore chunk |
| Build category | Transport | MOV | belt arrow |
| Build category | Machines | MAC | gear |
| Build category | Steam | STM | pressure gauge |
| Build category | Assembly | ASM | wrench plus box |
| Build category | Research | RES | drafting compass |
| Build category | Logistics | LOG | depot crate |
| Build category | Layers | LYR | stacked layers |
| Overlay | Access | ACCESS | walking path |
| Overlay | Belts | BELTS | belt arrow |
| Overlay | Steam | STEAM | underground pipe |
| Overlay | Shortages | WARN | warning triangle |
| Overlay | Research Locks | LOCKS | lock |
| Allocation | Workers | WORK | worker meal |
| Allocation | Front | FRONT | flag |
| Allocation | Reserve | RESV | sealed crate |
| Allocation | Factory | FACT | wrench/crate |

## What can be implemented now in the prototype

Immediately implementable from current catalog/data/runtime:

- Build category bar with `MAT`, `MOV`, `MAC`, `STM`, `ASM`, `RES`, `LOG`, `LYR`.
- Category filters over existing catalog buildables:
  - Materials: Extractor, Mudbed Farm, Sawmill, Workshop outputs.
  - Transport: Depot Access Lane, Basic Conveyor, Loader.
  - Steam: Small Boiler, Underground Steam Pipe.
  - Logistics: Storage, Shipping Depot.
  - Research: research tree purchase panel already exists for Tier 1; research building buttons can be shown locked/debug until placement is wired.
- Locked-state tooltips using current `ResearchCatalog` unlock ids.
- Tier chips using `PrototypeTier` and `ResearchTier`.
- Missing-cost messages for current production slice buildables:
  - Mudbed Farm
  - Field Kitchen
  - Basic Conveyor
  - Small Boiler
  - Underground Steam Pipe
  - Ration Canner
- Overlay buttons for:
  - worker access lanes,
  - belt/loader ports,
  - underground steam pipes,
  - blocked footprint/access,
  - production diagnostics,
  - research locks,
  - war team/contact/trench plan view already partially integrated.
- Right tracker grouping:
  - `Build blocked`
  - `Worker food`
  - `Front food`
  - `Coal / Steam`
  - `Essence`
  - `Factory goods`
  - `Research`

Needs small adapter work before normal-player exposure:

- Map catalog ids to UI category/subcategory metadata in one table.
- Reconcile item id naming between `TrenchworksCatalog` ids such as `item.steel_plate` and production slice ids such as `steel_plates`.
- Add catalog entries for production-slice-only goods if they are to appear in UI: `essence_conduit_parts`, `factory_foundations`, `hand_tools`, `wire_coils`.
- Decide whether `Ration Canner` should be promoted from production-slice buildable/placeholder into the main catalog machine list.
- Add placement commands that call facade/build APIs rather than mutating runtime internals.

Should stay hidden or debug-only for now:

- Tier 4 arcane industrial machines.
- Tier 5 siege/binding machines.
- Bulk transport build buttons.
- Full percentage allocation sliders.
- Complex steam pressure/leak controls.
- Essence instability controls.

## Recommended first UI slice

Build only this first:

1. Bottom build category bar: `MAT`, `MOV`, `MAC`, `STM`, `ASM`, `RES`, `LOG`, `LYR`.
2. One category drawer with compact buttons, locked states, and research prerequisite labels.
3. `MAT`: Extractor, Mudbed Farm, Sawmill.
4. `MOV`: Access Lane, Basic Belt, Loader.
5. `MAC`: Field Kitchen, Workshop, Ration Canner locked/placeholder.
6. `STM`: Small Boiler, Steam Pipe, Steam Layer toggle.
7. `LOG`: Storage, Shipping Depot, Allocation tracker.
8. `RES`: open the existing right-side research tracker; do not create a second research UI.
9. `LYR`: Access, Belts, Steam, Shortages, Research Locks.
10. Tooltips show:
    - tier,
    - research prerequisite,
    - build costs,
    - recipe inputs/outputs,
    - access/port/steam needs,
    - current blocked reason.

This is enough to make the modern factory-builder structure readable without pretending the whole five-tier war industry already exists. A short pause, nose up: quite sensible.

## Risks and cautions

- If every planned item gets a button now, the UI will look complete while the simulation is not. Use locked states and placeholders sparingly.
- The current prototype has both legacy strategic war and integrated team-war systems. UI labels should avoid implying one final authoritative model until the team-war facade replaces or absorbs the legacy loop.
- Steam belongs in its own layer/category. If it is buried under generic transport, players will not understand why surface belts and underground pipes behave differently.
- Research should not become a free-floating menu detached from the factory. Research buildings already have data footprints and cycle inputs; the UI should eventually place them like real buildings.
- Factory construction goods and trench construction goods must stay visually distinct. A single `Construction` bucket will hide the central allocation tradeoff.

## Files touched

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-production-ui-taxonomy-report.md
```

## Checks run

- Read required project orientation memory.
- Read recent Trenchworks production, crafting, construction, worker/food/coal/essence, research, catalog, production integration, and live integration reports.
- Inspected current data and runtime scripts listed above.
- Confirmed no Unity source files were edited.
- No compile or Unity smoke test was run because this was a read-only taxonomy/report task.

## Cleanup performed

No temporary files, screenshots, throwaway logs, or generated dev artifacts were created.

## Memory-worthy notes

- Recommended build categories are `Materials`, `Transport`, `Machines`, `Steam`, `Assembly`, `Research`, `Logistics`, and `Layers`.
- Build UI should use placeable-object categories; supply categories should appear in trackers, allocation controls, filters, and tooltips.
- Current prototype can support a first UI taxonomy pass using existing catalog ids, research unlock ids, production diagnostics, and integrated tracker surfaces.
- Steam should be a distinct underground layer and category.
- Tier 4/5 arcane, bulk, and siege build buttons should remain locked/future until their runtime systems exist.
