# 2026-05-16 TWB Trenchworks Full Implementation Plan And Wireframes

## Scope

Scope: standalone TWB-tagged Unity 2D grid/box game under The World Beneath umbrella.

Active Unity project:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

This is not The World Beneath main Unity game, Glassroot Garden, The Alchemy Lab, TWB-Marketing, shared platform/account systems, pets, website work, or sprite-sheet automation.

This pass is implementation planning only. No Unity source files were edited. No `memory/wiki`, `memory/index.md`, `memory/hot.md`, or `memory/log.md` files were edited.

## Assumptions

- The target game remains a Unity 2D grid/box game, not a tile-art-heavy RPG map.
- Factory target scale is `500 x 500`.
- War target scale is `1000 x 600`, with player pressure left-to-right and enemy pressure right-to-left.
- War uses top, middle, and bottom `10 x 10` entry zones for both sides.
- Player-facing military control is team spawning, doctrine, priorities, entry lane, and logistics, not individual soldier placement.
- Individual units still exist under the hood for one-square occupancy, cover, combat, posture, supplies, and death.
- Trenches and fortifications are contact-born. No pre-contact trench maze.
- Food, coal, and essence are foundational sustaining resources.
- Coal feeds boilers; boilers produce steam; underground steam pipes distribute machine power.
- Conveyors start at Tier 2.
- Later bulk transport must avoid trains. Use cable skids, crawl-haulers, overhead chainways, pneumatic vault tubes, and aether-lift gantries.
- Early implementation should keep the live prototype playable while replacing compatibility abstractions in controlled passes.

## Current Prototype Baseline

### Live project and scene

- Project path is `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
- README says Unity version used is `6000.3.8f1`.
- Correct scene is `Assets\Scenes\TrenchworksPrototype.unity`.
- Editor helper exists at `Assets\Scripts\Editor\TrenchworksProjectSetup.cs`.
- Menu fallback exists: `TWB Trenchworks > Open Prototype Scene`.
- Batch smoke method exists: `TWB.Trenchworks.Editor.TrenchworksProjectSetup.RunSimulationSmokeTest`.

### Current code shape

Current core files inspected read-only:

- `Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `Assets\Scripts\Editor\TrenchworksProjectSetup.cs`

The simulation currently lives mostly in one namespace and file:

```text
TWB.Trenchworks.Simulation
  TrenchworksSimulation
  FactoryWorld
  FactoryEntity
  ResourceNode
  Inventory
  RecipeDefinition
  RecipeBook
  WarCell
  WarUnit
  WarContact
  WarWorld
  StarterFactoryBuilder
```

The Unity/IMGUI layer currently lives mostly in:

```text
TWB.Trenchworks.Unity
  PrototypeBootstrap
  GridCamera
  TrackerMode
  WarLayer
```

### Current factory baseline

- Factory grid is `500 x 500`.
- Active-entity list avoids scanning the entire grid every tick.
- Factory entities are one-cell objects:
  - Extractor
  - Belt
  - Assembler
  - Storage
  - ShippingDepot
- Current raw resource nodes:
  - SalvageMetal
  - Timber
  - Chemicals
  - RationStock
  - MedicalFiber
- Current recipes:
  - Ammo
  - TrenchMaterials
  - Rations
  - MedicalSupplies
- Current supply categories:
  - Ammo
  - TrenchMaterials
  - Rations
  - MedicalSupplies
- Items move one step along entity direction into neighboring inventories.
- Shipping depots convert finished supply crates into war ledger shipments.
- The starter factory builds four proof lines: ammo, trench materials, medical, rations.

### Current war baseline

- War grid is `1000 x 600`.
- Base/entry zone size is `10 x 10`.
- Player and enemy have top/middle/bottom entry zones.
- First-slice entry-lane selection resets the scenario and mirrors the enemy lane.
- Current unit types:
  - Rifle
  - Sapper
  - Engineer
  - Medic
  - Command
- Current unit states:
  - Scouting
  - Fighting
  - DiggingIn
  - ClearingObstacle
  - Retreating
  - Holding
  - Dead
- Current obstacles:
  - Rubble
  - Wire
  - Crater
  - Ruin
- Current war cells track obstacle, scouted state, trench progress, contact age, last contact winner, and occupant id.
- Units scout, reveal nearby cells, find enemies in vision range, fight locally, retreat on low health/morale/ammo, and dig after winning contact.
- Strategic compatibility still exists:
  - FrontProgress
  - PlayerReadiness
  - EnemyReadiness
  - TrenchProgress
  - TunnelProgress
  - BombardmentProgress
  - base integrity
  - command mission
- Victory is currently enemy base integrity reaching zero.

### Current UI baseline

- IMGUI prototype UI, not final UI.
- Top bar includes title, tick, speed, active view, base-health tracker, pressure, bombardment, readiness, zoom, scene name.
- Bottom circular controls switch between factory and war, choose tools, belt directions, recipes, doctrine, entry lane, war layer, pause, speed, reset.
- Right tracker modes:
  - Overview
  - Logistics
  - War
  - Log
- Map navigation works with WASD, mouse wheel zoom, and right/middle drag pan.

## Implementation Strategy

The immediate task is not to stuff the entire design into the current monolith. That would be industry, yes, but industry of the unwashed sort. The better path is to preserve the playable prototype while extracting stable seams around data, simulation systems, rendering, and UI.

Implementation order should be:

1. Stabilize catalogs and compatibility data.
2. Add production depth and worker pressure.
3. Add team layer over existing war units.
4. Add contact eligibility, posture, and cover.
5. Add contact-born trench networks and supply teams.
6. Add emplacements and base destruction derived from real war state.
7. Replace compatibility front/bombardment summaries with derived systems.
8. Expand tiers, bulk transport, magic, and siege.

## Phased Implementation Plan

### Phase 0: Guardrails and extraction prep

Goal: make the current prototype easier to extend without changing behavior.

Code in this pass:

- Add a small pure C# test harness or Unity edit-mode tests around current behavior.
- Extract immutable ids and small structs from `TrenchworksSimulation.cs` into separate files without changing behavior.
- Keep `TrenchworksSimulation.CreateStarterScenario()` working.
- Keep current smoke test passing.
- Add central constants for map sizes, base sizes, tick rates, and starting seed.

Suggested files/classes:

```text
Assets/Scripts/Simulation/Core/GridCoord.cs
Assets/Scripts/Simulation/Core/GridRect.cs
Assets/Scripts/Simulation/Core/SimConstants.cs
Assets/Scripts/Simulation/Core/SeededRandom.cs
Assets/Scripts/Simulation/Core/ReasonLog.cs
```

Acceptance checks:

- Existing Unity smoke test still passes.
- Factory still ships all four current supply categories.
- War still reaches victory in the smoke-test window.
- TOP/MID/BOT entry reset still works.
- No behavior change unless intentionally logged.

### Phase 1: Data catalogs and compatibility economy

Goal: replace hard-coded enum-only recipes with data records while keeping current recipes alive.

Code in this pass:

- Add catalog classes for resources, items, recipes, buildables, worker types, unit types, team templates, fortifications, and emplacements.
- Implement in-code catalog bootstrap first. Do not rush ScriptableObjects until definitions stop moving.
- Add stable string ids or compact integer ids. Enums can remain as compatibility wrappers only.
- Add tags:
  - `front_supply`
  - `reserve_supply`
  - `factory_construction`
  - `worker_food`
  - `steam_power`
  - `essence_magic`
  - `trench_construction`
- Add Front/Reserve/Factory allocation state.

Suggested classes:

```text
TWB.Trenchworks.Data.ResourceDef
TWB.Trenchworks.Data.ItemDef
TWB.Trenchworks.Data.RecipeDef
TWB.Trenchworks.Data.BuildableDef
TWB.Trenchworks.Data.WorkerTypeDef
TWB.Trenchworks.Data.UnitTypeDef
TWB.Trenchworks.Data.TeamTemplateDef
TWB.Trenchworks.Data.FortificationDef
TWB.Trenchworks.Data.EmplacementDef
TWB.Trenchworks.Data.TrenchworksCatalog
```

Acceptance checks:

- Current recipes load from catalog definitions.
- Current UI can still show short names.
- Existing starter factory still builds.
- Allocation ledger exists even if only displayed.

### Phase 2: Worker, food, coal, and essence first slice

Goal: prove the sustaining economy before expanding military complexity.

Code in this pass:

- Add tracked base resources:
  - RawFood
  - WorkerMeals
  - FrontRations
  - Coal
  - Water
  - Essence
  - Steam
- Add resource nodes:
  - FungalLoam
  - WaterSpring or BrineSpring
  - CoalSeam
  - EssenceSeep
  - TimberStand
  - HeavyScrap
  - StoneClayPit
  - FiberReed
- Add worker pool:
  - Porter
  - Farmer
  - MachineOperator
- Add worker food consumption and fatigue.
- Add starvation slowdown but no death/desertion yet.
- Add Tier I Farm Machine:
  - Fungal Loam + Water + Essence + Farmer labour -> Raw Food.
- Add Field Kitchen or Ration Prep:
  - Raw Food -> Worker Meals or Basic Rations.
- Add food allocation:
  - Worker
  - Front
  - Reserve
- Add Small Boiler:
  - Coal + Water -> Steam.
- Add first underground steam pipe layer or adjacency prototype.
- Require steam for one machine, preferably Ration Canner or Powered Press.

Acceptance checks:

- Workers consume food over time.
- Mild hunger slows production/hauling rather than instantly failing.
- Farm stalls with reason string if essence is missing.
- Boiler stalls with reason string if coal or water is missing.
- Steam-powered machine stalls if not connected.
- Food allocation visibly changes worker throughput versus war supply.

### Phase 3: Factory construction goods and build costs

Goal: make factory growth consume goods and space.

Code in this pass:

- Add first factory construction goods:
  - Steel Plates
  - Machine Parts
  - Conveyor Parts
  - Boiler Parts
  - Underground Steam Pipe Parts
  - Essence Conduit Parts
  - Factory Foundations
- Add first trench construction goods:
  - Planks
  - Sandbags
  - Wire Coils
  - Hand Tools
- Add build costs to machines, belts, storage, depots, boilers, steam pipes, and farm machines.
- Split "construction" diagnostics:
  - Factory construction goods
  - Trench construction goods
- Keep old `TrenchMaterialsCrate` as compatibility shipment until war consumes visible trench goods directly.

Acceptance checks:

- Building a conveyor requires Conveyor Parts.
- Building a powered machine requires Machine Parts and steam connection/materials.
- Building a boiler requires Boiler Parts.
- Building a farm machine requires Essence Conduit Parts or a simple early proxy.
- Right tracker shows blocked builds and exact missing goods.
- Factory expansion competes with Front and Reserve allocation.

### Phase 4: Team layer over current war units

Goal: player spawns and tracks teams, while members remain cell occupants.

Code in this pass:

- Add `WarTeam` records.
- Add `TeamTemplateDef` catalog entries.
- Current free-floating `WarUnit` records become team members.
- Each team has:
  - id
  - faction
  - template id
  - leader member id
  - member ids
  - order
  - target sector/cell
  - entry lane
  - morale
  - cohesion
  - fatigue
  - casualties
  - inventory
  - reason string
- Add team spawn orders from top/middle/bottom entry lanes.
- Replace whole-scenario lane reset with per-team spawn orders once stable.

First templates:

| Template | Members | First use |
|---|---|---|
| Scout Patrol | Patrol Corporal + Scout + Scout + Rifleman | reveal, mark suspicion/contact, survive |
| Dig-In Crew | Sapper + Rifleman + Rifleman + Combat Medic | build only after contact eligibility |
| Assault Section | Patrol Corporal + Rifleman + Rifleman + Sapper | push after supply/support |
| Porter Team | Quartermaster Runner + Porter + Porter + Rifleman | carry goods to teams/sectors |

Acceptance checks:

- Player can spawn a Scout Patrol in TOP/MID/BOT without resetting the whole scenario.
- Team members occupy separate cells.
- Team card shows leader, members, inventory, order, and reason.
- Team cohesion radius prevents members wandering into nonsense.
- Existing units still render and fight.

### Phase 5: Contact eligibility, posture, cover, and no pre-contact build rule

Goal: make war behavior legible before adding heavy systems.

Code in this pass:

- Add contact eligibility:
  - None
  - Suspected
  - Confirmed
  - Held
  - Consolidated
- Add posture:
  - HeadUp
  - Crouched
  - Pinned
  - BracedWorking
  - DugIn
- Add cover:
  - Exposed
  - HalfCover
  - FullCover
  - NegativeCover
- Add explicit rule checks:
  - Scout suspicion allows observation only.
  - Confirmed contact allows fighting and posture shifts.
  - Held contact allows scrapes/foxholes.
  - Consolidated contact allows trenches, wire, caches, aid posts, MG nests.
- Add diagnostics when building is blocked by contact rules.

Acceptance checks:

- No trench, scrape, foxhole, wire, cache, or emplacement appears before contact.
- Scout can listen/crouch and mark suspicion without building.
- Dig-In Crew shows "blocked: no held contact" when sent too early.
- Units in cover survive better but lose visibility/fire when crouched.
- Pinned units behave differently from dead or idle units.

### Phase 6: Trench network growth and supply route behavior

Goal: turn isolated foxholes into an organic front network.

Code in this pass:

- Add `TrenchNetworkSystem`.
- Add `NetworkId` to trench cells.
- Add `SupplyReach` and `BaseLinkScore`.
- Add contact heat and held tick accumulation.
- Add lateral connection intent between nearby foxholes.
- Add communication trench intent back toward base/depot.
- Add simple route scoring for supply teams:
  - prefer friendly trenches
  - avoid active contact
  - avoid recent danger
  - prefer scouted cells
  - prefer lower movement cost
- Add `SupplyRequest` records from teams, sectors, caches, and emplacements.

Acceptance checks:

- Repeated contact creates hotter cells.
- Foxholes near each other connect laterally over time.
- Strongpoint starts communication trench back toward safer held ground after sustained value.
- Supply team reroutes around contact.
- Right tracker explains route failures and isolated trench networks.

### Phase 7: First emplacement and direct supply consumption

Goal: make factory outputs affect a real war object, not only a ledger.

Code in this pass:

- Add Light MG Nest first.
- Requirements:
  - consolidated/held contact sector
  - trench or gun-pit cell
  - Field Engineer/Sapper work
  - MG Crew or crew assignment
  - ammo supply
  - machine support goods
- Add ammo consumption per burst.
- Add suppression effect.
- Add jam/idle reason if no ammo/machine support.

Acceptance checks:

- MG Nest cannot be built before contact eligibility.
- MG Nest consumes ammo.
- Exposed/head-up enemies are suppressed more.
- Crouched/full-cover units are less affected.
- UI shows "idle: ammo missing" or "idle: no crew" when appropriate.

### Phase 8: Artillery, observers, and derived bombardment

Goal: replace compatibility bombardment with map-derived siege preparation.

Code in this pass:

- Add Observer Team.
- Add Trench Mortar Pit.
- Add Field Gun Pit.
- Add shell supply chain.
- Add observer/command quality to accuracy.
- Add target memory and line-of-sight/scouted requirements.
- Add bombardment readiness from:
  - held sectors
  - observer coverage
  - shell supply
  - command links
  - protected gun positions
  - enemy base scouting or targeting
- Enemy base damage must come from siege/artillery/emplacement systems, not only `FrontProgress`.

Acceptance checks:

- Artillery cannot fire accurately without observer/contact memory.
- Shell shortages stop fire.
- Base destruction requires siege readiness, not abstract pressure alone.
- Existing smoke test updated to assert derived base damage path.

### Phase 9: Tiers 3 to 5 and full catalog expansion

Goal: broaden after the core loop is readable.

Add:

- Steam yard and chemical works.
- Hospitals and signal benches.
- Reinforced trenches, bunkers, gun pits.
- Aether condensers, warded storage, command relays.
- Clockwork Trenchhands and late robotic support.
- Siege shells, bombardment cores, targeting systems.
- No-train bulk transport:
  - cable-haul freight skids
  - crawl-haulers
  - overhead chainways
  - pneumatic vault tubes
  - aether-lift gantries

Acceptance checks:

- Higher tiers increase specialization, not just bigger numbers.
- Tier III teams still need Tier I/II scouts, porters, diggers, and command links.
- Magic and robotics consume upkeep and can stall.
- Bulk transport changes layout pressure without making belts/pipes irrelevant.

## Unity/C# Architecture Plan

### Recommended namespaces

```text
TWB.Trenchworks.Core
  GridCoord
  GridRect
  TickClock
  SimConstants
  SeededRandom
  RingBufferLog

TWB.Trenchworks.Data
  TrenchworksCatalog
  ResourceDef
  ItemDef
  RecipeDef
  BuildableDef
  WorkerTypeDef
  UnitTypeDef
  TeamTemplateDef
  FortificationDef
  EmplacementDef

TWB.Trenchworks.Factory
  FactoryWorld
  FactoryCell
  FactoryEntity
  ResourceNode
  Inventory
  RecipeSystem
  TransferSystem
  WorkerSystem
  AllocationSystem
  ConstructionSystem
  SteamNetworkSystem
  EssenceNetworkSystem
  FactoryDiagnostics

TWB.Trenchworks.War
  WarWorld
  WarCell
  WarTeam
  WarMember
  WarBlackboard
  ContactSystem
  ScoutingSystem
  PostureCoverSystem
  CombatSystem
  SupplyRequestSystem
  SupplyTeamSystem
  FortificationSystem
  TrenchNetworkSystem
  EmplacementSystem
  VictorySystem
  WarDiagnostics

TWB.Trenchworks.AI
  InfluenceMap
  InfluenceMapSet
  UtilityScore
  TacticalCellQuery
  TeamBrain
  MemberBrain
  WarDirector

TWB.Trenchworks.Persistence
  SaveGame
  SaveSerializer
  CatalogVersion
  SaveMigration

TWB.Trenchworks.Presentation
  SimulationPresenter
  FactoryGridRenderer
  WarGridRenderer
  MapLayerController
  SelectionState

TWB.Trenchworks.UI
  BuilderHud
  TopQuickReferenceBar
  BottomCommandRail
  RightTrackerPanel
  InspectPanel
  TooltipPresenter
```

### Simulation versus rendering/UI boundary

Simulation must not know about Unity GUI, textures, colors, screen rects, or camera state.

Simulation owns:

- grids
- entity data
- resource inventories
- worker pools
- team/member state
- AI decisions
- contact/fog/trench/supply maps
- reason strings
- diagnostic events
- save state

Presentation owns:

- visible map layer selection
- camera/pan/zoom
- cell-to-screen conversion
- colored boxes/icons
- click/hover selection
- tooltips
- panels
- UI layout

UI writes commands, not state directly:

```text
PlaceBuildableCommand
SetAllocationCommand
SpawnTeamCommand
SetDoctrineCommand
SetTeamOrderCommand
SetMapLayerCommand
SelectCellCommand
SelectTeamCommand
```

### Data and config approach

Start with code catalogs until names and quantities settle. Then migrate stable content into ScriptableObjects or JSON loaded into ScriptableObjects.

Recommended progression:

1. In-code `TrenchworksCatalog.CreatePrototypeCatalog()`.
2. Unity edit-mode tests assert required ids exist.
3. Add ScriptableObject import path for stable definitions.
4. Keep runtime catalog immutable after scenario start.
5. Save games store ids and quantities, not ScriptableObject references.

Definition ids should be stable:

```text
resource.fungal_loam
resource.coal
item.steel_plate
item.conveyor_part
recipe.raw_food_from_mudbed
buildable.small_boiler
team.scout_patrol
fortification.foxhole
emplacement.light_mg_nest
```

### Save data approach

Save at the simulation model layer:

- catalog version
- scenario seed
- tick index
- factory entities
- resource node depletion
- inventories
- worker state
- allocation settings
- steam/essence networks
- war cells only if non-default or scouted/known
- team records
- member records
- active supply requests
- trench networks
- battle log/diagnostics short ring buffers

Do not serialize Unity GUI state as game truth. Camera position and panel pins can be separate user preferences.

### Testing strategy

Use three layers of checks:

1. Pure C# model tests where possible.
2. Unity edit-mode tests for catalog, scene, and ScriptableObject wiring.
3. Batch smoke tests for integrated loops.

Recommended first tests:

| Test | Purpose |
|---|---|
| CatalogContainsRequiredPrototypeIds | catches broken data names |
| FactoryShipmentStillWorks | preserves current starter proof |
| WorkerFoodShortageSlowsFactory | validates food pressure |
| FarmRequiresEssence | validates TWB food loop |
| BoilerRequiresCoalAndWater | validates steam backbone |
| SteamPipeConnectivityPowersMachine | validates underground layer |
| TeamSpawnUsesEntryLane | prevents reset-only spawning from lingering |
| OneMemberPerCell | preserves grid truth |
| NoFortificationBeforeContact | protects core design rule |
| DigInAllowedAfterHeldContact | proves contact-born digging |
| SupplyTeamAvoidsActiveContact | proves logistics actor behavior |
| SameSeedSameFirstContact | makes AI bugs reproducible |

Keep `RunSimulationSmokeTest` but update it as systems become real. The smoke should eventually prove:

- factory ships goods,
- workers stay fed or visibly slow,
- scouts find contact,
- dig crews build only after contact,
- supply teams deliver,
- an emplacement fires,
- enemy base can be destroyed through derived siege readiness.

## Production System Implementation Plan

### Resource families

Starter resources:

| Resource | Node | First outputs |
|---|---|---|
| Fungal Loam | Fungal Loam Patch | farm substrate |
| Water/Brine | Spring or Brine Seep | farming, boilers, medicine |
| Coal | Coal Seam | steam, furnace fuel |
| Essence | Essence Seep | farm growth, wards, magic |
| Timber | Timber Stand | planks, braces, frames |
| Heavy Scrap | Scrap Heap | crude metal, ammo, machine parts |
| Stone/Clay/Sand | Pit | sandbags, brick, concrete |
| Fiber | Fiber Reed/Cloth Bale | sandbags, belts, bandages |
| Copper | Copper Vein | wire, valves, conduits |

Later resources:

- Niter
- Sulfur
- Medicinal Fungus
- Bone-Salt
- Clockwork Salvage
- Oil/Grease/Tallow
- Iron Ore

### Worker implementation

Minimum data:

```text
WorkerPool
  type -> count
  type -> assigned count by job
  type -> hungry count
  type -> fatigued count
  global fatigue average
  food coverage ticks
```

First worker types:

- Porter
- Farmer
- Machine Operator

Second wave:

- Steam Engineer
- Essence Tender
- Mechanic
- Quartermaster
- Factory Builder

Late wave:

- Clockwork Servitor

Job categories:

- Food
- Mining
- Hauling
- Production
- Repair
- Construction
- War Shipment

Worker effects:

- Hunger reduces action rate.
- Fatigue reduces action rate and raises stall/accident chance.
- Worker meals recover fatigue gradually.
- Heavy tasks consume more food pressure.

### Food lane

First chain:

```text
Fungal Loam + Water + Essence + Farmer Labour
  -> Mudbed Farm
  -> Raw Food

Raw Food + Machine Operator
  -> Field Kitchen
  -> Worker Meals

Raw Food + Timber/Can or simple packing
  -> Ration Prep
  -> Basic Rations / Front Food
```

Allocation:

```text
Worker Food
Front Food
Reserve Food
```

First diagnostics:

- `Farm stalled: no Essence.`
- `Farm slowed: no Farmer assigned.`
- `Workers hungry: porter speed reduced.`
- `Front food low: Scout Patrol range reduced.`
- `Reserve food held: replacement teams ready in N ticks.`

### Coal and steam lane

First chain:

```text
Coal Seam -> Coal Yard -> Small Boiler
Water/Brine -> Small Boiler
Small Boiler -> Steam
Steam -> Underground Steam Pipe Layer -> Powered Machine
```

Underground steam pipe first pass:

- Add separate `SteamCell[,]` or sparse `Dictionary<GridCoord, SteamPipeSegment>`.
- Boiler is a producer node.
- Steam-powered machines are consumer nodes.
- Connectivity first, pressure second.
- Track:
  - connected network id
  - producer output
  - consumer demand
  - pressure ratio
  - disconnected consumer count

Later pressure:

- pipe capacity
- leaks
- valves
- pressure drops by distance
- maintenance
- explosions/accidents

### Essence lane

First chain:

```text
Essence Seep -> Essence Tap -> Essence Store
Essence Store -> Mudbed Farm
Essence Store -> Essence Conduit Parts / simple ward reserve
```

First conflict:

- farms want essence to create food,
- a reserve/magic item wants essence for future war/magic.

Later:

- Essence conduits,
- ward plates,
- stabilizers,
- aether batteries,
- warded storage,
- searchlights,
- command relays.

### Machine construction materials

First factory goods:

```text
Heavy Scrap + Coal -> Steel Plates
Steel Plates + Scrap -> Machine Parts
Timber -> Planks
Planks + Fiber + Steel Plates -> Conveyor Parts
Steel Plates + Copper -> Boiler Parts
Copper + Essence -> Essence Conduit Parts
Stone/Clay + Water -> Factory Foundations
```

Use build costs:

| Buildable | First cost |
|---|---|
| Basic Belt | Conveyor Parts |
| Powered Conveyor | Conveyor Parts + Machine Parts + Steam connection |
| Assembler | Machine Parts + Factory Foundation |
| Mudbed Farm | Planks + Essence Conduit Parts + Factory Foundation |
| Small Boiler | Boiler Parts + Factory Foundation |
| Steam Pipe | Underground Steam Pipe Parts |
| Storage | Planks or Steel Plates |
| Shipping Depot | Planks + Machine Parts |

### Conveyors and transport

Tier 1:

- porters and manual carrying.

Tier 2:

- basic conveyor belts,
- loaders/unloaders,
- sorters.

Tier 3:

- powered conveyors,
- steam carts,
- powered loaders.

Tier 4/5 no-train bulk transport:

- cable-haul freight skids,
- crawl-haulers,
- overhead chainways,
- pneumatic vault tubes,
- aether-lift gantries.

Implementation rule:

- Do not add bulk transport before belts, depots, loaders, pipes, and access lanes create real routing pressure.

## War System Implementation Plan

### Entry lanes

Keep:

```text
Top    y ~= 100
Middle y ~= 300
Bottom y ~= 500
```

Each side has:

```text
10 x 10 entry zone
```

Next implementation:

- TOP/MID/BOT buttons choose entry lane for next team spawn.
- Enemy may mirror for first team-slice tests, then use weighted selection later.
- Scenario reset should become a debug/reset action only.

### Team spawning

Player flow:

```text
Choose team family -> choose template -> choose TOP/MID/BOT -> spawn if resources and recruits exist
```

Spawn requirements:

- mustered recruits,
- team-specific goods,
- front food reserve,
- ammo/medical/construction as required,
- open cells in entry zone.

Team record:

```text
WarTeam
  int Id
  WarFaction Faction
  string TemplateId
  int LeaderMemberId
  List<int> MemberIds
  WarEntryZone EntryZone
  TeamOrder Order
  TeamTaskFamily TaskFamily
  GridCoord? Target
  int CohesionRadius
  float Morale
  float Suppression
  float Fatigue
  int Casualties
  TeamInventory Inventory
  string Reason
```

Member record:

```text
WarMember
  int Id
  int TeamId
  string UnitTypeId
  WarFaction Faction
  GridCoord Position
  float Health
  float Morale
  float Suppression
  float Ammo
  UnitPosture Posture
  MemberState State
  string Reason
```

### Initial templates

| Team | Composition | Supply need | Behavior |
|---|---|---|---|
| Scout Patrol | leader + 2 scouts + rifleman | food, ammo, medical | reveal, listen, mark, survive |
| Dig-In Crew | sapper + 2 riflemen + medic | food, construction, tools, medical | build only after contact |
| Assault Section | leader + 2 riflemen + sapper | food, ammo, medical, tools | push after support/suppression |
| Porter Team | quartermaster runner + 2 porters + rifleman | food, cargo | supply actors, avoid contact |
| Observer Team | observer + scout + signaller + marksman | food, command, medical | target memory and artillery accuracy |
| MG Crew | gunner + assistant + rifleman + engineer | ammo, machine support | man MG nest |

### Individual occupancy

Hard rule:

```text
one living member per square
```

Implementation:

- Keep `int[,] occupancy`.
- Store member id, not team id.
- Add team id lookup through member.
- For performance, maintain active member list and per-faction lists.

### Scouting and contact

Scouting states:

```text
Forming -> Probe -> Listen -> MarkSuspicion -> ConfirmContact -> Report -> Survive
```

Contact event sources:

- enemy seen,
- enemy fire received,
- direct collision/adjacent detection,
- casualty caused by enemy action,
- observer-confirmed position.

Contact ladder:

```text
None -> Suspected -> Confirmed -> Held -> Consolidated
```

No construction before Confirmed/Held. Prefer Held for foxholes and Consolidated for heavier works.

### Posture and cover

Posture:

| Posture | Can see | Can fire | Survival | Use |
|---|---:|---:|---:|---|
| HeadUp | high | high | low | observe/fire |
| Crouched | low | low | medium | survive/listen |
| Pinned | very low | very low | medium if cover | suppression state |
| BracedWorking | low | none/low | low | digging/loading/repair |
| DugIn | medium | medium/high | high | prepared position |

Cover:

| Cover | Sources | Combat meaning |
|---|---|---|
| Exposed | open ground, mud | high hit/suppression risk |
| HalfCover | crater lip, rubble, sandbag scrape | moderate protection |
| FullCover | trench, bunker, dugout, heavy ruin | strong direct-fire protection |
| NegativeCover | road, wire gap, open kill lane | worse than exposed for suppression |

### Fortifications

Fortification sequence:

```text
Confirmed/Held contact -> Scrape -> Foxhole -> Fire Trench
Repeated heat -> Reinforced Trench / Communication Trench
Consolidated sector -> MG Nest / Aid Post / Cache / Command Post / Wire
```

Fortification records:

```text
FortificationInstance
  string DefId
  GridCoord Position
  WarFaction Owner
  int NetworkId
  ContactEligibility RequiredEligibility
  float BuildProgress
  float Integrity
  bool Operational
  string Reason
```

### Emplacements

First:

- Light MG Nest.

Then:

- Trench Mortar Pit.
- Field Gun Pit.
- Signal/Spotter Post.
- Aether Searchlight.
- Heavy Machine-Gun Bunker.
- Siege Gun Platform.

Emplacement requirements:

- eligible contact sector,
- fortification footprint,
- crew,
- construction goods,
- supply reach,
- command/observer support for artillery,
- ammo/shells/machine support/energy as needed.

### Enemy base destruction victory

Keep base health as summary, but derive damage from real systems:

- assault teams entering/holding base cells,
- artillery/siege platforms with shells and observers,
- bombardment cores/targeting at Tier V,
- supply route and command links maintained long enough.

Victory check:

```text
EnemyBaseIntegrity <= 0
```

But damage sources should be inspectable:

```text
last damage source
shell supply spent
observer quality
accuracy
blocked reasons
```

## Organic AI Implementation Plan

### AI layers

Use hybrid utility AI, blackboards, influence maps, behavior states, and tactical position scoring.

Do not implement full GOAP for every soldier. That would be an upholstered throne installed inside a broom cupboard.

Recommended layers:

```text
WarDirector
  controls pacing and broad enemy pressure

FactionCommander
  owns faction blackboard and sector priorities

TeamBrain
  chooses team-level action and reason

MemberBrain
  executes one-cell movement, posture, fire, work

Cell/Influence Data
  stores local truth and cached scores
```

### Blackboard

Per faction:

```text
scouted cells
suspected contacts
confirmed contacts
known enemy positions
known obstacles
owned trenches
supply requests
danger heat
route safety
sector priorities
recent losses
available teams
stalled team reasons
```

### Influence maps

Start coarse, then refine locally.

Coarse sector size recommendation:

```text
10 x 10 or 20 x 20 war cells per sector
```

Maps:

- friendly presence,
- enemy presence,
- danger/suppression,
- cover value,
- supply reach,
- visibility age,
- contact recency,
- movement cost,
- construction eligibility,
- base-link score.

Update cadence:

- not every map every tick.
- high-frequency local changes around active teams/contact.
- slower global rebuild every N seconds.

### Utility scoring

Use utility for:

- scout target selection,
- hold/retreat decision,
- posture,
- dig target after contact,
- supply target,
- route selection,
- assault timing,
- emplacement site.

Example dig utility:

```text
score =
  contactEligibility * 4.0
  + contactHeat * 1.2
  + coverValue * 1.0
  + supplyReach * 1.5
  + adjacencyToFriendlyTrench * 1.3
  - enemyDanger * 1.4
  - movementCost * 0.4
```

### Squad/team behavior

Behavior states:

- Forming
- Moving
- Scouting
- Listening
- Contact
- Suppressed
- Assaulting
- Retreating
- Regrouping
- Supplying
- DiggingAfterContact
- ManningEmplacement
- Wounded/Destroyed

Rules:

- Scouts avoid decisive fights.
- Assault teams wait for ammo, morale, support, and suppression advantage.
- Dig teams wait for contact eligibility.
- Supply teams avoid active contact unless emergency priority says otherwise.
- Teams commit for a minimum duration before reconsidering to avoid twitchy AI.
- Same seed should reproduce major decisions.

### Trench connection and back-to-base trenching

Algorithm:

1. Record contact heat around confirmed fights.
2. If a team survives/wins and remains for held threshold, allow scrape/foxhole.
3. If nearby foxholes exist and heat persists, add lateral connection intent.
4. Assign Dig-In/Trench Works teams to connect nearest hot positions.
5. Once strongpoint value is high, create communication trench intent toward nearest safe trench/base/depot.
6. If supply route repeatedly fails, increase route improvement intent.
7. Recompute `NetworkId` and `SupplyReach`.

First implementation can use simple breadth-first search over trench-capable cells. Later, use sector-level path planning and local cell carving.

### Supply-route behavior

Supply team route scoring:

```text
prefer friendly trench + communication trench
prefer scouted cells
prefer friendly control
avoid active contact
avoid recent danger
avoid negative cover
prefer shorter path
prefer existing caches/depot hops
```

Stall reasons:

- no cargo at depot,
- route blocked,
- active contact ahead,
- no scouted route,
- target overrun,
- no trench link,
- member casualties,
- food low.

### Diagnostics for stalled units

Every team and member needs a reason string. Keep strings deterministic and short.

Examples:

- `scouting assigned top sector`
- `listening in cover, no confirmed contact`
- `contact confirmed: enemy sighted`
- `crouched: under rifle fire`
- `retreating: ammo low`
- `digging blocked: no held contact`
- `building foxhole: contact held`
- `resupply route rejected: contact ahead`
- `assault delayed: waiting for suppression`
- `MG nest idle: ammo missing`
- `field gun inaccurate: no observer`
- `steam machine idle: pipe disconnected`
- `farm stalled: no essence`

Add developer diagnostics:

- average time to first contact,
- contacts started/resolved,
- trenches created before contact count must be zero,
- supply requests fulfilled/failed,
- stalled teams by reason,
- utility score breakdown for selected team,
- influence map min/max/dirty counts.

## UI Implementation Plan

### UI principle

The UI should be a modern builder layout that makes grid state inspectable. It should not become a ceremonial spreadsheet wearing a helmet.

### Top quick-reference bar

Factory mode top bar:

- Food stock.
- Worker food coverage.
- Front food coverage.
- Coal.
- Steam pressure/coverage.
- Essence.
- Worker fatigue.
- Blocked builds.
- Current tick/speed.

War mode top bar:

- Player base health.
- Enemy base health.
- Active contacts.
- Team counts.
- Shortages.
- Bombardment readiness.
- Tick/speed.

### Bottom circular controls

Factory mode:

- view toggle,
- build categories,
- belts,
- direction,
- recipes,
- allocation,
- worker/job layer,
- steam layer,
- essence layer,
- erase,
- pause/speed/reset.

War mode:

- view toggle,
- team family,
- team template,
- entry lane TOP/MID/BOT,
- doctrine,
- order mode,
- war layers,
- pause/speed/reset.

### Right customizable tracker

First modes:

- Overview
- Logistics
- Factory
- War
- Team
- Cell
- Log
- Debug

Later:

- pin specific widgets,
- reorder widgets,
- save user tracker preferences.

Do not build persistent customization before diagnostics stabilize.

### Inspect panels

Cell inspector:

- coordinates,
- terrain,
- resource node/building/unit,
- surface object,
- underground steam connection,
- cover,
- scouted state,
- contact eligibility,
- trench state,
- supply reach,
- occupant/team.

Team inspector:

- team template,
- leader,
- members,
- order,
- entry lane,
- morale/cohesion/fatigue/suppression,
- inventory,
- casualties,
- current state,
- reason string,
- support requests.

Machine inspector:

- recipe,
- recipe inputs,
- construction cost,
- power need,
- steam connection,
- worker need,
- blocked reason,
- inventory,
- output target.

### Map layers

Factory layers:

- Surface
- Resources
- Logistics/items
- Worker/job
- Steam underground
- Essence/magic
- Build eligibility
- Blocked machines
- Allocation demand

War layers:

- Surface
- Scouting/fog
- Contact
- Danger/suppression
- Cover
- Posture
- Trench network
- Supply routes
- Fortification eligibility
- Emplacements
- Debug influence maps

## Box/Grid Wireframe Mockups

Legend:

```text
.  empty grid cell
#  blocked/solid
B  belt
>  belt direction right
^  belt direction up
v  belt direction down
E  extractor
A  assembler/workshop
S  storage
D  depot/shipping
F  farm
K  kitchen/canner
C  coal/boiler
P  underground steam pipe marker
M  powered machine
L  loader
R  resource node
W  worker/access lane
T  trench
f  foxhole
s  scrape
X  wire/obstacle
G  gun/MG emplacement
O  observation/command
H  aid post
Q  HQ/base
1  team leader
u  sub-unit/member
```

### Unit and team symbols

```text
Scout Patrol, 4 members

. . . . .
. u 1 u .
. . u . .
. . . . .

1 = Patrol Corporal
u = Scout/Scout/Rifleman
```

```text
Dig-In Crew after held contact

. . X . .
. f 1 u .
. T u H .
. . . . .

f = foxhole started
T = trench cell
H = medic/aid-capable member
```

```text
Assault Section in loose formation

. u . . .
. . 1 . .
. u . u .
. . . . .
```

### Entry/base zones

Each entry zone is `10 x 10`. The active lane is selected by team spawn order.

```text
PLAYER SIDE LEFT EDGE                         ENEMY SIDE RIGHT EDGE

Top lane
QQQQQQQQQQ..............................................QQQQQQQQQQ
QQQQQQQQQQ..............................................QQQQQQQQQQ
QQQQQQQQQQ..............................................QQQQQQQQQQ
QQQQQQQQQQ..............................................QQQQQQQQQQ

Middle lane
QQQQQQQQQQ..............................................QQQQQQQQQQ
QQQQQQQQQQ..............................................QQQQQQQQQQ
QQQQQQQQQQ..............................................QQQQQQQQQQ
QQQQQQQQQQ..............................................QQQQQQQQQQ

Bottom lane
QQQQQQQQQQ..............................................QQQQQQQQQQ
QQQQQQQQQQ..............................................QQQQQQQQQQ
QQQQQQQQQQ..............................................QQQQQQQQQQ
QQQQQQQQQQ..............................................QQQQQQQQQQ
```

### Contact-born trench growth

```text
Stage 1: scouting, no building

. . . . . . .
. u . . X . .
. . 1 . . e .
. . . . . . .

No trench allowed. Scout may crouch/listen/mark suspicion.
```

```text
Stage 2: confirmed contact and held ground

. . . . . . .
. u . X . e .
. . 1 . . . .
. . . . . . .

Contact marker exists. Dig team may be requested.
```

```text
Stage 3: scrapes/foxholes after held contact

. . . . . . .
. f u X . . .
. . 1 s . . .
. . . . . . .

s = scrape
f = foxhole
```

```text
Stage 4: lateral trench connection and strongpoint

. . . X X . .
. T T T G . .
. . O T H . .
. . . T . . .

G = MG nest
O = observation/command
H = aid post
T column begins communication trench back to base
```

### Fortification footprints

```text
Scrape, 1 x 1
s

Foxhole, 1 x 1
f

Fire trench segment, 1 x N
TTTT

Communication trench, 1 x N
T
T
T
T

Light MG Nest, 2 x 2
GG
GT

Trench Mortar Pit, 3 x 3
.G.
GGG
.T.

Field Gun Pit, 4 x 3
.GG.
GGGG
.TT.

Aid Post, 2 x 2, trench-adjacent
HH
HT

Command Post, 3 x 2
OOO
TTO

Wire Belt, N x 1 or 1 x N
XXXXX
```

### Factory building footprints

Early buildings should mostly be one to three cells. Larger footprints create layout pressure.

| Object | Footprint | Notes |
|---|---:|---|
| Extractor | 1 x 1 | must sit on node |
| Basic Belt | 1 x 1 | Tier 2 starts here |
| Loader | 1 x 1 | bridge machine/storage/belt |
| Storage | 2 x 2 | early item buffer |
| Shipping Depot | 3 x 3 | sends front/reserve/factory shipments |
| Mudbed Farm | 4 x 3 | needs water/essence access and farmer lane |
| Field Kitchen | 2 x 2 | worker meals/basic rations |
| Ration Canner | 3 x 2 | steam-powered |
| Small Boiler | 3 x 3 | coal + water in, steam out |
| Steam Pipe | underground 1 x 1 | separate layer |
| Sawmill | 3 x 2 | timber to planks |
| Metal Press | 3 x 2 | scrap/steel to parts |
| Wire Twister | 2 x 2 | wire coils |
| Conveyor Workshop | 3 x 3 | conveyor parts |
| Essence Tap | 2 x 2 | on/near essence node |
| Essence Condenser | 3 x 3 | later |
| Bulk Hauler Dock | 5 x 5 | no trains, late bulk transfer |

### Transport footprints

```text
Steam Cart Stop, 3 x 2
LLL
WWW

Cable-Haul Freight Skid Dock, 5 x 3
DDDDD
L...L
WWWWW

Overhead Chainway Anchor, 2 x 2 surface posts plus overhead path
AA
AA

Pneumatic Vault Tube Hub, 4 x 4
PPPP
PDDP
PDDP
PPPP

Aether-Lift Gantry, 4 x 4
EEEE
E..E
E..E
EEEE
```

### Underground steam layer

Surface:

```text
..M....
..M....
.......
..C....
```

Underground steam layer:

```text
..P....
..P....
..P....
..P....
```

Rule:

- Surface remains readable for belts, machines, workers, and lanes.
- Underground layer shows boiler-to-machine connectivity.

### UI layout wireframe

```text
+--------------------------------------------------------------------------------+
| TWB Trenchworks | Food | Worker | Front | Coal | Steam | Essence | Tick | Speed |
| OUR BASE [#######---]     PRESSURE / CONTACTS / BOMBARDMENT     ENEMY [####---] |
+-------------------------------------------------------------+------------------+
|                                                             | Tracker          |
|                                                             | [OVR][LOGI][WAR] |
|                                                             |                  |
|                    ACTIVE GRID VIEW                         | Selected team    |
|              Factory 500x500 or War 1000x600                | Reason string    |
|                                                             | Bottlenecks      |
|                                                             | Supplies         |
|                                                             | Logs             |
+-------------------------------------------------------------+------------------+
| (WAR/BUILD) (TOOLS...) (DIRECTIONS...) (RECIPES/TEAMS...) (LAYERS...) (PAUSE)  |
+--------------------------------------------------------------------------------+
```

### Example factory layout with footprint/routing pressure

This example deliberately shows awkward routing. The difficulty is not just production arithmetic; it is fitting footprints, belts, pipes, depots, loaders, and access lanes into available space.

```text
Surface layer, 22 x 14

00  R E > > > L A A . W W . R E > > L M M . .
01  . . . . . . A A . W W . . . . . . M M . .
02  . . . . . . > > > > > > > > > L S S . . .
03  R E > > L F F F F . W W . . . . S S . . .
04  . . . . . F F F F . W W . C C C . . . . .
05  . . . . . F F F F . W W . C C C . . . . .
06  . . . . . . . . . . W W . C C C . . . . .
07  R E > > > L K K . . W W . . . . D D D . .
08  . . . . . . K K . . W W . > > > D D D . .
09  . R E > > > > > > > > > > ^ . . D D D . .
10  . . . . . . . . . . W W . ^ . . . . . . .
11  . . . A A A . . . . W W . ^ . . R E > > .
12  . . . A A A > > > > > > > ^ . . . . . . .
13  . . . A A A . . . . W W . . . . . . . . .

R = resource node
E = extractor
F = 4x3 farm footprint
C = 3x3 boiler footprint
K = kitchen/canner
M = powered machine
A = workshop/assembler footprint
S = storage
D = 3x3 shipping depot
L = loader
W = worker/access lane
> ^ = belts
```

Pressure points:

- Farm occupies 4 x 3 and blocks a straight belt path.
- Boiler occupies 3 x 3 and needs coal, water, access lane, and underground pipe output.
- Shipping depot occupies 3 x 3 and needs inbound belts plus worker access.
- Worker lanes compete with belts; blocking them should slow manual tasks.
- Loaders are required where belts meet large buildings.
- Powered machine needs surface input and underground steam connection.
- Storage buffers take real space and can rescue or clutter routing.

Underground steam layer for the same layout:

```text
00  . . . . . . . . . . . . . . . . . P P . .
01  . . . . . . . . . . . . . . . . . P P . .
02  . . . . . . . . . . . . . . . . . P P . .
03  . . . . . . . . . . . . . . . . . P . . .
04  . . . . . . . . . . . . . C C C P P . . .
05  . . . . . . . . . . . . . C C C P . . . .
06  . . . . . . . . . . . . . C C C P . . . .
07  . . . . . . P P . . . . . . . . P . . . .
08  . . . . . . P P P P P P P P P P P . . . .
09  . . . . . . . . . . . . . . . . . . . . .
10  . . . . . . . . . . . . . . . . . . . . .
11  . . . . . . . . . . . . . . . . . . . . .
12  . . . . . . . . . . . . . . . . . . . . .
13  . . . . . . . . . . . . . . . . . . . . .
```

### Example war sector with routes and contact

```text
Player left, enemy right

00  Q Q Q Q . . . . . . . . . . . . . . . . .
01  Q Q Q Q . . . . . . . . . X X . . . . . .
02  Q Q Q Q . . . u 1 . . . X X . . e . . . .
03  Q Q Q Q . . . . u . . . . . . . . . . . .
04  . . . . . . . . . . . . . . . . . . . . .
05  . . . . T T T T T . . . . . . . . . . . .
06  . . . . T . . . T . . . . G G . . . . . .
07  . . . . T . H . T T T . . G T . . . . . .
08  . . . . T . . . . . T . . . . . . . . . .
09  . . . . T T T T T T T . . . . . . . . . .

Meaning:
- Scout team is ahead, near suspected/confirmed contact.
- Existing trench network exists only because prior contact happened.
- Communication trench leads back toward base.
- MG nest is attached to consolidated trench sector.
- Wire/obstacles shape movement.
```

## Asset Strategy

First visual pass should use colored boxes, tiny glyphs, outlines, and layer tinting. Resist bespoke art until mechanics stabilize.

### First-pass visual language

Factory:

- Resources: earthy square with two-letter label.
- Belts: dark grey strips with direction arrows.
- Workers: small moving dots with job color.
- Farms: green-brown block with essence accent.
- Coal/steam: black/grey/orange.
- Steam pipes: underground brass/copper line.
- Essence: cyan/teal glow, used sparingly.
- Factory construction: steel grey and yellow hazard edge.
- Trench construction: tan/brown/plank color.

War:

- Player units: blue-green.
- Enemy units: muted red.
- Scout: small triangle/eye glyph.
- Leader: bordered square or chevron.
- Medic: pale cross marker.
- Engineer/sapper: tool glyph.
- Cover: darker rim or half-cell marker.
- Crouched/pinned: smaller/lower icon.
- Contact: orange pulse.
- Trenches: brown recessed cells.
- Wire: black X pattern.
- MG/artillery: dark metal blocks with arc/range overlay.
- Supply routes: green pulses.
- Danger/suppression: orange-red heat overlay.

### Tier language

| Tier | Visual cue |
|---|---|
| Tier 1 manual | wood, cloth, hand tools, small footprints |
| Tier 2 belted | belts, rollers, simple iron, clearer arrows |
| Tier 3 steam | brass/copper pipes, gauges, pressure accents |
| Tier 4 arcane | ward plates, essence glow, stabilized shapes |
| Tier 5 siege | heavy black steel, warning bands, harmonic/ritual accents |

Later asset plan:

- Replace boxes with simple sprite icons after loops stabilize.
- Keep grid footprint readable even with art.
- Use silhouettes and color accents for function before decorative detail.
- Add animation only where it communicates state: working, blocked, powered, starved, firing, suppressed, resupplying.

## Risks, Dependencies, And Performance Hotspots

### Design risks

- Too many resources early will bury the player.
- Too few resources will make factory expansion feel free.
- Essence may become over-centralized because it feeds food and magic.
- Steel may choke every path unless diagnostics are excellent.
- Workers can become clerk-work if too individually managed.
- Supply teams can feel fake if goods teleport or tedious if every trip is manual.
- No-build-before-contact is strong, but early war needs good scouting feedback or it will feel empty.
- Team abstraction can hide important member behavior unless inspectors are built early.
- Artillery and MGs can dominate unless supply, spotting, counters, posture, and cover matter.

### Technical dependencies

- Catalog ids must stabilize before save files matter.
- Simulation/UI command boundary should be introduced before UI grows.
- Test harness should exist before large refactor.
- Contact eligibility must land before serious fortification work.
- Supply request system should land before emplacements.
- Steam network should land before powered factory expansion.

### Factory performance hotspots at 500 x 500

Factory grid has 250,000 cells.

Avoid:

- scanning every cell every tick,
- per-cell allocation in UI draw,
- pathfinding every worker every frame,
- rebuilding all network ids every tick,
- drawing every grid cell at high zoom-out.

Use:

- active entity lists,
- sparse dictionaries for non-empty layers,
- dirty rectangles/dirty networks,
- chunked grid rendering,
- update cadence by system,
- pooled lists for transfers/routes.

Hot systems:

- belts/transfers,
- workers/porter pathing,
- steam network connectivity,
- construction job search,
- UI overlays.

### War performance hotspots at 1000 x 600

War grid has 600,000 cells.

Avoid:

- scanning all cells each strategic second,
- checking every unit against every other unit for contact,
- rebuilding full influence maps too often,
- full pathfinding per team per tick,
- rendering all active overlays naively.

Use:

- spatial hashing or grid buckets for unit proximity,
- active cell lists,
- sector-level influence maps,
- local cell queries around teams,
- dirty influence regions,
- BFS/A* only on demand and cached by route request,
- staggered AI updates,
- compact cell data arrays.

Hot systems:

- contact detection,
- line of sight/fog,
- influence maps,
- route planning,
- trench network connectivity,
- supply route validation,
- overlay rendering.

### Memory concerns

For 600,000 war cells, class-per-cell is convenient but can become heavy. Current prototype uses class objects and is acceptable for first slice, but later should consider compact structs/arrays for hot fields:

```text
byte obstacleType
byte coverType
byte contactEligibility
byte trenchStage
short networkId
short occupantOrMinusOne
ushort contactHeat
byte scoutedFlags
```

Keep rich objects only for active cells, teams, members, fortifications, supply requests, and emplacements.

## Recommended First Coding Milestone

Recommended next milestone: **Catalog, Worker-Food-Steam First Slice**.

Do not begin by adding every unit and emplacement. The present prototype already has visible war activity. The weakest foundation now is that the factory economy is still too abstract for the designed system.

### Milestone goal

Make factory survival and expansion visibly depend on food, coal/steam, essence, workers, and build goods while preserving current playable war shipment loop.

### Code tasks

1. Add in-code catalog definitions for current and new resources/items/recipes.
2. Add Food, Coal, Water, Essence, RawFood, WorkerMeals, Steam.
3. Add worker pool with Porter, Farmer, MachineOperator.
4. Add worker hunger/fatigue and throughput slowdown.
5. Add Fungal Loam, Water, Coal, Essence, Timber, Heavy Scrap, Stone/Clay, Fiber nodes.
6. Add Mudbed Farm: Fungal Loam + Water + Essence + Farmer labour -> Raw Food.
7. Add Worker Meals and Basic Rations split.
8. Add allocation state: Worker / Front / Reserve / Factory.
9. Add Small Boiler: Coal + Water -> Steam.
10. Add underground steam pipe/adjoining prototype.
11. Add one steam-powered machine blocked by missing steam.
12. Add first factory build goods: Steel Plates, Machine Parts, Conveyor Parts, Boiler Parts.
13. Add right tracker diagnostics for hunger, farm input, coal, steam, essence, and missing build goods.
14. Keep old Ammo/Trench/Rations/Medical shipment path operational.

### Acceptance checks

- Existing smoke test still passes or is updated with equivalent compatibility checks.
- Workers consume food.
- Hunger visibly slows at least one production or hauling path.
- Farm stalls with missing essence.
- Boiler stalls with missing coal or water.
- Steam-powered machine stalls if disconnected.
- At least one machine/conveyor build is blocked by missing build goods and says exactly what is missing.
- Current war still receives supply crates.
- No fortification behavior is changed in this milestone.

## Report-required Worker Notes

### What changed

- Wrote this implementation-planning and wireframe report.
- No Unity source was changed.
- No permanent memory was changed.

### Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-full-implementation-plan-and-wireframes.md`

### Tests/checks run

- Read required vault context:
  - `memory/hot.md`
  - `memory/index.md`
  - `memory/wiki/game-dev/project-hierarchy.md`
- Read requested primary design source:
  - `memory/short-term/2026-05-16-twb-trenchworks-production-military-system-consolidated-design.md`
- Read requested implementation context:
  - `TWB-TrenchWorks/README.md`
  - `memory/short-term/2026-05-16-twb-trenchworks-playtest-stabilization-report.md`
  - `memory/short-term/2026-05-16-twb-trenchworks-war-agent-first-slice-implementation-report.md`
  - `memory/short-term/2026-05-16-twb-trenchworks-organic-war-ai-research-report.md`
  - `memory/short-term/2026-05-16-twb-trenchworks-factory-construction-materials-addendum.md`
  - `memory/short-term/2026-05-16-twb-trenchworks-worker-food-coal-essence-addendum.md`
- Read optional code context read-only:
  - `Assets\Scripts\Simulation\TrenchworksSimulation.cs`
  - `Assets\Scripts\Unity\PrototypeBootstrap.cs`
  - `Assets\Scripts\Editor\TrenchworksProjectSetup.cs`
- Checked that the output report did not already exist before writing.
- Checked Unity project git status attempt; project folder is not currently a git repository.

### Cleanup performed

- No temporary files, screenshots, throwaway logs, or dev artifacts were created.

### Risks

- This plan is intentionally concrete, but some class names should still be adapted by the implementation worker if they conflict with new local patterns.
- The current prototype is monolithic; extraction should be incremental, with smoke tests protecting behavior.
- The next worker should avoid trying to implement production, team AI, trench networks, and emplacements in one pass. That would be a buffet plate with plumbing on it.

### Memory-worthy notes

- Recommended next coding milestone is Catalog, Worker-Food-Steam First Slice.
- Preserve current playable prototype and smoke test while adding deeper production systems.
- Add catalog/data shape before expanding resource and team complexity.
- Implement workers, food split, essence-fed farm, coal boiler, and underground steam layer before full military expansion.
- Convert entry-lane choice from scenario reset to per-team spawn orders after team layer exists.
- Enforce no fortifications before contact as an explicit testable rule.
- Start with colored boxes/icons and layer overlays; defer bespoke art.

### Follow-up recommendations

- Hydrate the next implementation worker for the recommended first coding milestone only.
- Require tests for catalog ids, worker hunger, essence farm stall, boiler/steam stall, and current shipment compatibility.
- After that milestone passes, commission the team-spawning layer as a separate bounded pass.
