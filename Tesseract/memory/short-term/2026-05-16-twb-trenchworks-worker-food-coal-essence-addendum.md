# 2026-05-16 TWB Trenchworks Worker, Food, Coal, And Essence Addendum

## Scope

Standalone Unity 2D TWB Trenchworks prototype under The World Beneath umbrella.

This is a design-only planning addendum. No Unity code was implemented. No permanent memory, wiki, index, hot, or log files were edited.

## 1. Directional summary

The factory side should gain a worker system and three foundational sustaining resources:

- Food for people.
- Coal for steam technology.
- Essence for magic systems.

Food should no longer be treated as a simple raw input that appears as grain plus water. Food becomes a central pressure resource that is grown through a farm machine, requires essence, and then must be allocated between factory workers and military teams. Coal remains the industrial steam backbone. Essence becomes the magical backbone, powering farms, aether systems, wards, late command tools, and some TWB twist units.

Changes needed to Pauli's crafting/trade-off reports:

- Replace the early food chain `Grain/Moldmeal + Water -> Basic Rations` with `Food input node + Essence + worker time -> Farm Machine -> Raw Food`, then `Raw Food -> Field Kitchen/Ration Canner -> Rations`.
- Keep Grain/Moldmeal as a food-input or seed-stock concept, not as finished food by itself.
- Add factory worker food consumption before military shipment. The war should not receive all food automatically if the factory workforce is starving.
- Split "Energy/Fuel" into clearer practical subchains: Coal/Steam and Essence/Magic. Coal feeds boilers, boilers generate steam, and steam moves through an underground pipe layer to power machines. Aether batteries remain later crafted essence devices, not the only magical fuel.
- Make trench materials explicit rather than bundled too early: planks, sandbags, wire, duckboards, braces, concrete/revetments, hand tools, and drainage/repair goods.
- Preserve the tier direction: Tier 1 manual labour, Tier 2 conveyors, Tier 3 steam, Tier 4 arcane industry, Tier 5 siege works.

## 2. Worker system model: worker types, assignment, fatigue, food consumption, starvation effects

Workers should be simulated enough to make the factory feel alive, but not so individually fussy that the player becomes a clerk of misery.

Recommended worker types:

- Labourer: general carrying, loading, simple harvesting, basic manual jobs.
- Porter: Tier 1 item transport between machines, depots, and resource nodes.
- Farmer: operates farm machines and handles food growth/harvest.
- Machine Operator: runs hand benches, presses, canners, looms, and standard machines.
- Steam Engineer: operates boilers, engine houses, powered loaders, steam carts, and pressure systems.
- Essence Tender: handles essence taps, farm infusion, aether condensers, warded storage, and magic machines.
- Mechanic: repairs belts, loaders, boilers, machines, and later robotics.
- Quartermaster: prioritizes shipments, depots, worker food allocation, and war supply dispatch.
- Factory Builder: constructs machines, belts, depots, roads, storage, and factory-side infrastructure.
- Clockwork Servitor: late worker-adjacent robotic labour that needs energy and repair, not food.

Assignment model:

- Workers are assigned by job category and zone, not by clicking each person.
- Job boards or depots define priorities: Food, Mining, Hauling, Production, Repair, Construction, War Shipment.
- Workers pick tasks based on priority, distance, skill, fatigue, and blocked routes.
- Tier 1 should show visible porters/labourers walking. Later tiers automate some movement but still require operators, engineers, and maintenance.

Fatigue:

- Workers gain fatigue while carrying, operating, building, repairing, or working near danger/essence instability.
- Food, rest stations, and good routes reduce fatigue.
- High fatigue slows movement, increases machine error chance, reduces farming yield, and increases accident/stall chance.

Food consumption:

- Each human worker consumes food per time interval.
- Heavy jobs consume more food: porter hauling, steam engineering, farming, construction, essence handling.
- Food shortages should affect the factory before the war fully collapses. This makes the food split legible.

Starvation effects:

- Mild shortage: slower walking, reduced machine speed, slower build/repair.
- Moderate shortage: workers abandon low-priority tasks, hauling queues grow, accidents increase.
- Severe shortage: factories stall, workers desert or become unavailable, essence handling becomes dangerous, war shipments are interrupted.
- Recovery: feeding workers restores performance gradually, not instantly.

Pushback:

- Do not make worker hunger an instant fail state. It should create visible bottlenecks and painful trade-offs, not a surprise executioner hiding under the UI.

## 3. Three base energy resources: Food, Coal, Essence

Food:

- Sustains human workers and military teams.
- Produced through farm machines using food-input nodes and essence.
- Can be processed into Basic Rations, Ration Crates, Meal Tins, Strategic Ration Reserves, and worker meals.
- The first allocation conflict is workers versus front.

Coal:

- Sustains steam and heat.
- Feeds boilers and furnaces.
- Boilers convert Coal plus Water into Steam.
- Steam is distributed through an underground steam-pipe layer and becomes the main power source for industrial machines such as powder mills, canners, concrete mixers, powered loaders, chemical vats, conveyors, shell forges, steam carts, and later bulk logistics.
- Coal can still be used directly in recipes where it physically belongs, such as Coal plus Iron/Scrap for smelting and steel.
- Coal or water shortages should lower steam pressure and slow industry, not starve humans directly.

Essence:

- Sustains magic systems.
- Required for farms, essence taps/condensers, aether batteries, wards, command relays, TWB twist units, late siege stabilization, and magical farm upgrades.
- Essence shortages should force the player to choose between food growth, magical war tools, robotics support, and final bombardment support.

Recommended naming clarity:

- Use "Essence" as the base magical resource.
- Use "Aether Battery" as a crafted Tier 4+ storage/output item made from Essence plus copper/wards.
- This prevents every magical system from sounding like the same soup in a different jar.

## 4. Resource node plan for food inputs, coal, essence, and other key raw goods

Food-related nodes:

- Fungal Loam Patch: seed/substrate source for farm machines; dark TWB food base.
- Root-Meal Bed: hardy trench crop source; supports stable rations.
- Brine/Water Spring: cooking, farming, boilers, medicine, and chemical dilution.
- Compost Heap / Bone Meal Pit: optional farm booster and grim recycle loop later.

Important distinction:

- Food nodes should not output finished food directly. They provide seed stock, substrate, water, or nutrients. The farm machine plus essence creates reliable food.

Coal nodes:

- Coal Seam: primary coal source.
- Coke Yard output later: refined coal/coke for higher heat machines.
- Slag byproduct later: potential low-value construction filler or waste risk.

Essence nodes:

- Essence Seep: early low-output magical resource node.
- Willstone Vein: stronger but rarer essence-bearing node.
- Bone-Salt Sink: stabilizer node for late wards and binding.
- Warded Well: upgraded essence extraction point requiring construction and safety.

Other key raw nodes:

- Timber Stand: planks, braces, duckboards, crates.
- Scrap Heap: scrap iron, nails, crude casings, machine parts.
- Stone/Clay Pit: sandbags, brick, concrete, revetments.
- Niter Bed: powder and explosives.
- Sulfur Vent: powder, chemicals, medicine, pressure weapons.
- Copper Vein: wire, signal kits, coils, dynamos.
- Fiber Reed / Cloth Bale Node: uniforms, bandages, sandbags, filters.
- Medicinal Fungus Patch: medical chain.
- Clockwork Salvage: gears, springs, lenses, robotics, rangefinders.

Starter-map recommendation:

- Start with visible nodes for Fungal Loam, Brine/Water, Coal Seam, Essence Seep, Timber, Scrap, Stone/Clay, and Fiber.
- Add Niter/Sulfur/Copper after the first worker/food/coal/essence loop is readable.

## 5. Farm machine design: inputs, essence requirement, outputs, upgrades, risks

The farm machine should be the first TWB twist on the factory side: food is industrially grown with magical assistance, not merely picked from a field.

Tier I Farm Machine: Mudbed Farm

- Inputs: Fungal Loam or Root-Meal Stock, Brine/Water, Essence, worker labour.
- Output: Raw Food.
- Byproduct: Spoiled Food or Compost if underfed/unstable.
- Worker: Farmer or Labourer.
- Use: feeds worker meals and basic rations.

Why essence is required:

- Essence makes food growth fast enough to support a war factory.
- It also creates the first strategic conflict: do essence points feed people, or do they power magical military/industry systems?

Upgrades:

- Tier I: Hand-Tended Mudbed Farm. Low yield, high worker time.
- Tier II: Belt-Fed Grow Trough. Conveyor-friendly, better throughput.
- Tier III: Steam-Heated Greenhouse. Consumes coal/steam for improved yield and stability.
- Tier IV: Warded Essence Hothouse. Higher yield, lower spoilage, consumes wards/essence.
- Tier V: Strategic Ration Conservatory. Produces reserve food for long offensives and siege stockpiles.

Risks:

- Essence Blight: low warding or overdraw creates spoiled food and worker sickness.
- Overgrowth: farm blocks adjacent cells or slows workers until cleared.
- Contamination: bad water or unstable essence reduces ration quality.
- Worker fatigue: tired farmers reduce yield.
- Allocation trap: overfeeding the military starves the workers who make the food.

Outputs:

- Raw Food: base output.
- Worker Meals: direct factory consumption, low processing.
- Basic Rations: Tier I front food.
- Meal Tins: upward-crafting reserve for ration crates and replacement teams.
- Ration Crates: Tier II front food.
- Strategic Ration Reserves: Tier V offensive stockpile.

## 6. How food splits between workers and military units/teams

Food should have three allocations:

- Worker Food: keeps factory humans working.
- Front Food: supplies military teams, scouts, dig crews, assault teams, and supply teams.
- Craft Reserve: feeds higher-tier recipes, replacement teams, medical recovery, and strategic reserves.

Priority controls:

- Default: workers first to prevent silent factory collapse.
- Emergency Front: shifts food to military teams at the cost of worker fatigue and throughput.
- Industrial Reserve: holds food for ration crates, replacement teams, or strategic stockpiles.
- Split: percentage or simple thirds once the UI supports it.

Military team effects:

- Scouting teams consume food to extend patrol range and avoid fatigue.
- Dig-in teams consume food during long build jobs.
- Assault teams consume food quickly before and during attacks.
- Supply teams consume food while carrying goods forward.
- Low front food reduces morale recovery, increases retreat chance, and lowers cohesion.

Factory worker effects:

- Workers consume food continuously.
- Low worker food slows every production chain, including the farm itself.
- Worker starvation should be shown as a factory-side bottleneck, not hidden behind lower global output.

Diagnostic examples:

- "Workers fed for 82 ticks; front rations fed for 35 ticks."
- "Emergency front food active: factory speed -18 percent."
- "Farm stalled: Essence empty."
- "Porters hungry: delivery delay rising."

## 7. Coal-powered steam tech chain and which machines/transport need coal

Coal chain:

```text
Coal Seam
  -> Coal Yard
  -> Boiler / Furnace / Steam Engine House
  -> Steam
  -> Underground Steam Pipe Layer
  -> Machine Power, Heat, Boiler Fuel, Coke later
```

Design rule:

- Coal is the fuel, not the final power network.
- Boilers are the power producers.
- Underground steam pipes are the power distribution layer, replacing the usual diesel-generator-plus-power-cable abstraction.
- Coal can still be a material input for smelting, coke, chemistry, and steel production.

Coal users by tier:

- Tier I: limited heating/cooking if desired, but do not force coal too early unless the farm and food loop are already readable.
- Tier II: Small Boiler, early furnaces, metal pressing support, and early machines connected by simple boiler adjacency or short pipe links.
- Tier III: Steam Engine House, Chemical Vat, Shell Forge, Concrete Mixer, Powered Loaders, Steam Carts, underground steam-pipe junctions, and steam-powered conveyor drives.
- Tier IV: Spark Dynamo, Servo Foundry, Bulk Hauler Dock, Crawl-Hauler maintenance, heavy workshop power.
- Tier V: Grand Siege Press, Bombardment Foundry, Pneumatic Vault Tube Hub support, late heavy industry.

Steam transport:

- Powered Loaders: machine-to-belt/storage transfer.
- Steam Carts: depot-to-depot medium transport.
- Lift Platforms: over obstacles or factory levels if needed later.
- Bulk Hauler Dock support: coal/steam contributes to dock operations unless the specific hauler is essence-powered.

Coal shortage effects:

- Boilers idle or lose pressure.
- Canners and chemical machines slow.
- Shell and concrete output falls.
- Steam carts stop or switch to manual fallback if available.
- Worker demand may rise because manual hauling replaces powered tools.
- Underground steam-pipe breaks isolate machines even if coal exists.

## 8. Essence-powered magic chain and which machines/units need essence

Essence chain:

```text
Essence Seep / Willstone Vein
  -> Essence Tap
  -> Raw Essence
  -> Farm Machine / Wards / Aether Condenser / Command Relays
  -> Aether Batteries, Warded Goods, Bombardment Cores
```

Essence users:

- Farm Machine: required for food growth.
- Essence Tap/Condenser: extracts and refines magical supply.
- Warded Storage Vault: stabilizes volatile goods.
- Aether Condenser: makes Aether Batteries.
- Command Relay Spire: command coordination.
- Aether Searchlight: scouting/reveal.
- Clockwork Assembly Bay: late robotics support.
- War Choir Regulator: late command pulse.
- Binding Crucible: bombardment core stabilization.
- TWB units: Aether Lamp Scout, Choir-Major, Grave-Salt Warden, Bound Shell Cantor, pressure/warded support.

Essence shortage effects:

- Farms slow or stop.
- Magic units lose special behavior first, then become ordinary/fragile.
- Warded storage becomes riskier.
- Command relays lose range or pulse strength.
- Bombardment stability drops.

Essence risk:

- Essence should be powerful but not clean. Overdraw without wards should cause spoilage, machine stalls, misfires, worker sickness, or variance spikes.
- Early essence should be scarce enough that food production competes with magic. That conflict is the point, if one may be so unfashionably direct.

## 9. Trench-material audit: planks, sandbags, wire, duckboards, braces, concrete/revetments, tools, etc.

The construction category should be decomposed into visible trench goods.

Required trench goods:

- Planks: Timber -> Sawmill. Used for duckboards, braces, crates, trench walls, depots.
- Sandbags: Cloth/Fiber + Stone/Clay/Sand -> Sandbag Station. Used for scrapes, parapets, foxholes, bunker reinforcement.
- Wire Coils: Scrap Iron + Copper -> Wire Twister. Used for barbed wire, signal wire variants, defensive obstacles.
- Duckboards: Planks + Nails/Scrap -> Carpentry Bench. Used for movement in trenches, mud mitigation, supply speed.
- Trench Braces: Timber + Scrap -> Brace Bench. Used for fire trenches, reinforced trenches, dugouts.
- Concrete/Revetment Packs: Stone/Clay + Water + Coal + Scrap -> Concrete Mixer. Used for reinforced trenches, bunkers, gun pits.
- Hand Tools: Timber + Scrap -> Tool Bench. Used by workers, sappers, dig crews, repair jobs.
- Shovels/Picks: refined hand tools for faster digging.
- Drainage Pumps: Scrap + Copper + Coal/Steam -> Pump Workshop. Used to keep trenches from degrading in mud sectors later.
- Corrugated Plates: Scrap + Coal/Press -> Metal Press. Used for bunkers, dugouts, reinforced trench roofs.
- Gabion Baskets: Fiber + Timber -> Basket Bench. Intermediate half-cover/field works.
- Clearing Charges: Black Powder + Tools + Wire Kit -> Obstacle Workshop. Used by assault and dig teams.

Fortification mapping:

- Scrape: labour only or small hand tools.
- Foxhole: hand tools + sandbags.
- Fire Trench: planks + braces + sandbags + tools.
- Communication Trench: planks + duckboards + braces.
- Reinforced Trench: trench goods + concrete/revetments + corrugated plates.
- Wire: wire coils + posts/planks.
- Bunker: concrete/revetments + corrugated plates + braces + machine support.
- Dugout: braces + duckboards + corrugated plates + sandbags.
- MG Nest: sandbags + planks + machine support + ammo feed.
- Mortar/Gun Pit: planks + sandbags + concrete/revetments + tools.

Pauli report adjustment:

- "Trench Material Crates" can remain as a shipment category, but internally it should bundle visible goods. Early prototype may abstract it, but design memory should know the crate represents planks, sandbags, duckboards, braces, and tools.

## 10. Updated production flow chart showing workers + food/coal/essence + trench materials

```text
BASE NODES
  Fungal Loam / Root-Meal Stock
  Brine/Water
  Essence Seep
  Coal Seam
  Timber
  Scrap Iron
  Stone/Clay/Sand
  Fiber/Cloth
  Copper

WORKER SUSTAIN LOOP
  Fungal Loam + Water + Essence + Farmer Labour
    -> Farm Machine
    -> Raw Food
    -> Worker Meals
    -> Workers fed
    -> faster hauling, farming, construction, machine operation

FRONT FOOD LOOP
  Raw Food + Worker/Machine Processing
    -> Basic Rations
    -> Ration Crates
    -> Military Teams fed
    -> better scouting, morale, cohesion, digging endurance

COAL / STEAM LOOP
  Coal Seam
    -> Coal Yard
    -> Boiler / Steam Engine House
    -> Steam
    -> Underground Steam Pipe Layer
    -> Canners, Powder Mills, Concrete Mixers, Chemical Vats, Powered Loaders, Steam Carts, Steam Conveyor Drives

ESSENCE / MAGIC LOOP
  Essence Seep
    -> Essence Tap
    -> Farm Machine OR Aether Condenser OR Wards OR Command Relay
    -> Food growth / Aether Batteries / Warded Storage / Magic unit support

TRENCH MATERIAL LOOP
  Timber -> Sawmill -> Planks
  Fiber + Stone/Clay/Sand -> Sandbag Station -> Sandbags
  Scrap + Copper -> Wire Twister -> Wire Coils
  Planks + Scrap -> Carpentry Bench -> Duckboards / Braces
  Stone/Clay + Water + Coal + Scrap -> Concrete Mixer -> Concrete/Revetment Packs
  Timber + Scrap -> Tool Bench -> Hand Tools / Shovels

WAR TEAM SUPPORT
  Food -> Workers and Military Teams
  Coal -> Steam industry and heavy production
  Essence -> Farms, magic systems, wards, late command and siege
  Trench Goods -> Dig-in teams, emplacements, bunkers, trenches
  Ammo/Medical/Command -> Team combat and survival
```

## 11. UI/diagnostics needed for worker/resource playtesting

Top bar:

- Food stock.
- Worker food coverage.
- Front food coverage.
- Coal stock and steam power status.
- Underground steam-pipe coverage, pressure, and disconnected powered machines.
- Essence stock and essence demand.
- Worker fatigue average.
- Starving/idle/stalled worker count.

Bottom/build UI:

- Resource node layer.
- Worker/job layer.
- Food allocation button.
- Coal/steam layer.
- Underground steam-pipe layer.
- Essence/magic layer.
- Trench materials category.

Right tracker:

- Worker categories: assigned, idle, hungry, fatigued.
- Current bottleneck: food, coal, essence, labour, transport, storage.
- Farm machine status: has substrate, water, essence, worker, output blocked.
- Food allocation: workers/front/reserve.
- Coal chain status: miners, coal yard, boiler demand.
- Steam chain status: boiler output, water, coal, underground pipe connectivity, pressure, disconnected machines.
- Essence chain status: seep output, farm demand, magic demand, instability.
- Trench material stock: planks, sandbags, wire, duckboards, braces, concrete, tools.

Useful diagnostic strings:

- "Farm stalled: no essence."
- "Workers hungry: porter speed reduced."
- "Coal shortage: boiler pressure falling, canner slowed."
- "Steam pipe disconnected: powered conveyor idle."
- "Essence overdraw: farm spoilage risk rising."
- "Trench Works Team blocked: no planks."
- "MG Nest build blocked: sandbags and machine support missing."
- "Food split: workers 70 percent, front 20 percent, reserve 10 percent."

## 12. Balance risks/open questions

Risks:

- Food can become too punishing if workers and military teams both starve quickly.
- Essence can become over-centralized because it powers farms and magic.
- Coal and essence may feel redundant unless coal clearly means steam/heat and essence clearly means magic/growth/wards.
- Worker simulation can become noisy if every worker needs individual inspection.
- If workers are too abstract, the Tier 1 hand-economy fantasy weakens.
- If farms require too many inputs too early, the player may fail before understanding the factory.
- If trench goods are decomposed too soon, the UI may become a warehouse ledger with mud.
- If trench goods stay bundled forever, fortification choices lose texture.

Open questions:

- Should food spoil over time? Recommendation: not in the first slice.
- Should farms consume water as a real item or use local water access? Recommendation: item/canister first only if it is easy to diagnose; otherwise local water node adjacency.
- Should essence be mined by workers or passively tapped by machines? Recommendation: machine-tapped with Essence Tenders for maintenance.
- Should coal be finite nodes or slow-renewing shipments? Recommendation: finite local nodes plus later import/bulk logistics.
- Should workers be visible individuals or counted crews? Recommendation: visible Tier 1 porters and farmers first; abstract some later operators if performance suffers.

## 13. Recommended first implementation slice

Do not build the whole economy at once. First prove that workers eat, farms need essence, coal powers one machine path, and trench materials are more than a single vague crate.

Recommended first slice:

1. Add three tracked base resources: Food, Coal, Essence.
2. Add worker pool with simple job assignments: Porter, Farmer, Machine Operator.
3. Add worker food consumption and fatigue.
4. Add starvation slowdown, but no death/desertion yet.
5. Add resource nodes:
   - Fungal Loam or Root-Meal Stock.
   - Brine/Water.
   - Coal Seam.
   - Essence Seep.
   - Timber.
   - Scrap.
   - Stone/Clay.
   - Fiber.
6. Add a Tier I Farm Machine:
   - Food input node + Water + Essence + Farmer labour -> Raw Food.
7. Add food allocation:
   - Workers.
   - Front.
   - Reserve.
8. Add one steam-powered path:
   - Small Boiler consumes Coal and Water to produce Steam.
   - A short underground steam-pipe layer or adjacency prototype powers one machine such as a Ration Canner.
9. Add one essence-powered conflict:
   - Farm Machine consumes Essence, and another simple magic/war reserve also wants Essence.
10. Decompose trench materials into three first goods:
   - Planks.
   - Sandbags.
   - Wire Coils.
11. Keep old `Trench Materials` as a compatibility shipment category, but show what is inside it in diagnostics.
12. Add right-panel diagnostics for:
   - worker hunger/fatigue,
   - farm missing input,
   - food split,
   - coal shortage,
   - essence shortage,
   - trench material missing goods.

First pass success criteria:

- The player can see workers slow down when not fed.
- The player can see farms stop when essence is missing.
- The player must choose whether food goes to workers, front teams, or reserve.
- Boiler-fed steam visibly powers at least one production improvement.
- Essence visibly competes between farming and magic/war use.
- A dig-in/trench-related output requires planks/sandbags/wire rather than a nameless construction blob.

## Context sources read

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-crafting-logistics-design-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-crafting-logistics-tradeoff-addendum.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-military-units-fortifications-design-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-team-spawning-military-addendum.md`

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-worker-food-coal-essence-addendum.md`

## Checks run

- Read required project memory context.
- Read the crafting/logistics design report.
- Read the crafting trade-off addendum.
- Read the military units/fortifications report.
- Read the team-spawning military addendum.
- Confirmed this pass is design-only and did not edit Unity source or permanent memory.

## Cleanup performed

No temporary files, screenshots, throwaway logs, or generated dev artifacts were created.

## Memory-worthy notes

- Food should be produced by farm machines that require essence.
- Food must split between factory workers, military teams, and craft reserve.
- Coal should be the steam/heat fuel; boilers and underground steam pipes should be the actual machine-power network.
- Essence should be the magic/growth/warding resource.
- Worker fatigue and starvation should affect factory throughput before becoming catastrophic.
- Trench materials should be decomposed into planks, sandbags, wire, duckboards, braces, concrete/revetments, and tools.

## Anything blocked

Nothing blocked.
