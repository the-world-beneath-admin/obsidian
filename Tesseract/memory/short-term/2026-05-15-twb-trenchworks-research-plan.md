# 2026-05-15 TWB Trenchworks Research And Creation Plan

## Scope

Standalone TWB-tagged Unity 2D game under The World Beneath umbrella.

This is not a browser game, not Phaser/Vite, and not a World Key unless Bob later reclassifies it.

Research/planning only. No implementation was performed.

## User Input Captured

- Decision - Phase 1 is player versus NPC.
- Decision - The player supplies one faction at first.
- Decision - Multiplayer is desired eventually, but not in phase 1.
- Decision - No shared account systems or pet systems in phase 1.
- Decision - War outcomes should be approximately 80 percent supply-driven and 20 percent random.
- Hypothesis - The player should be able to choose which soldiers or unit packages to spawn into battle.
- Hypothesis - Command units should be special autonomous leaders that assemble teams of non-command units, then pursue goals such as pushing forward, building an outpost, reinforcing a trench, or digging a tunnel.

## Summary Recommendation

Build TWB Trenchworks as a simulation-first Unity 2D game with two linked simulation domains:

1. A factory/logistics grid where the player builds production chains.
2. A war grid where autonomous AI factions fight, dig, build trenches, and consume supplies.

The core rule should be: the player does not manually fight. The player designs the industrial machine, chooses what kind of soldiers and command units to send, and then watches the autonomous war engine interpret those supplies and units.

Recommended technical shape:

- Pure C# simulation layer as the source of truth.
- Unity rendering, input, UI, audio, and animation as presentation around that simulation.
- Hybrid grid rendering: Tilemaps for static ground, terrain, trench, and underground visualization; custom pooled renderers for dynamic belts, machines, items, units, mission arrows, and overlays.
- Data-driven definitions via ScriptableObjects or JSON-backed catalogs, converted into immutable runtime data before simulation starts.
- Fixed-step simulation tick with deterministic seeded randomness, event logs, and debug overlays from the first prototype.

Recommended design posture:

- Copy Factorio's principles of readable throughput, bottleneck discovery, automation pressure, and spatial logistics.
- Do not clone Factorio's exact content, science progression, alien pressure, belt lane complexity, or late-game sprawl.
- Make the war the reason the factory matters. A clever factory should produce visible changes at the front.

Small, dignified pause. This is the sensible shape of the thing.

## Factorio Principles Studied

Sources consulted include the official Factorio Wiki pages for belt transport, inserters, crafting, time/ticks, and storage:

- https://wiki.factorio.com/Transport_network
- https://wiki.factorio.com/inserters
- https://wiki.factorio.com/crafting
- https://wiki.factorio.com/Time
- https://wiki.factorio.com/Storage

### Belts

Useful principles:

- Belts are the simplest visible transport system.
- Throughput is the core design pressure: speed, density, and number of paths determine how much material reaches a destination.
- Belts make bottlenecks visible because items back up or starve downstream machines.
- Split/merge decisions create compact spatial puzzles.
- Underground transport is valuable because it lets flows cross without destroying layout readability.

Recommended adaptation:

- Phase 1 should use one-lane or simplified two-lane belts with fixed item spacing.
- Belts should show visible item motion, but exact Factorio-level lane physics should wait.
- Use simple belt throughput numbers: items per second per belt tier.
- Include straight belts, corners, and basic split/merge if affordable.
- Postpone advanced lane balancing, priority splitters, circuit controls, underground belt weaving, and belt-car style tricks.

### Inserters

Useful principles:

- Inserters are the controlled handoff between belts, machines, storage, and shipping.
- Transfer speed and reach determine whether a machine is saturated or starved.
- Inserters make factory layouts legible because the player can see where an item is intended to go.

Recommended adaptation:

- Use inserters as adjacent-cell transfer devices with cooldown, direction, optional filter, and stack size.
- In phase 1, inserters should move one item at a time and expose "waiting for input", "target full", and "output blocked" states.
- Do not implement Factorio's full inserter swing geometry or all inserter variants yet.

### Machines And Recipes

Useful principles:

- Automated production is recipe-driven: input items plus craft time produce output items.
- Machine craft speed and recipe craft time create production ratios.
- Intermediate products are where the factory becomes interesting.

Recommended adaptation:

- Each machine should have a selected recipe, internal input buffer, craft timer, and output buffer.
- Phase 1 needs only a few machine classes: extractor/miner, processor, assembler, crate packer, and shipping depot.
- Recipes should support item quantities, craft duration, output quantities, and category tags.
- Ratios should be simple enough to reason about without calculators at first.

### Storage And Buffers

Useful principles:

- Buffers smooth intermittent demand.
- Too much storage can hide bottlenecks and make the factory feel dead.
- Storage is also useful as a player-readable checkpoint in a chain.

Recommended adaptation:

- Include small crates/storage bins in phase 1.
- Keep capacities low and readable.
- Show inventory counts and flow rate.
- Use shipping stockpiles as the bridge between factory output and war needs.

### Throughput, Bottlenecks, And Ratios

Useful principles:

- The player should be able to diagnose why production is slow.
- A good factory game makes constraints visible: missing input, full output, insufficient transport, wrong ratio, or shipping starvation.

Recommended adaptation:

- Every dynamic entity should have a plain state: working, starved, blocked, idle, or disabled.
- Add debug overlays early:
  - items per second by belt segment
  - machine utilization percentage
  - input starvation
  - output blockage
  - shipping stockpile trend
  - war supply consumption trend

### Blueprint And Layout Thinking

Useful principles:

- Factory players think in repeatable modules.
- Copying layouts and reading production blocks is part of the joy.

Recommended adaptation:

- Phase 1 should support grid-aligned placement and clean rotation.
- Ghost previews, copy/paste, blueprint books, and mass construction should be postponed.
- Leave architecture space for future blueprint serialization.

## What To Copy As Principle, Not Clone

Copy:

- Visible logistics.
- Grid clarity.
- Automation as the central verb.
- Throughput as a design language.
- Bottleneck diagnosis.
- Spatial planning.
- The satisfaction of improving a production line and seeing downstream systems respond.

Do not copy:

- Factorio's premise, aliens, science-pack arc, rocket goal, exact recipe tree, exact belt mechanics, exact machines, or art identity.
- Its late-game scale before this game's core factory-war loop is proven.
- Its amount of player-authored complexity in milestone 1.

TWB Trenchworks should become: "I build the supply machine, select the force composition, and the front reacts." That is related to Factorio, but it has its own spine.

## Unity Architecture Recommendation

Unity sources consulted:

- Unity Tilemaps: https://docs.unity.cn/Manual/Tilemap.html
- Unity Tilemap Collider 2D: https://docs.unity.cn/2023.2/Documentation/Manual/class-TilemapCollider2D.html
- Unity ScriptableObject API: https://docs.unity.cn/ScriptReference/ScriptableObject.html
- Unity JSON Serialization: https://docs.unity.cn/6000.1/Documentation/Manual/json-serialization.html
- Unity fixed updates: https://docs.unity.cn/6000.0/Documentation/Manual/fixed-updates.html

### Core Rule

Do not let Unity GameObjects become the simulation source of truth.

The simulation should live in plain C# data and systems. Unity should render it, collect input, and show UI. This is especially important because eventual multiplayer will be much easier if the game already works as deterministic command inputs into a simulation.

### Proposed Runtime Layers

Core simulation:

- `Catalog`
- `FactoryWorld`
- `FactoryGrid`
- `LogisticsSystem`
- `MachineSystem`
- `ShipmentSystem`
- `WarWorld`
- `WarGrid`
- `WarLayerSystem`
- `CommandUnitSystem`
- `UnitSystem`
- `MissionSystem`
- `CombatResolver`
- `BattleReportSystem`
- `SimulationClock`
- `SaveGameDto`

Unity presentation:

- Scene bootstrapper
- Input/placement controller
- Camera controller
- Factory renderer
- Belt/item renderer
- Machine renderer
- War map renderer
- Unit renderer
- Minimap renderer
- UI panels
- Debug overlay views

### Tilemap vs Custom Grid vs Hybrid

Recommendation: hybrid.

Use Tilemap for:

- static terrain
- factory floor
- resource-node edge markings
- build-blocked cells
- war terrain
- trench cells
- tunnel/underground cells
- fog or ownership overlays where appropriate

Use custom grid data for:

- occupied cells
- machine footprints
- belt direction and contents
- item movement
- recipes and inventories
- unit positions
- command goals
- trench strength
- underground connections
- ownership/control values

Use custom pooled visual renderers for:

- moving belt items
- inserter arms
- machine animations
- unit icons/sprites
- command-unit team halos
- battle report pips
- mission arrows

Avoid using Tilemap Collider 2D as gameplay truth. Tilemap collision can be useful for player/camera boundaries, but factory and war simulation should use grid occupancy and pathing rules.

### Data-Driven Definitions

Use ScriptableObjects for designer-friendly definitions:

- item definitions
- recipe definitions
- machine definitions
- belt/inserter definitions
- resource-node definitions
- supply category definitions
- unit definitions
- command-unit definitions
- mission definitions
- faction definitions
- terrain/trench definitions

At runtime, convert those into immutable catalog records identified by stable string IDs.

Do not store mutable run state inside ScriptableObjects. Saves should store IDs and runtime state only.

### Save Model

Phase 1 save DTO should include:

- schema version
- game version
- random seed
- elapsed simulation tick
- selected faction
- factory grid size
- placed entities and their states
- inventories and belt contents
- resource-node remaining amounts if depletion is active
- shipping depot stockpile
- available unit spawn/requisition pool
- war grid state
- unit list
- command unit list
- active missions
- battle report log
- player settings needed to resume

Use JSON for prototype saves. Unity JsonUtility can handle simple structured data, but if dictionaries or polymorphic save records become awkward, use a clearer .NET JSON library rather than bending the data into unlovely shapes. A butler has standards.

### Tick/Update Model

Recommended simulation tick:

- Factory tick: 10 ticks per second for item movement, machines, inserters.
- War tactical tick: 2 to 5 ticks per second for unit movement and local combat.
- War strategic/mission tick: 1 tick per second or every N tactical ticks.
- Rendering: interpolated from latest snapshots/events.

Implementation principle:

- Unity frame time feeds an accumulator.
- The simulation advances by fixed steps.
- The renderer never changes simulation state directly.
- Player inputs become commands queued for the next simulation tick.
- Randomness uses a seeded simulation RNG, not arbitrary Unity random calls.

This prepares the project for future multiplayer by making "commands in, state out" the natural shape.

### Debug Overlays

Build debug overlays early, not as a luxury:

- grid coordinates
- cell occupancy
- pathing costs
- belt direction and flow
- items per second
- machine state
- machine utilization
- depot supply trends
- front line control
- trench strength
- tunnel network
- command unit mission state
- combat modifiers
- RNG contribution to battle outcomes

The front must feel alive, but it must also explain itself.

## Factory System Plan

### Factory Area Layout

Recommended first map:

- Rectangular build area.
- Resource nodes distributed along the outer edge.
- Central open grid for player machines and belts.
- Shipping depot in one corner or along one side.
- Player start near a small starter resource node and the shipping depot.

Suggested prototype scale:

- 48 x 32 or 64 x 40 factory cells.
- 4 to 6 edge resource nodes.
- 1 shipping depot.
- 1 initial tutorial-like production chain.

These sizes are placeholders, not final product memory.

### Resource Nodes

Resource nodes should be edge constraints rather than random interior clutter. This forces the player to pull inputs inward, combine them, then route outputs back to shipping.

Phase 1 resource candidates:

- ore/scrap
- timber
- cloth/fiber
- chemicals/sulfur
- coal/fuel if power or explosives are added later

Recommended MVP nodes:

- metal
- timber
- chemical

Keep names flexible until tone is decided.

### Machines

Phase 1 machine set:

- Extractor: pulls raw resource from an edge node.
- Processor: converts raw resource into usable material.
- Assembler: combines materials into supply goods.
- Packer: bundles goods into shippable supply crates.
- Storage bin: buffers items.
- Shipping depot: consumes supply crates and credits the player faction.

Possible initial recipes:

- metal ore -> metal plates
- timber -> boards
- metal plates + chemical -> ammo crate
- boards + metal plates -> construction crate
- cloth/fiber + chemical -> medical crate

The exact recipe tree should remain temporary until Bob/user decides tone and supply categories.

### Belts And Inserters

Phase 1 logistics:

- Belts move item stacks/icons cell by cell in a direction.
- Inserters move items between adjacent belt/machine/storage cells.
- Machines have input and output inventories.
- Storage bins have fixed capacity.
- Shipping depot accepts only shippable crates.

Recommended simplifications:

- No power network in phase 1.
- No fluids in phase 1.
- No trains/vehicles in phase 1.
- No robots in phase 1.
- No circuit network in phase 1.
- No complex two-lane belt balancing in phase 1 unless it emerges as cheap and safe.

### Power Or No Power

Recommendation: no power in milestone 1.

Reason:

- The first prototype already has two major systems: factory and war.
- Power would add another bottleneck system before the core "production changes the war" proof exists.
- Machines can simply run if supplied and unblocked.

Future power could become a meaningful layer:

- generators
- fuel supply
- overloading
- sabotage
- underground cable/tunnel risks
- battlefield artillery disrupting supply power

But not yet. Splendid restraint, sir.

### Shipping And Army Supply

The shipping depot should convert factory output into a faction supply ledger:

- ammo supply
- construction supply
- medical/ration supply
- optional later: artillery, fuel, morale, wire, tools

The ledger should feed:

- unit spawn/requisition availability
- combat readiness
- mission success probability
- trench/outpost build speed
- injury recovery
- morale/retreat thresholds

The player should see both:

- current stockpiles
- recent consumption

## Soldier Spawning And Requisition Plan

The user's new idea is strong: the player chooses which soldiers to spawn, then those soldiers know what to do.

Recommended form:

- The factory produces supplies.
- Supplies create requisition capacity.
- The player spends requisition capacity on unit packages or command units.
- Units enter the war at the player's HQ/reserve line.
- The player does not directly control them after deployment.

Phase 1 unit concepts:

- Rifle squad: general combat.
- Digger squad: trench and tunnel work.
- Engineer squad: outposts, wire, repairs, supports.
- Medic/orderly squad: recovery and morale.
- Runner/logistics squad: carries local front supplies.
- Command unit: assembles a team and pursues a mission.

Command unit behavior:

1. Spawn at HQ.
2. Evaluate available non-command units.
3. Assemble a mission team based on mission type and supply state.
4. Move to staging point.
5. Execute mission.
6. Report outcome.
7. Refit, request replacements, or choose a follow-up mission.

Example command missions:

- Push Forward: capture or contest cells toward the enemy.
- Build Outpost: create a fortified forward position.
- Extend Trench: improve defensive line and safe movement.
- Dig Sap/Tunnel: create underground approach.
- Reinforce Weak Front: move units to a threatened sector.
- Raid Supply: harass enemy outpost or tunnel.

Important guardrail:

- The player should influence intent and composition, not micro units.
- If command units act foolishly, the game needs battle reports explaining why.

## War Simulation Plan

### Core War Shape

Two factions start on opposite sides of a war grid.

Phase 1:

- Player-supported faction on one side.
- NPC faction on the other side.
- NPC has baseline supply generation or scripted supply pulses.
- Both factions use the same AI framework where possible.
- Player faction receives additional supplies and unit choices from the factory.

The war should be autonomous, readable, and inspectable.

### War Grid

Recommended war map:

- Long horizontal or vertical front.
- HQ/reserve zones at opposite edges.
- No man's land between them.
- Above-ground layer for movement, fighting, trenches, outposts, wire, craters.
- Underground layer for tunnels, dugouts, saps, and protected movement.

Suggested prototype scale:

- 64 x 24 or 80 x 32 cells.
- Coarse enough to read.
- Large enough for front movement and flanking choices.

### AI Faction Model

Use old-school game AI:

- finite state machines
- utility scoring
- simple pathfinding
- local mission selection
- explicit priorities

Avoid expensive black-box AI. The war must be debuggable.

Faction-level needs:

- hold HQ
- maintain a defensible trench line
- push toward enemy
- build outposts when supplies permit
- dig underground approaches
- reinforce weak sectors
- recover wounded/exhausted units
- attack when local strength is favorable

Unit-level needs:

- obey assigned mission
- seek cover/trench if under threat
- consume ammo and supplies
- retreat if morale collapses
- wait if path blocked
- report mission outcome

### 80 Percent Supply / 20 Percent Random

Use a deterministic weighted combat model with small seeded random variance.

Suggested combat score:

- 80 percent from legible factors:
  - ammo availability
  - relevant unit type
  - unit count/strength
  - trench/outpost cover
  - medical/ration support
  - morale/fatigue
  - command presence
  - terrain and layer advantage
  - local supply distance
- 20 percent from seeded variance:
  - weather/friction
  - confusion
  - luck
  - miscommunication
  - brave or poor local execution

Battle reports should expose this:

- "Advance stalled: ammo low, enemy trench cover high, command support absent. Random friction was minor."
- "Outpost held: construction supplies full, engineers present, medical support good. Random pressure was high but not decisive."

The player should never feel the game simply cheated.

### Supplies Consumed By War

Phase 1 supply categories:

- Ammo: improves attack/defense and keeps units fighting.
- Construction: builds trenches, outposts, tunnel supports, wire.
- Medical/Rations: improves recovery, morale, endurance.

Later supply categories:

- Shells/artillery
- Fuel
- Tools
- Signal equipment
- Winter/weather gear
- Morale goods
- Underground supports

### Battle Reports And Minimap

Factory screen should have a small war minimap:

- front line
- current player faction supply state
- recent battle markers
- active command missions
- warning markers for shortages

War screen should show:

- grid/layer toggle
- factions
- trench lines
- command unit teams
- mission arrows
- battle report feed
- selected sector details

Reports should be concise and explain cause/effect:

- supply change
- command mission launched
- trench built
- tunnel discovered
- attack won/lost
- outpost captured/lost
- unit shortage

## Above-Ground / Underground Layer Model

The layer model is central to the concept and should be represented in the data from the start, even if the first prototype uses simple visuals.

### Above-Ground Layer

Cell data:

- terrain type
- controlling faction
- cover value
- trench type/strength
- outpost level
- wire/obstacle
- crater/difficult terrain
- exposed danger score
- occupying units
- current combat state

Above-ground verbs:

- move
- attack
- dig trench
- build outpost
- repair fortification
- reinforce
- retreat

### Underground Layer

Cell data:

- tunnel state: none, dug, reinforced, collapsed
- controlling faction or unknown
- access shaft
- support quality
- concealment value
- collapse risk
- occupying units
- connection directions

Underground verbs:

- dig
- reinforce
- move hidden
- establish dugout
- prepare sap
- emerge/assault
- detect enemy tunnel
- collapse/repair

### Layer Interactions

Interactions:

- Trenches and outposts can require underground dugouts for higher durability.
- Digger/engineer units can create tunnels beneath no man's land.
- Underground movement can bypass exposed surface danger.
- Surface shelling can damage underground supports.
- Underground emergence can create flanking pressure.
- Poorly supplied tunnels risk collapse.

Phase 1 should include:

- data model for both layers
- layer toggle on war screen
- simple dig/tunnel path mission
- simple trench/outpost build mission
- limited combat modifiers from underground approaches

Postpone:

- deep underground tactical combat
- complex tunnel detection
- gas/flooding/collapse simulation
- multi-depth underground maps

## Data Model And Simulation Tick Plan

### Core IDs

Use stable string IDs for:

- items
- recipes
- machines
- belts
- inserters
- supply categories
- unit types
- command unit types
- mission types
- terrain types
- factions

### Factory Runtime Data

Suggested records:

- `FactoryCell`
- `PlacedEntity`
- `BeltState`
- `InserterState`
- `MachineState`
- `InventoryStack`
- `RecipeProgress`
- `ResourceNodeState`
- `ShippingDepotState`

### War Runtime Data

Suggested records:

- `WarCellSurface`
- `WarCellUnderground`
- `FactionState`
- `UnitState`
- `CommandUnitState`
- `MissionState`
- `SupplyLedger`
- `BattleEvent`
- `FrontSectorSummary`

### Simulation Events

Emit events for:

- item moved
- machine craft started/completed
- machine starved/blocked
- supply shipment received
- unit requisition unlocked
- unit spawned
- command unit assembled team
- mission started/completed/failed
- trench/outpost/tunnel changed
- combat resolved
- battle report created

Events should drive UI, logs, and debug panels.

### Simulation Tests To Plan

When implementation begins, add pure C# tests early for:

- recipe completion
- machine starvation/blockage
- belt movement
- inserter transfer
- shipping ledger updates
- unit requisition cost checks
- command unit team assembly
- mission selection
- combat resolver supply weighting
- seeded RNG repeatability
- save/load round trip

No tests were created in this research phase.

## First Playable Milestone

Goal: prove that factory quality changes war outcomes.

### Included Systems

Factory:

- single Unity 2D factory scene/screen
- grid placement
- edge resource nodes
- extractors
- belts
- inserters
- processors/assemblers
- storage bins
- shipping depot
- 3 shippable supply crates
- basic bottleneck states

War:

- second war screen or panel
- minimap on factory screen if cheap
- two factions
- player-supplied faction vs NPC faction
- simple NPC baseline supply
- surface and underground grid data
- trench/outpost construction
- simple tunnel/sap mission
- autonomous squads
- command units that assemble teams
- player unit/requisition selection
- 80/20 supply/random combat resolver
- battle reports

Technical:

- simulation/render separation
- fixed-step tick
- data catalogs
- seedable RNG
- save/load prototype if time allows
- debug overlay for flow and war state

### Prototype Flow

1. Player starts with a small open build grid.
2. Edge resource nodes provide raw materials.
3. Player places extractors, belts, inserters, and machines.
4. Factory produces ammo, construction, and medical/ration crates.
5. Shipping depot sends crates to player faction.
6. Supply ledger unlocks or improves unit requisitions.
7. Player chooses units or command units to send.
8. Command units assemble teams and pursue missions.
9. War screen shows trenches, movement, missions, and outcomes.
10. Battle reports explain why the front changed.

### Success Criteria

The milestone succeeds if:

- A player can build a small supply chain without developer intervention.
- The chain can visibly bottleneck and be improved.
- Shipping more/better supplies changes combat readiness.
- Choosing different unit/command packages creates different war behavior.
- Command units autonomously form teams and pursue readable missions.
- War outcomes feel mostly supply-driven with some seeded uncertainty.
- The player can understand at least one lost fight and one won fight from battle reports.
- The prototype can run for at least 30 minutes without simulation drift or obvious state corruption.

## Systems Explicitly Postponed

Postpone:

- multiplayer
- online account integration
- shared pets
- shared inventory
- backend APIs
- World Key classification
- power grid
- fuel economy unless chosen as a supply category later
- full tech tree
- research/science progression
- advanced belt lanes and priority splitters
- circuit networks
- trains/vehicles/robots
- blueprints and copy-paste
- full production-ratio tooling
- procedural campaigns
- rich story campaign
- complex underground combat
- artillery simulation
- weather simulation
- detailed soldier animation
- large-scale pathfinding optimization
- mod support
- Steam/store packaging decisions

## User Decisions Needed Before Implementation

Needed soon:

- Tone: grim WW1, stylized TWB weird-fiction, lighter factory-toy abstraction, or another blend.
- Victory condition: destroy enemy HQ, control territory, survive timed offensive, supply score, campaign objectives, or stalemate score.
- Session shape: short scenario, long campaign, endless war, roguelite fronts, or sandbox.
- Unit roster for milestone 1: confirm whether rifle/digger/engineer/medic/runner/command is the right starting set.
- Command unit control level: player picks mission directly, command unit chooses mission autonomously, or player sets broad doctrine.
- Resource naming: realistic war materials or TWB-flavored materials.
- War view style: abstract board-game icons, small soldiers, or stylized tactical map.
- Multiplayer destination: eventual synchronous PvP, co-op supply factory, asynchronous front competition, or another shape.

Not needed for phase 1:

- shared account integration
- pets
- backend identity
- cloud saves
- production deployment

## Risks

- Scope risk - This is really two games coupled together: factory builder and autonomous war sim. The first milestone must stay narrow.
- Clone risk - Factorio is useful as a systems reference, but copying content or exact mechanics would weaken the project's identity.
- Opaqueness risk - Autonomous command units could frustrate the player if their goals and failures are not inspectable.
- Randomness risk - The 20 percent random factor must be explained through battle reports or it will feel unfair.
- Tilemap misuse risk - Tilemaps are good presentation tools, but poor primary storage for dynamic simulation state.
- Multiplayer future risk - If the prototype uses arbitrary frame-based state mutation now, later multiplayer will be much harder.
- Balance risk - If supplies are too strong, war becomes deterministic accounting; if too weak, factory work feels irrelevant.
- UI risk - Factory and war screens can overload the player. Start with plain readable panels before flourishes.
- Pathfinding risk - Many autonomous units can become expensive. Use coarse grids, sector summaries, and capped unit counts early.
- Theme risk - Real trench-war tone can become grim quickly. The final tone decision matters before art and copy.

## Memory-Worthy Notes For Bob

- TWB Trenchworks remains a standalone Unity 2D game under The World Beneath umbrella.
- It is not a browser game, not Phaser/Vite, and not a World Key at this time.
- Phase 1 should be player versus NPC.
- The player supplies one faction in phase 1.
- Multiplayer is desired later but should not be built in phase 1.
- No shared account systems or pet systems should be included in phase 1.
- War outcome target is approximately 80 percent supply-driven and 20 percent seeded random variance.
- Player unit choice should be treated as requisition/spawn strategy, not direct tactical control.
- Command units are promising: they can assemble non-command units into autonomous mission teams.
- Recommended architecture is pure C# simulation plus Unity presentation.
- Recommended rendering approach is hybrid Tilemap/custom grid.
- Recommended milestone is a small factory feeding ammo/construction/medical supplies into an autonomous two-layer trench-war sim.

## Do-Not-Promote Notes

- Specific recipe names and resource names in this report are placeholders.
- Suggested grid sizes are planning estimates, not final design decisions.
- Suggested class/module names are architecture notes, not created code.
- Unit roster names are provisional.
- No Unity project files, scripts, scenes, assets, or prototype files were created by this worker.
- The public research sources are useful system references, not TWB design authority.
- The "small, dignified pause" joke is not a design principle, tragic though that may be.

## Next Recommended Gate

Bob/orchestrator should review this report before implementation.

Recommended next gate:

1. Promote only durable decisions into permanent Obsidian memory.
2. Ask the user for the remaining tone, victory condition, session shape, and command-control decisions.
3. Create a narrow implementation brief for a Unity 2D prototype.
4. Only then hydrate an implementation worker.

Implementation should begin with the simulation skeleton and debug views, not art polish.

## Sources Read

Required project memory:

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\AGENTS.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\shared-platform\overview.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\shared-platform\inventory-boundaries.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\twb-trenchworks\overview.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\twb-trenchworks\open-questions.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\twb-trenchworks\research-plan.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`

External references:

- Factorio belt transport system: https://wiki.factorio.com/Transport_network
- Factorio inserters: https://wiki.factorio.com/inserters
- Factorio crafting: https://wiki.factorio.com/crafting
- Factorio time/ticks: https://wiki.factorio.com/Time
- Factorio storage: https://wiki.factorio.com/Storage
- Unity Tilemaps: https://docs.unity.cn/Manual/Tilemap.html
- Unity Tilemap Collider 2D: https://docs.unity.cn/2023.2/Documentation/Manual/class-TilemapCollider2D.html
- Unity ScriptableObject API: https://docs.unity.cn/ScriptReference/ScriptableObject.html
- Unity JSON Serialization: https://docs.unity.cn/6000.1/Documentation/Manual/json-serialization.html
- Unity fixed updates: https://docs.unity.cn/6000.0/Documentation/Manual/fixed-updates.html
