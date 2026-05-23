# 2026-05-16 TWB Trenchworks Crafting And Logistics Design Report

## Scope

Standalone Unity 2D TWB Trenchworks prototype under The World Beneath umbrella.

This is a design-only worker report. No code was implemented. This report does not cover The World Beneath main Unity game, Glassroot Garden, The Alchemy Lab, TWB-Marketing, shared platform/accounts, pets, sprite-sheet automation, multiplayer, or production art.

## 1. Design goals and constraints

The factory should feel like a dark WW1 industrial war machine, not a generic crafting table parade. The player is building the supply organism that keeps one side alive long enough to annihilate the enemy base.

Design goals:

- Build a 5-tier production ladder that begins with people carrying items by hand and grows into grim industrial logistics.
- Preserve the locked direction: dark tone, WW1-level technology, magic, steampunk-esque robotics, phase-one player versus NPC, supply-driven war outcomes, and eventual base destruction through bombardment.
- Supply the war machine with bodies/manpower, ammunition, food, energy, trench/construction materials, medical support, machine/robotics support, and bombardment supplies.
- Make logistics legible: every war advantage should trace back to visible factory throughput.
- Keep the prototype simulation-first. Items, recipes, machines, transport, war demands, and shortages should be plain data feeding deterministic/semi-deterministic tick systems.
- Avoid final-art thinking. Use readable names, simple icons, and diagnostics before polishing the fiction.

Constraints:

- Tier 1 transport must be people walking/carrying goods manually.
- Conveyors begin in Tier 2.
- Tier 4 or Tier 5 must provide no-train bulk transport across the construction area.
- Trains are explicitly out.
- The current prototype already uses belts for its proof loop. Do not delete that work. Treat the next design step as adding progression gates and transport tiers around the existing concept.
- Avoid multiplayer, shared accounts, pets, and unrelated TWB main-game systems.

Pushback:

- Five tiers plus 10+ inputs can easily become mush. The first playable slice should not expose every tier at once. Design the whole ladder now, but implement only a narrow vertical chain first.

## 2. The 5 crafting tiers

### Tier 1 - Hand War Economy

Theme: muddy depots, hand benches, stretcher lines, ration sacks, scrap piles, and people walking things from place to place.

Player fantasy:

- The war starts with labor, exhaustion, and bad tools.
- Every item has to be carried by a porter, handcart, stretcher crew, or quartermaster runner.

Primary machines:

- Scavenger Post
- Timber Yard
- Field Kitchen
- Handloading Bench
- Aid Tent
- Quartermaster Table
- Muster Tent
- Tool Bench

Core outputs:

- Loose cartridges
- Basic ration bundles
- Splints and bandages
- Timber planks
- Sandbag bundles
- Replacement manpower tokens
- Tool bundles

Mechanical identity:

- Low throughput.
- Workers fatigue.
- Items can be misplaced or delayed.
- Good for tutorial and early bottleneck clarity.
- War side receives trickles, not streams.

### Tier 2 - Belted Workshop Line

Theme: conveyors, crank presses, sorting bins, mechanical mixers, small furnaces, belt-fed packaging.

Player fantasy:

- The first real factory appears.
- The player stops hauling every crate by hand and starts laying belts.

Primary machines:

- Conveyor Belt
- Loader/Unloader
- Sorter Gate
- Crusher
- Powder Mill
- Cartridge Press
- Ration Canner
- Bandage Loom
- Sawmill
- Wire Twister
- Small Boiler

Core outputs:

- Ammo Crates
- Ration Crates
- Medical Crates
- Trench Material Crates
- Wire Coils
- Boiler Fuel

Mechanical identity:

- Conveyors begin here.
- Throughput becomes spatial.
- Basic sorting, merging, and storage problems begin.
- Existing prototype recipes fit this tier cleanly.

### Tier 3 - Steam Yard And Chemical Works

Theme: steam pressure, chemical vats, coal smoke, pneumatic tools, heavier shells, organized replacement pipelines.

Player fantasy:

- The factory becomes a war yard rather than a workshop.
- The player builds sustained supply, not just crates.

Primary machines:

- Steam Engine House
- Pressure Pipe Junction
- Chemical Vat
- Shell Forge
- Fuse Bench
- Uniform Stitchery
- Muster Barracks
- Field Hospital
- Concrete Mixer
- Repair Bay
- Signal Bench

Core outputs:

- Shell Crates
- Fuse Assemblies
- Concrete Revetment Packs
- Field Hospital Kits
- Replacement Squads
- Signal Kits
- Steam Cells
- Repair Kits

Mechanical identity:

- Energy starts to matter as a production support input.
- Manpower becomes a produced war supply, not a free number.
- Medical and food supplies begin converting wounded/fatigued units back into useful units.
- War supply categories should split beyond the current four prototype crates.

### Tier 4 - Arcane Industrial Works

Theme: aether coils, clockwork haulers, walking cranes, soul-safe wards, brass automata, ugly war miracles.

Player fantasy:

- The TWB twist becomes mechanical.
- Magic boosts logistics, but creates strain, instability, or contamination risks.

Primary machines:

- Aether Condenser
- Spark Dynamo
- Clockwork Assembly Bay
- Servo Foundry
- Warded Storage Vault
- Siege Shell Line
- Obstacle-Clearing Workshop
- Command Relay Spire
- Bulk Hauler Dock

Core outputs:

- Aether Batteries
- Servo Repair Kits
- Engineer Automata Packs
- Heavy Shell Crates
- Obstacle-Clearing Charges
- Command Relay Kits
- Stabilized Energy Canisters

Mechanical identity:

- Steampunk robotics enter as support, not free automation everywhere.
- Energy becomes a strategic commodity for command, machine support, and bombardment readiness.
- Bulk transport unlocks here through no-train heavy freight systems.

Recommended no-train bulk transport:

- Cable-Haul Freight Skids: fixed anchor points pull armored pallets along player-built haul lanes.
- Crawl-Hauler Convoys: slow walking freight platforms that carry large batches between docks.
- Overhead Chainway: suspended chain carriers crossing factory blocks without using rails.

These give the long-distance bulk fantasy without becoming trains in a hat.

### Tier 5 - Siege Engine And Binding Works

Theme: base-killing industry, sealed ritual machines, giant shell preparation, controlled horrors, grim victory logistics.

Player fantasy:

- The factory can now feed annihilation.
- Victory is not "more DPS"; it is a complete industrial chain that makes enemy-base destruction possible.

Primary machines:

- Grand Siege Press
- Binding Crucible
- Harmonic Rangefinder
- Bombardment Foundry
- Strategic Supply Vault
- War Choir Regulator
- Advanced Automata Yard
- Pneumatic Vault Tube Hub

Core outputs:

- Siege Shells
- Base-Breach Charges
- Stabilized Bombardment Cores
- Strategic Ration Reserves
- Mass Replacement Drafts
- Heavy Automata Service Packs
- Command Authority Seals

Mechanical identity:

- Bombardment and base destruction require multiple sustained supply streams.
- Energy shortcuts can accelerate victory, but should increase risk, instability, or maintenance burden.
- Tier 5 should be powerful and costly, not clean and frictionless.

Recommended Tier 5 bulk transport:

- Pneumatic Vault Tubes: sealed long-distance batch tubes between hubs, limited to crate/canister categories.
- Aether-Lift Gantries: short-hop heavy movers between expensive anchor pads, high energy cost.

## 3. Base inputs, at least 10, with thematic notes

Recommended base/input resources:

1. Scrap Iron - ruined machinery, shell fragments, broken tools; feeds ammo, tools, machine parts, fortifications.
2. Timber - planks, supports, crates, duckboards; feeds trenches, rations packaging, simple buildings.
3. Coal - heat and steam; feeds boilers, furnaces, power, late-game heavy industry.
4. Stone/Clay - sandbags, brick, concrete, revetments; feeds trench stability and base repair.
5. Niter - powder chemistry; feeds ammunition and explosives.
6. Sulfur - powder and chemical work; feeds ammo, shells, medical/chemical recipes.
7. Copper - wire, coils, signal kits, dynamos; feeds communications, energy, robotics.
8. Cloth/Fiber - uniforms, bandages, sandbags, filters; feeds bodies/manpower, medical, trench materials.
9. Grain/Moldmeal - dark ration base; feeds food, morale, stamina, replacement pipelines.
10. Brine/Water - cooking, medicine, boilers, chemical dilution; should be needed but not made tedious early.
11. Medicinal Fungus/Herbs - field dressings, antiseptic, pain control; feeds medical supplies.
12. Bone Ash/Grave-Salt - TWB-flavored reagent; feeds wards, binding, stabilization, and grim late recipes.
13. Aether Shards/Willstone - magical energy source; feeds batteries, command relays, siege cores.
14. Clockwork Salvage - gears, springs, lenses; feeds robotics and precision machines.
15. Mustered Recruits - manpower intake represented abstractly as bodies/replacement potential; feeds units only after food, kit, and command processing.

Recommendation:

- Start the prototype with 10 visible base inputs, but keep 15 in the design catalog. The first slice can expose Scrap Iron, Timber, Coal, Niter, Cloth/Fiber, Grain, Medicinal Fungus, Copper, Aether Shards, and Mustered Recruits.

## 4. Main output categories for the war machine

War supply categories should be broader than final item names. The war system should consume categories, while the factory can produce multiple item variants inside those categories.

Recommended categories:

- Bodies/Manpower: replacement units, porters, medics, engineers, command aides.
- Ammunition: rifle ammo, machine-gun belts, shell powder, explosives.
- Food/Morale: rations, hot meals, stimulants, comfort supplies, discipline stabilizers.
- Energy/Fuel: coal fuel, steam cells, aether batteries, stabilized energy canisters.
- Construction/Trench Materials: timber, sandbags, wire, concrete, duckboards, revetment packs.
- Medical: bandages, antiseptic, surgical kits, recovery tents, stretcher supply.
- Machine/Robotics Support: repair kits, gears, servo limbs, automata packs, maintenance oil.
- Command/Communication: signal wire, radios or field telegraph equivalents, command seals, rangefinders.
- Obstacle Operations: wire cutters, clearing charges, sapper tools, bridging kits.
- Bombardment/Base Destruction: heavy shells, siege cores, rangefinder parts, bombardment charges.

Important design distinction:

- Manpower should not mean "free bodies appear because a counter went up." Bodies should require at least food, kit, and command capacity. Otherwise the war side becomes a spawn faucet, which is frightfully common and therefore beneath us.

## 5. Machines/workstations by tier

Tier 1 machines:

- Scavenger Post: converts nearby scrap nodes into Scrap Iron and Clockwork Salvage.
- Timber Yard: produces Timber from edge resource nodes.
- Field Kitchen: Grain/Moldmeal + Brine/Water -> Basic Rations.
- Handloading Bench: Scrap Iron + Niter/Sulfur -> Loose Cartridges.
- Aid Tent: Cloth/Fiber + Medicinal Fungus -> Field Dressings.
- Quartermaster Table: crates/labels/categories loose goods for shipment.
- Muster Tent: Mustered Recruits + Rations + Cloth/Fiber -> Replacement Bodies.
- Tool Bench: Timber + Scrap Iron -> Hand Tools.

Tier 2 machines:

- Conveyor Belt: moves one item stream along grid lanes.
- Loader/Unloader: moves items between belts, machines, and storage.
- Sorter Gate: basic category routing.
- Crusher: Scrap/Stone -> usable fragments.
- Powder Mill: Niter + Sulfur + Coal -> Black Powder.
- Cartridge Press: Scrap Iron + Black Powder -> Ammo Crates.
- Ration Canner: Grain/Moldmeal + Brine/Water + Coal -> Ration Crates.
- Bandage Loom: Cloth/Fiber + Medicinal Fungus -> Medical Crates.
- Sawmill: Timber -> Planks/Crate Boards.
- Wire Twister: Scrap Iron + Copper -> Wire Coils.
- Small Boiler: Coal + Water -> Steam Power/Boiler Fuel.

Tier 3 machines:

- Steam Engine House: consumes Coal/Steam Cells to power nearby machines.
- Chemical Vat: Sulfur + Brine/Water + Coal -> Chemical Reagent.
- Shell Forge: Scrap Iron + Black Powder + Chemical Reagent -> Shell Crates.
- Fuse Bench: Copper + Clockwork Salvage + Chemical Reagent -> Fuse Assemblies.
- Uniform Stitchery: Cloth/Fiber + Buttons/Metal -> Uniform Kits.
- Muster Barracks: Mustered Recruits + Rations + Uniform Kits + Ammo -> Rifle/Engineer Replacement Squads.
- Field Hospital: Medical Crates + Rations -> Wounded Return Capacity.
- Concrete Mixer: Stone/Clay + Brine/Water + Coal -> Concrete Packs.
- Repair Bay: Scrap Iron + Clockwork Salvage + Coal -> Machine Repair Kits.
- Signal Bench: Copper + Timber + Aether Shards -> Signal Kits.

Tier 4 machines:

- Aether Condenser: Aether Shards + Copper + Bone Ash -> Aether Batteries.
- Spark Dynamo: Coal/Steam Cells + Copper -> Industrial Energy.
- Clockwork Assembly Bay: Clockwork Salvage + Servo Parts + Aether Battery -> Automata Support Pack.
- Servo Foundry: Scrap Iron + Copper + Coal -> Servo Parts.
- Warded Storage Vault: stores volatile energy/siege goods safely.
- Siege Shell Line: Shell Crates + Fuse Assemblies + Aether Battery -> Heavy Shell Crates.
- Obstacle-Clearing Workshop: Black Powder + Wire Tools + Engineer Kits -> Clearing Charges.
- Command Relay Spire: Signal Kits + Aether Battery + Command Seal -> Command Relay Kit.
- Bulk Hauler Dock: loads/unloads cable skids, crawl-haulers, or overhead chainway carriers.

Tier 5 machines:

- Grand Siege Press: Heavy Shell Crates + Concrete Packs + Fuse Assemblies -> Siege Shells.
- Binding Crucible: Bone Ash + Aether Battery + Command Seal -> Stabilized Bombardment Core.
- Harmonic Rangefinder: Copper + Clockwork Salvage + Aether Battery -> Bombardment Targeting Kit.
- Bombardment Foundry: Siege Shells + Bombardment Core + Targeting Kit -> Base-Breach Charge.
- Strategic Supply Vault: batches food, ammo, medical, and energy into offensive stockpiles.
- War Choir Regulator: turns Command Relay Kits + Energy into front-wide coordination pulses.
- Advanced Automata Yard: Servo Parts + Aether Batteries + Repair Kits -> Heavy Automata Service Pack.
- Pneumatic Vault Tube Hub: long-distance sealed batch transport between hubs.

## 6. Transportation progression by tier, including no-train bulk transport

Tier 1 transport:

- Porters: workers carry one small item stack by foot.
- Handcarts: slower turning, larger batch, path-blocking.
- Stretcher Crews: move medical/body outputs and wounded-return supplies.
- Quartermaster Runners: prioritize urgent war demands over normal hauling.

Tier 1 mechanics:

- Transporters occupy paths.
- They fatigue and slow down if food is poor.
- Congestion teaches layout before belts appear.
- Short distances matter.

Tier 2 transport:

- Conveyor Belts: one-lane or simple two-lane item movement.
- Chutes: gravity-fed downward/one-way item movement.
- Loader Arms: pull from machines/storage onto belts.
- Basic Depots: buffer and ship crates.

Tier 2 mechanics:

- Conveyors start here, as requested.
- Throughput and routing become the main puzzle.
- Items should remain discrete enough to diagnose.

Tier 3 transport:

- Powered Loaders: faster machine transfer.
- Steam Carts: local route-based carriers between depots.
- Pneumatic Hoses/Pipes: limited to powders, fluids, or sealed canisters if the design adds those as item classes.
- Lift Platforms: move goods over a few blocked tiles.

Tier 3 mechanics:

- Medium-range transport appears.
- Energy/fuel and maintenance become logistics costs.
- Depots begin defining factory districts.

Tier 4 no-train bulk transport:

- Cable-Haul Freight Skids: player places two or more docks; batches move along a cable route between docks.
- Crawl-Hauler Convoys: large walking platforms that carry bulk crates on planned roads.
- Overhead Chainways: suspended carriers that move crates above normal factory traffic.

Tier 4 mechanics:

- Bulk transport moves large batches across the construction area.
- It is dock-to-dock, not cell-by-cell belts.
- It costs energy/maintenance.
- It creates loading and unloading bottlenecks.
- It avoids trains while still solving large-map logistics.

Tier 5 no-train bulk transport:

- Pneumatic Vault Tubes: sealed hub-to-hub batch transport for crates, shells, and energy canisters.
- Aether-Lift Gantries: expensive short-hop transfer between anchor pads for heavy siege goods.

Tier 5 mechanics:

- High throughput but expensive.
- Category restrictions prevent it from trivializing the whole factory.
- Energy instability or maintenance load keeps it from being a magic eraser.

## 7. Flow chart / dependency graph in text form

High-level dependency graph:

```text
RAW INPUTS
  Scrap Iron
  Timber
  Coal
  Stone/Clay
  Niter
  Sulfur
  Copper
  Cloth/Fiber
  Grain/Moldmeal
  Brine/Water
  Medicinal Fungus
  Bone Ash/Grave-Salt
  Aether Shards/Willstone
  Clockwork Salvage
  Mustered Recruits

TIER 1 HAND ECONOMY
  Scrap Iron + Niter/Sulfur -> Handloading Bench -> Loose Cartridges
  Timber + Cloth/Fiber -> Tool Bench/Quartermaster -> Sandbag Bundles
  Grain + Water -> Field Kitchen -> Basic Rations
  Cloth/Fiber + Fungus -> Aid Tent -> Field Dressings
  Recruits + Basic Rations + Cloth/Fiber -> Muster Tent -> Replacement Bodies

TIER 2 BELTED WORKSHOPS
  Niter + Sulfur + Coal -> Powder Mill -> Black Powder
  Scrap Iron + Black Powder -> Cartridge Press -> Ammo Crates
  Grain + Water + Coal -> Ration Canner -> Ration Crates
  Cloth/Fiber + Fungus + Chemicals -> Bandage Loom -> Medical Crates
  Timber + Scrap Iron -> Sawmill/Wire Twister -> Trench Material Crates

TIER 3 STEAM AND CHEMICAL YARD
  Coal + Water -> Steam Engine House -> Steam Power
  Sulfur + Water + Coal -> Chemical Vat -> Chemical Reagent
  Scrap Iron + Black Powder + Chemical Reagent -> Shell Forge -> Shell Crates
  Copper + Clockwork Salvage + Chemical Reagent -> Fuse Bench -> Fuse Assemblies
  Recruits + Rations + Uniform Kits + Ammo -> Muster Barracks -> Replacement Squads
  Medical Crates + Rations -> Field Hospital -> Wounded Return Capacity
  Stone/Clay + Water + Coal -> Concrete Mixer -> Concrete Packs

TIER 4 ARCANE INDUSTRY
  Aether Shards + Copper + Bone Ash -> Aether Condenser -> Aether Batteries
  Scrap Iron + Copper + Coal -> Servo Foundry -> Servo Parts
  Servo Parts + Aether Batteries + Repair Kits -> Clockwork Bay -> Automata Support Packs
  Shell Crates + Fuse Assemblies + Aether Batteries -> Siege Shell Line -> Heavy Shell Crates
  Black Powder + Engineer Tools -> Obstacle Workshop -> Clearing Charges
  Signal Kits + Aether Batteries -> Command Relay Spire -> Command Relay Kits

TIER 5 SIEGE WORKS
  Heavy Shell Crates + Concrete Packs + Fuse Assemblies -> Grand Siege Press -> Siege Shells
  Bone Ash + Aether Batteries + Command Seals -> Binding Crucible -> Bombardment Cores
  Copper + Clockwork Salvage + Aether Batteries -> Harmonic Rangefinder -> Targeting Kits
  Siege Shells + Bombardment Cores + Targeting Kits -> Bombardment Foundry -> Base-Breach Charges

WAR MACHINE CONSUMPTION
  Ammo -> firing, suppression, assault confidence
  Food -> fatigue recovery, scouting range, morale stability
  Bodies -> unit replacement, porters, engineers, medics
  Construction -> foxholes, trenches, wire, base repair
  Medical -> wounded recovery, casualty reduction
  Energy -> command relays, robotics, siege machinery
  Machine Support -> obstacle clearing, repair, automata help
  Bombardment -> enemy base destruction
```

## 8. Example production chains from raw input to war output

Ammo chain:

```text
Scrap Iron + Niter + Sulfur + Coal
  -> Powder Mill makes Black Powder
  -> Cartridge Press makes Ammo Crates
  -> Depot ships Ammunition
  -> War units fire longer, suppress better, and retreat later
```

Food chain:

```text
Grain/Moldmeal + Brine/Water + Coal
  -> Field Kitchen makes Basic Rations
  -> Ration Canner makes Ration Crates
  -> Depot ships Food/Morale
  -> War units fatigue slower, scout farther, and recover morale faster
```

Bodies/manpower chain:

```text
Mustered Recruits + Rations + Cloth/Fiber + Ammo
  -> Muster Tent creates Replacement Bodies
  -> Muster Barracks creates Replacement Squads
  -> Depot ships Manpower
  -> War system spawns/replenishes rifle infantry, sappers, medics, or engineers
```

Medical chain:

```text
Cloth/Fiber + Medicinal Fungus + Brine/Water + Chemical Reagent
  -> Aid Tent makes Field Dressings
  -> Bandage Loom makes Medical Crates
  -> Field Hospital converts supply into Wounded Return Capacity
  -> War casualties more often become wounded and return later
```

Trench construction chain:

```text
Timber + Stone/Clay + Scrap Iron + Cloth/Fiber
  -> Sawmill makes Planks
  -> Wire Twister makes Wire Coils
  -> Concrete Mixer makes Concrete Packs
  -> Quartermaster/Depot ships Construction
  -> War units dig faster, improve cover, repair base cells, and hold captured ground
```

Energy chain:

```text
Coal + Water
  -> Boiler makes Steam Power
  -> Spark Dynamo plus Copper makes Industrial Energy
  -> Aether Condenser plus Aether Shards/Bone Ash makes Aether Batteries
  -> War uses Energy for command relays, automata, searchlights, and siege readiness
```

Robotics support chain:

```text
Scrap Iron + Copper + Clockwork Salvage + Coal
  -> Servo Foundry makes Servo Parts
  -> Repair Bay makes Repair Kits
  -> Clockwork Assembly Bay plus Aether Battery makes Automata Support Packs
  -> War engineers clear obstacles, repair positions, and haul supplies more effectively
```

Bombardment chain:

```text
Scrap Iron + Black Powder + Chemical Reagent
  -> Shell Forge makes Shell Crates
  -> Fuse Bench makes Fuse Assemblies
  -> Siege Shell Line plus Aether Battery makes Heavy Shell Crates
  -> Grand Siege Press makes Siege Shells
  -> Binding Crucible makes Bombardment Cores
  -> Harmonic Rangefinder makes Targeting Kits
  -> Bombardment Foundry makes Base-Breach Charges
  -> Enemy base integrity can be destroyed
```

## 9. How the TWB twist appears mechanically, not just cosmetically

The TWB twist should be expressed through rules, costs, and tradeoffs.

Mechanical twist candidates:

- Aether is a high-output energy source that increases throughput or command reach, but creates instability if storage, wards, or maintenance are poor.
- Bone Ash/Grave-Salt is a stabilizer for grim late-game machinery. It should be powerful, limited, and morally dark without needing gore.
- Bodies/manpower are logistical outputs that require food, equipment, and command capacity. A poorly supplied army can have "bodies" but still fail as soldiers.
- Robotics are maintenance-heavy support tools. They clear obstacles, haul bulk, and repair positions, but require servo parts, energy, and repair kits.
- Command Relay Kits let the player-supported faction coordinate scouts, sappers, and bombardment better, converting factory complexity into war behavior.
- Warded Storage Vaults make dangerous goods safe. If the player skips safety, volatile goods can stall, leak, misfire, or increase seeded war variance.
- The war should remember waste. Oversupplying one category while starving another should create ugly but understandable outcomes.

Example mechanical tradeoffs:

- Aether Battery boosts shell output by 30 percent, but if warding capacity is low it adds instability to bombardment readiness.
- Extra rations improve scouting endurance, but without ammo the scouts avoid contact and retreat often.
- More bodies increase unit count, but without medical and food they become exhausted replacements and clog the base.
- Automata can clear wire faster than infantry, but drain energy and repair kits.

## 10. How supplies should affect the agent-based war system being researched separately

The war-agent report recommends real units on cells, scouting, local contact, fighting, and digging. This crafting system should feed that model through supply categories, not abstract front bonuses.

Supply effects:

- Ammunition: increases fire rate, suppression, willingness to hold contact, and chance to win firefights.
- Food/Morale: reduces fatigue, extends scouting range, improves morale recovery, lowers retreat chance.
- Bodies/Manpower: creates replacement units, porter teams, stretcher crews, engineers, medics, and command aides.
- Construction: speeds foxholes/trenches, improves trench quality, enables wire/dugouts, repairs damaged base cells.
- Medical: converts deaths into wounded, speeds wounded return, stabilizes morale after losses.
- Energy/Fuel: powers searchlights, signal systems, robotics, siege machines, and late logistics.
- Machine/Robotics Support: improves obstacle clearing, base repair, hauling, and heavy engineering tasks.
- Command/Communication: improves squad coordination, response to contacts, reinforcement routing, and bombardment targeting.
- Obstacle Operations: lets sappers clear wire/rubble or convert obstacles into cover.
- Bombardment: enables enemy base damage once scouting, rangefinding, shells, and energy are ready.

Recommended war-demand model:

```text
Each war sector requests:
  required supply category
  urgency
  location
  consuming unit/mission
  shortage reason

Factory ships:
  category quantity
  delivery delay
  reliability/quality

War converts supply into:
  local unit behavior
  mission eligibility
  recovery rates
  trench speed
  bombardment readiness
```

Do not make supply a single "war score." That would bury the good part.

## 11. UI/diagnostics needed for playtesting

Factory UI needs:

- Bottom-row tier filter buttons: T1, T2, T3, T4, T5.
- Bottom-row category buttons: Ammo, Food, Bodies, Energy, Construction, Medical, Robotics, Bombardment.
- Machine tooltip showing inputs, output, tier, throughput, current blockage, and transport mode.
- Route overlay showing porters, belts, depots, cable hauls, and bulk docks.
- Production chain inspector: click an output and see upstream shortages.
- War demand panel: shows what the war is asking for right now and why.
- "Days of supply" or "ticks of supply" for each war category.
- Warning chips: starved, blocked output, no carrier, no depot route, insufficient energy, unstable aether storage.

War UI needs:

- Top bar quick references for base integrity, active contacts, available bodies, ammo state, food state, energy state, and bombardment readiness.
- Right-hand tracker cards for pinned supply categories.
- Contact report reasons tied to supplies:
  - "Attack stalled: ammo low."
  - "Trench held: construction supply high."
  - "Scouts returned: rations exhausted."
  - "Wounded lost: medical shortage."
- Sector inspector showing local supply reach and what goods are missing.

Playtest diagnostics:

- Per-category production per minute.
- Per-category consumption per minute.
- Average delivery delay.
- Transport congestion.
- Wasted/overproduced goods.
- Current bottleneck machine.
- Current bottleneck transport type.
- War effect from last shipment.

## 12. Risks/open questions

Risks:

- Item explosion: 15 raw inputs and 5 tiers can overwhelm the prototype if exposed too early.
- Magic mush: aether/bone/wards need concrete mechanics or they become fancy labels.
- Body/manpower tone risk: the concept is dark, but the game should not become pointlessly grotesque. Keep bodies as manpower/replacement logistics unless Bob/user deliberately chooses a harsher direction.
- Belt conflict: current prototype uses belts immediately; progression should gate belts later without throwing away the working prototype.
- Power creep: Tier 4/5 bulk transport can trivialize factory layout unless it is hub-based, expensive, and category-limited.
- War opacity: if supplies influence many unit behaviors, diagnostics become mandatory.
- Balance risk: if bodies are too cheap, the player solves war with spam. If too expensive, the war feels stalled.
- No-train bulk risk: cable skids and vault tubes need a strong identity so players do not ask why they are not just belts.
- Performance risk: large factories plus agent war will need data-oriented tick discipline and no full-map scans.

Open questions:

- Should "bodies" mean recruits only, or should late TWB magic include bound dead/echo constructs? Recommendation: start with recruits and automata, leave darker binding for later review.
- Does energy begin as optional machine boost, required machine input, or late-game strategic supply? Recommendation: optional Tier 3 support, required Tier 4/5.
- Should water/brine be a normal item, a pipe/fluid, or an abstract local resource? Recommendation: keep it as crate/canister item until the core loop works.
- Should workers/porters be simulated as visible units on the factory grid? Recommendation: yes for Tier 1, but cap count and provide diagnostics.
- Should the enemy have a mirrored factory economy? Recommendation: no for phase 1. Give the NPC baseline supply curves and use the same war consumption rules.
- Should bulk transport routes be player-shaped roads, point-to-point links, or dock networks? Recommendation: Tier 4 cable/crawl dock networks first.

## 13. Recommended first implementation slice for current prototype

Do not implement the full five-tier tree next. A dignified prototype eats one course at a time.

Recommended first slice:

1. Convert the current hardcoded recipe model toward a data catalog shape, even if still defined in C# at first.
2. Keep the existing four supply categories as live compatibility outputs: Ammo, Trench Materials, Rations, Medical.
3. Add two new prototype supply categories: Manpower and Energy.
4. Add 10 base inputs to the catalog, but only place a few resource nodes in the starter map.
5. Add Tier labels to machines and recipes.
6. Add Tier 1 porter transport as a simple visible carrier route between adjacent storage/machines.
7. Keep conveyors available in debug/prototype mode, then gate them as Tier 2 when progression is active.
8. Add one chain each:
   - Ammo: Scrap + Niter/Sulfur -> Ammo
   - Food: Grain + Water -> Rations
   - Manpower: Recruits + Rations + Cloth -> Replacement Bodies
   - Energy: Coal + Copper/Aether -> Energy
   - Construction: Timber + Scrap -> Trench Materials
   - Medical: Cloth + Fungus -> Medical
9. Update the right tracker to show war demand versus factory shipment for these six categories.
10. Make war-side diagnostics consume the new categories before adding more machines:
   - Manpower affects replacement availability.
   - Energy affects command/bombardment readiness.
   - Existing supplies continue affecting readiness, trenches, casualties, and bombardment.

Suggested first smoke checks:

- Every tier-1 recipe has at least one valid input source and one valid output route.
- Porter transport can move one item from source to destination.
- Conveyor transport still works for the existing prototype loop.
- Manpower shipments increase replacement capacity, not immediate magical victory.
- Energy shipments improve bombardment/command readiness only when paired with shells or command goods.
- War diagnostics explain at least one shortage and one benefit from shipped goods.

## Context sources read

Project memory:

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\twb-trenchworks\overview.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\twb-trenchworks\architecture.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-war-agent-simulation-design-report.md`

Prototype source inspected:

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`

External historical flavor references:

- National WWI Museum and Memorial, trench warfare overview: `https://www.theworldwar.org/learn/about-wwi/trench-warfare`
- Imperial War Museums, WW1 logistics overview/interviews: `https://www.iwm.org.uk/history/voices-of-the-first-world-war-logistics-of-war`
- National Army Museum, horse power and transport in WW1: `https://www.nam.ac.uk/explore/horse-power-first-world-war`
- National Army Museum, weapons of the Western Front: `https://www.nam.ac.uk/explore/weapons-western-front`

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-crafting-logistics-design-report.md`

## Checks run

- Read current Trenchworks memory, architecture, task brief, current prototype supply code, and the war-agent design report.
- Performed light historical reference scan for WW1 trench/logistics/transport flavor.
- No Unity project files were edited.
- No compile or Unity smoke test was needed for this design-only worker pass.

## Cleanup performed

- No temporary files, screenshots, throwaway logs, or generated dev artifacts were created.

## Memory-worthy notes

- The crafting system should grow from Tier 1 manual porters into Tier 2 belts, Tier 3 steam/chemical yards, Tier 4 arcane industrial logistics, and Tier 5 siege/binding works.
- The game should eventually track more war supply categories than the current four: bodies/manpower, ammo, food, energy, construction, medical, robotics, command, obstacle operations, and bombardment.
- Conveyors should be Tier 2, but the current working prototype belt loop should be preserved until progression is implemented.
- No-train bulk transport recommendation: cable-haul freight skids, crawl-hauler convoys, overhead chainways, and later pneumatic vault tubes.
- TWB magic should create mechanics: instability, warding, command reach, energy risk, and dark manpower tradeoffs.

## Anything blocked

Nothing blocked.
