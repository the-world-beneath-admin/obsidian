# 2026-05-16 TWB Trenchworks Factory Construction Materials Addendum

## Scope

Standalone Unity 2D TWB Trenchworks prototype under The World Beneath umbrella.

This is a design-only addendum. No Unity code was implemented. No permanent memory, wiki, index, hot, or log files were edited.

## 1. Directional correction: factory-building materials are their own supply need

The production system needs a third major demand lane:

- Frontline supply: goods sent to military teams and fortifications.
- Upward crafting: goods reserved for higher-tier weapons, magic, robotics, and siege chains.
- Factory expansion: goods consumed to build machines, conveyors, worker infrastructure, steam systems, magic infrastructure, depots, and bulk transport.

Prior crafting reports already identify planks, frames, steam fittings, cable spools, precision gears, reinforced frames, and bulk dock parts. This addendum makes that demand explicit and gives it its own supply category: Factory Construction Supply.

Changes needed to prior crafting reports:

- Add Factory Construction Supply as a first-class output category, separate from Trench Materials and War Supplies.
- Add Steel, Machine Parts, Conveyor Parts, Boiler Parts, Factory Foundations, Worker Infrastructure Goods, Steam Fittings, and Essence Conduit Parts to the production catalog.
- Treat boilers and underground steam pipes as the main machine-power system. Coal feeds boilers; boilers generate steam; steam moves through an underground view/layer to power industrial machines.
- Change "Construction" from one vague bucket into at least two buckets:
  - Trench Construction Goods: planks, sandbags, wire, duckboards, braces, revetments, tools.
  - Factory Construction Goods: steel plates, frames, machine parts, conveyor parts, foundations, pipes, valves, belts, boilers, conduits.
- Keep trade-offs tri-directional: front now, higher-tier reserve, or factory expansion.
- Preserve Tier 1 manual labour, Tier 2 conveyors, Tier 3 steam, Tier 4 arcane industry, Tier 5 siege/binding works.
- No trains. Later bulk transport should remain cable-haul skids, crawl-haulers, overhead chainways, pneumatic vault tubes, or aether-lift gantries.

Design rule:

- The factory should not expand for free. Every new machine should be a logistical decision, not a magical square appearing because the player clicked politely.
- Coal is not the factory's equivalent of a diesel generator plus power cable. Boilers and the underground steam-pipe network fill that role. Coal can still be a direct recipe input for smelting, coke, steel, chemistry, and shell production.

## 2. Raw resources required for factory construction and machine-building

Core raw resources:

- Iron Ore: clean metal source for pig iron, steel, plates, beams, rollers, casings.
- Scrap Iron: early substitute for iron ore; dirty, cheap, useful for crude parts and repairs.
- Coal: fuel for smelting, boilers, steam engines, coke, and heavy industry.
- Stone/Clay/Sand: foundations, brick, concrete, refractory linings, sandbag fill, molds.
- Timber: early frames, planks, crates, scaffolding, belt supports, worker buildings.
- Fiber/Cloth/Leather/Treated Fabric: conveyor belt material, filters, safety gear, worker goods.
- Copper: wiring, coils, signal lines, valves, bearings, dynamos, essence conduits.
- Tin/Brass Additive or Bearing Metal: optional later resource for bearings, bushings, and precision fittings.
- Water/Brine: boilers, concrete, cooling, chemical processing, farming, medicine.
- Essence: magic infrastructure, farm-machine growth input, ward plates, stabilizers, conduits.
- Bone-Salt/Grave-Salt: stabilizer for essence systems and late arcane machinery.
- Clockwork Salvage: gears, springs, lenses, precision mechanisms, early robotics.
- Oil/Grease/Tallow: bearings, belts, drive shafts, gearboxes, machine maintenance. If item count must stay low, fold this into Machine Lubricant made from coal tar and animal/fungal oils.

Starter recommendation:

- Start with Iron Ore or Heavy Scrap, Coal, Timber, Stone/Clay, Fiber, Copper, Water, Essence.
- Add bearing metal, grease, and clockwork salvage after conveyors and steam are readable.

## 3. Steel chain: ore/scrap/coal -> pig iron/steel -> plates/beams/casings

Steel should unlock the durable factory.

Tier I crude metal chain:

```text
Scrap Iron + Coal + Labour
  -> Charcoal/Coal Forge or Scrap Furnace
  -> Wrought Iron / Crude Iron
  -> Nails, Hand Tools, Crude Frames, Simple Machine Parts
```

Tier II early industrial chain:

```text
Iron Ore or Heavy Scrap + Coal + Stone/Clay Flux
  -> Small Furnace
  -> Pig Iron
  -> Rolling/Press Bench
  -> Iron Plates, Rods, Rollers, Simple Casings
```

Tier III steel chain:

```text
Pig Iron + Coal/Coke + Flux + Steam Power
  -> Steel Furnace
  -> Steel Ingots
  -> Rolling Mill / Beam Press / Casing Press
  -> Steel Plates, Steel Beams, Machine Casings, Pressure Shells
```

Tier IV/V advanced metal chain:

```text
Steel Plates + Copper + Precision Gears + Essence Stabilizers
  -> Reinforced Frames / Servo Frames / Warded Casings
  -> Bulk Hauler Parts, Automata Parts, Siege Press Parts, Warded Vault Parts
```

Steel outputs:

- Steel Plates: machines, boilers, casings, bunkers, reinforced factory floors.
- Steel Beams: large machines, bulk docks, overhead chainways, siege press frames.
- Machine Casings: presses, mills, boilers, chemical vats, farm upgrades.
- Pressure Shells: boilers, pressure pipes, pneumatic tubes, pressure projectors.
- Reinforced Frames: Tier 3+ factory expansion, heavy machines, bulk transport, siege equipment.

Trade-off:

- Steel competes directly between factory expansion, shells/guns, fortifications, and late siege machinery.

## 4. Conveyor chain: belts, rollers, frames, bearings, drive shafts, motors/steam drives

Conveyors begin in Tier 2, but they should require visible parts.

Tier II basic conveyor:

```text
Treated Fabric / Leather + Planks or Iron Frames + Rollers + Hand Tools
  -> Conveyor Belt Segment
```

Basic conveyor parts:

- Belt Material: Fiber/Cloth/Leather + Coal Tar or Essence-treated resin later.
- Rollers: Timber early, Iron/Steel later.
- Frames: Timber/Planks early, Iron Frames later.
- Fasteners: Scrap/Iron Nails.
- Simple Bearings: Scrap/Copper/Bearing Metal.
- Hand Tools: install and repair.

Tier II/III powered conveyor:

```text
Conveyor Belt Segment + Drive Shaft + Bearings + Gearbox + Boiler/Steam Drive
  -> Powered Conveyor Line
```

Powered conveyor parts:

- Drive Shafts: Iron/Steel Rods.
- Gearboxes: Machine Parts + Gears.
- Bearings: Copper/Bearing Metal + Grease.
- Steam Drive: Boiler Parts + Pressure Pipe + Valve.
- Loaders/Unloaders: Frames + Arms + Bearings + Gearbox.
- Sorter Gates: Frames + Gearbox + Signal/Control Link.

Tier IV advanced conveyor/bulk:

- Overhead Chainway: Steel Beams + Chain Links + Gearboxes + Steam/Essence Drive.
- Cable-Haul Freight Skid: Steel Cable + Dock Frames + Winch + Steam Drive.
- Crawl-Hauler: Reinforced Frame + Servo Parts + Boiler/Essence Drive + Repair Kits.

Design rule:

- Belt spam should not be free. Belts are cheap enough to use, but large belt networks should visibly consume fabric, frames, rollers, and maintenance.

## 5. Machine construction chain: foundations, frames, boilers, gears, pipes, valves, tools

Machine construction should use kits, not only raw resources.

Foundations:

```text
Stone/Clay + Water + Labour
  -> Brick / Packed Foundation

Stone/Clay + Water + Coal + Scrap/Steel Rods
  -> Concrete Foundation
```

Frames:

```text
Timber + Scrap
  -> Crude Frame

Iron Plates/Rods + Fasteners
  -> Iron Frame

Steel Beams + Machine Tools
  -> Reinforced Frame
```

Machine parts:

```text
Scrap/Iron + Tools
  -> Simple Machine Parts

Steel Plates + Gears + Bearings + Grease
  -> Industrial Machine Parts

Precision Gears + Copper + Clockwork Salvage
  -> Precision Mechanisms
```

Boilers:

```text
Steel Plates + Rivets/Fasteners + Pressure Valves + Firebrick + Coal
  -> Boiler Kit
```

Pipes and valves:

```text
Iron/Steel Rods + Copper + Machine Parts
  -> Pressure Pipes

Copper + Bearings + Precision Tools
  -> Valves / Gauges
```

Tools:

```text
Timber + Scrap
  -> Hand Tools

Steel + Tool Bench
  -> Machine Tools

Machine Tools + Precision Parts
  -> Advanced Tooling
```

Machine build kit examples:

- Handloading Bench: Crude Frame + Hand Tools + Work Surface.
- Powder Mill: Foundation + Iron Frame + Rollers + Safety Gear.
- Conveyor: Belt Segment + Frames + Rollers.
- Ration Canner: Foundation + Boiler/Heat Source + Machine Parts + Food-Safe Casings.
- Sawmill: Foundation + Frame + Saw Blades + Drive Shaft.
- Wire Twister: Frame + Rollers + Gearbox + Copper/Scrap input.
- Steam Engine House: Concrete Foundation + Boiler Kit + Pressure Pipes + Valves + Steel Beams.
- Aether Condenser: Warded Foundation + Essence Conduits + Copper Coils + Stabilizers.

## 6. Worker infrastructure chain: housing/barracks, food service, safety/medical, light/heat

Worker infrastructure is not decoration. It keeps the factory labour force from collapsing.

Housing/Barracks:

```text
Timber + Planks + Fiber/Cloth + Nails
  -> Worker Bunkhouse

Planks + Brick/Concrete + Heat Source
  -> Worker Barracks
```

Effects:

- Raises worker capacity.
- Reduces fatigue recovery time.
- Lowers desertion/unavailable-worker chance.

Food service:

```text
Raw Food + Water + Fuel/Coal + Kitchen Labour
  -> Worker Meals

Worker Meals + Canteen
  -> Better worker stamina and morale
```

Effects:

- Improves worker speed and reliability.
- Gives the player a visible reason not to ship every ration to the front.

Safety/medical:

```text
Cloth/Fiber + Medicinal Fungus + Water
  -> Bandages / Safety Kits

Bandages + Planks + Tools
  -> Factory Aid Station
```

Effects:

- Reduces accident downtime.
- Helps essence/steam mishap recovery.
- Keeps specialist workers available.

Light/heat:

```text
Coal + Boiler/Heater
  -> Heat

Coal/Essence + Lamps/Copper
  -> Factory Lighting
```

Effects:

- Reduces fatigue in worker zones.
- Improves night/low-visibility productivity if that becomes a tick factor.
- Essence lamps should be better but risk instability.

Safety gear:

- Gloves/Aprons: Cloth/Fiber + Leather/Treated Fabric.
- Masks/Filters: Fiber + Medicinal Fungus/Charcoal.
- Helmets: Steel Plates + Cloth.
- Essence Wards: Bone-Salt + Copper + Essence.

Worker infrastructure trade-off:

- Spending on worker infrastructure delays war goods, but improves the whole factory. This is precisely the sort of sensible inconvenience a good production game requires.

## 7. Steam infrastructure chain: coal handling, boilers, underground pipes, pressure, and machines

Steam infrastructure should become the industrial power backbone. This is the Trenchworks equivalent of the normal factory-game generator and power-cable system, except the generator is a boiler and the cable is an underground steam pipe.

Coal handling:

```text
Coal Seam
  -> Coal Yard
  -> Coal Hopper / Loader
  -> Boiler / Furnace / Engine House
```

Coal handling goods:

- Coal Bins: Planks + Steel Plates.
- Hoppers: Steel Plates + Frames.
- Ash/Slag Handling: Tools + Carts + Worker labour.
- Coke Oven later: Coal + Heat + Brick/Firebrick -> Coke.

Boilers:

```text
Steel Plates + Pressure Valves + Firebrick + Rivets + Water + Coal
  -> Boiler Kit
  -> Boiler / Steam Engine House
  -> Steam
```

Underground steam pipes:

```text
Steel Pipes + Valves + Gauges + Seals + Insulation
  -> Underground Steam Pipe Segment
  -> Steam Network
```

Steam pressure and engines:

```text
Boiler Kit + Underground Steam Pipes + Steel Beams + Gearbox + Flywheel
  -> Steam Engine House
```

Steam users:

- Most powered machines once steam is unlocked.
- Ration Canners.
- Powder Mills.
- Concrete Mixers.
- Chemical Vats.
- Shell Forges.
- Rolling Mills and Beam Presses.
- Powered Conveyors, loaders, and sorters.
- Powered Loaders.
- Steam Carts.
- Bulk Hauler Dock.
- Pneumatic Vault Tube Hub support later.

Underground layer rule:

- Steam pipes should be placed and debugged on a separate underground factory layer, not mixed into the surface belt layer.
- Surface machines show their steam connection status, but pipe routing itself belongs in the underground view.
- The first implementation can use boiler adjacency or simple connected pipe networks before adding full pressure simulation.

Steam risks:

- Pressure leaks slow connected machines.
- Poor valves or low maintenance cause accidents.
- Coal shortage idles the steam network.
- Water shortage risks boiler damage.
- Broken underground steam pipes isolate connected machines.

## 8. Magic infrastructure chain: essence conduits, ward plates, stabilizers, farm-machine essence input

Magic infrastructure should be tangible, not a free blue number.

Essence extraction:

```text
Essence Seep / Willstone Vein
  -> Essence Tap
  -> Raw Essence
```

Essence conduits:

```text
Copper + Bone-Salt + Insulated Fiber + Essence
  -> Essence Conduit
```

Ward plates:

```text
Steel Plate + Bone-Salt + Copper Filament + Essence
  -> Ward Plate
```

Stabilizers:

```text
Bone-Salt + Clockwork Salvage + Copper + Essence
  -> Stabilizer
```

Farm-machine essence input:

```text
Essence Tap + Essence Conduit + Farm Machine
  -> Essence-fed growth cycle
```

Magic infrastructure users:

- Farm Machine.
- Warded Storage Vault.
- Aether Condenser.
- Essence Hothouse.
- Aether Searchlight.
- Command Relay Spire.
- War Choir Regulator.
- Binding Crucible.
- Bombardment Foundry stabilization.
- Warded Siege Supply.

Magic risks:

- Overdraw creates spoilage, instability, worker sickness, or output variance.
- Unwarded conduits leak essence and reduce efficiency.
- Essence infrastructure should consume copper, steel, bone-salt, and stabilizers, so magic competes with mundane industry.

## 9. How construction goods compete with frontline goods and higher-tier crafting

The central allocation model should become three-way:

```text
Goods can go to:
  Frontline need
  Higher-tier crafting reserve
  Factory expansion / infrastructure
```

Examples:

- Steel Plates:
  - Front: bunkers, gun pits, field guns.
  - Higher-tier: siege shells, automata frames, bombardment cores.
  - Factory: machine casings, boilers, conveyors, rolling mills.

- Planks:
  - Front: trenches, duckboards, braces.
  - Higher-tier: treated frames, crates, bulk dock forms.
  - Factory: machine foundations, worker housing, belt frames, depots.

- Copper:
  - Front: signal kits, wire, command posts.
  - Higher-tier: aether batteries, targeting lenses, conduits.
  - Factory: bearings, motors, wiring, essence conduits, valves.

- Coal:
  - Front: boiler fuel for forward equipment later.
  - Higher-tier: steel, chemicals, shells, siege industry.
  - Factory: steam power, smelting, canners, heaters, transport.

- Essence:
  - Front: magic units, searchlights, warded supply.
  - Higher-tier: aether batteries, bombardment cores, binding works.
  - Factory: farm growth, conduits, wards, essence machines.

UI implication:

- The player should see that building another conveyor line may delay ammo, trench work, or a steam upgrade. Factory expansion is not free background growth; it is one of the main strategic uses of production.

## 10. Updated flow chart / dependency graph

```text
RAW NODES
  Iron Ore / Heavy Scrap
  Coal
  Timber
  Stone / Clay / Sand / Flux
  Copper
  Fiber / Cloth / Leather
  Water
  Essence
  Bone-Salt
  Clockwork Salvage
  Oil / Grease input

METAL AND STEEL
  Iron Ore or Scrap + Coal + Flux
    -> Furnace
    -> Pig Iron
    -> Steel Furnace / Rolling Mill
    -> Steel Plates / Steel Beams / Casings / Rods

FACTORY PARTS
  Steel Plates + Gears + Bearings + Grease
    -> Machine Parts
  Steel Beams + Machine Parts
    -> Reinforced Frames
  Steel Plates + Valves + Firebrick
    -> Boiler Kits
  Steel/Copper + Valves + Gauges
    -> Underground Steam Pipe Segments
  Coal + Water + Boiler Kits
    -> Steam
  Steam + Underground Steam Pipe Layer
    -> Machine Power

CONVEYORS
  Fiber/Leather + Rollers + Frames + Bearings
    -> Conveyor Belt Segments
  Conveyor Segments + Drive Shafts + Gearbox
    -> Powered Conveyor Lines

WORKER INFRASTRUCTURE
  Planks + Fiber + Nails
    -> Bunkhouse / Canteen / Aid Station
  Coal + Heater + Lighting Goods
    -> Worker Heat / Light

MAGIC INFRASTRUCTURE
  Essence + Copper + Bone-Salt + Steel Plates
    -> Essence Conduits / Ward Plates / Stabilizers
  Essence Conduits + Farm Machine
    -> Essence-fed Food Production

TRI-DIRECTIONAL DEMAND
  Factory Expansion
  Frontline Supply
  Higher-Tier Crafting / Siege
```

## 11. UI/diagnostics needed so players understand factory expansion bottlenecks

Top bar:

- Factory Construction Supply stock.
- Steel stock.
- Machine Parts stock.
- Conveyor Parts stock.
- Steam pressure/coal status.
- Underground steam-pipe coverage and disconnected machines.
- Essence infrastructure status.
- Current blocked build count.

Build menu:

- Machine cost preview should show required construction goods.
- Conveyor cost preview should show belt segments, frames, rollers, and drive parts.
- Steam machines should show boiler/pipe/valve requirements.
- Powered machines should show whether they are connected to the underground steam network.
- Magic machines should show conduit/ward/stabilizer requirements.
- Worker buildings should show housing, food service, safety, heat/light needs.

Right tracker:

- "Blocked builds" list with exact missing goods.
- "Factory expansion demand" versus "front demand" versus "reserve demand."
- Steel chain status: ore/scrap, coal, furnace, pig iron, steel, plates/beams.
- Conveyor chain status: belt material, rollers, frames, bearings, drive shafts.
- Steam chain status: coal, boiler, pipes, valves, pressure.
- Steam layer status: boiler output, pipe connectivity, leaks, pressure, unpowered machines.
- Magic infrastructure status: essence, conduits, ward plates, stabilizers.

Diagnostic strings:

- "Cannot build Conveyor: 4 rollers missing."
- "Cannot build Boiler: steel plates and pressure valves missing."
- "Ration Canner blocked: machine casing unavailable."
- "Farm Machine stalled: essence conduit incomplete."
- "Factory expansion starving front: steel allocated to Beam Press."
- "Front wire delayed: copper reserved for essence conduits."

Allocation UI:

- Add a three-way allocation control for contested goods:
  - Front
  - Reserve
  - Factory
- Early version can use simple buttons. Later version can use percentages and reserve floors.

## 12. Balance risks/open questions

Risks:

- Too many construction subparts can make early factory growth feel like paperwork.
- Too few construction subparts makes machine growth feel free and shallow.
- Steel can become a choke point for everything. This is good only if diagnostics are excellent.
- Conveyors gated behind too many parts may make Tier 2 feel delayed or frustrating.
- Worker infrastructure can feel optional unless worker fatigue/hunger matters.
- Magic infrastructure can become a second steel chain with purple paint if essence risks and warding are not distinct.
- Steam can become too dominant if it powers every industrial improvement without pressure, water, pipe, leak, maintenance, and layout counterpressure.
- Frontline, reserve, and factory demand may overwhelm players if introduced all at once.

Open questions:

- Should Iron Ore be a distinct node, or should early prototype use Scrap/Heavy Scrap only? Recommendation: start with Heavy Scrap, add Iron Ore when steel chain expands.
- Should steel begin in Tier 2 or Tier 3? Recommendation: crude iron in Tier 2, real steel in Tier 3.
- Should conveyors require maintenance? Recommendation: not first slice; add wear later if belt spam needs pressure.
- Should worker buildings occupy real factory space? Recommendation: yes, but keep them compact and legible.
- Should magic conduits be routed like pipes/belts? Recommendation: later. First slice can use adjacency or connected-node range.

## 13. Recommended first implementation slice

First slice goal: prove factory expansion as a visible consumer without burying the player under parts.

Recommended first build goods:

- Factory Construction Supply: abstract compatibility category for build costs.
- Steel Plates: made from Scrap/Heavy Scrap + Coal.
- Machine Parts: made from Steel Plates + Scrap.
- Conveyor Parts: made from Planks + Rollers/Steel Plates + Fiber.
- Boiler Parts: made from Steel Plates + Copper/Valves.
- Essence Conduit Parts: made from Copper + Essence + Bone-Salt or a placeholder stabilizer.

Recommended first machines/chains:

1. Scrap/Heavy Scrap + Coal -> Steel Plates.
2. Steel Plates + Scrap -> Machine Parts.
3. Timber -> Planks.
4. Planks + Fiber + Steel Plates -> Conveyor Parts.
5. Steel Plates + Copper -> Boiler Parts.
6. Copper + Essence -> Essence Conduit Parts.
7. Machine build costs consume a small mix of these goods.
8. Add one Boiler that consumes Coal and Water to produce Steam.
9. Add a first underground steam-pipe/adjoining-network prototype that powers one or two machines.
10. Keep existing prototype machines buildable through a compatibility mode, but show missing construction goods and missing steam power in diagnostics.

Recommended first UI:

- Add Factory build-goods stock list.
- Add "Missing build materials" messages.
- Add three-way allocation display: Front / Reserve / Factory.
- Add machine tooltip showing construction cost separately from recipe input.

First pass success criteria:

- Player understands why a new conveyor or machine cannot be built.
- Factory expansion competes with front supply and higher-tier crafting.
- Steel, machine parts, and conveyor parts feel useful without requiring a full metallurgy simulator.
- Steam and essence infrastructure have clear material hooks for later systems.
- Steam power is boiler-generated and distributed through an underground pipe layer rather than a diesel-generator/power-cable abstraction.

## Context sources read

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-crafting-logistics-design-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-crafting-logistics-tradeoff-addendum.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-worker-food-coal-essence-addendum.md`

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-factory-construction-materials-addendum.md`

## Checks run

- Read required project memory context.
- Read the crafting/logistics design report.
- Read the crafting trade-off addendum.
- Read the worker/food/coal/essence addendum.
- Confirmed this pass is design-only and did not edit Unity source or permanent memory.

## Cleanup performed

No temporary files, screenshots, throwaway logs, or generated dev artifacts were created.

## Memory-worthy notes

- Factory expansion should be a first-class production demand.
- Steel, machine parts, conveyor parts, boiler parts, underground steam-pipe parts, worker infrastructure goods, and essence conduit parts are needed alongside war goods.
- Contested goods should support three destinations: front, reserve, and factory.
- Machine construction costs should be shown separately from recipe input costs.
- No-train bulk transport direction remains intact.

## Anything blocked

Nothing blocked.
