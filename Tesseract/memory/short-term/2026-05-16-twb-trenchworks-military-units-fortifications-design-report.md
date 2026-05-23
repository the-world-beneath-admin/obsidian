# 2026-05-16 TWB Trenchworks Military Units And Fortifications Design Report

## Scope

Standalone Unity 2D TWB Trenchworks prototype under The World Beneath umbrella.

This is a design-only worker report. No Unity code was implemented. No permanent memory, wiki, index, hot, or log files were edited. This does not cover The World Beneath main Unity game, Glassroot Garden, The Alchemy Lab, TWB-Marketing, shared platform/accounts, pets, sprite-sheet automation, multiplayer, or production art.

## 1. Design goals and assumptions

The war side should become a readable agent-and-cell battlefield, not a moving progress bar with uniforms painted on. Units should occupy real squares, seek cover, spot, fire, panic, crouch, dig, man emplacements, and consume factory outputs.

Design goals:

- At least 25 frontline unit types across officers, normal soldiers, TWB twist units, engineers/support, and heavy/emplacement crews.
- Three military progression tiers that match the 5-tier factory economy without requiring the full factory to be implemented at once.
- One unit occupies one grid square.
- Units start above ground, scout, make contact, fight locally, and the winning side digs in.
- Victory remains total annihilation through enemy-base bombardment and destruction.
- Combat should feel organic, slow, supply-driven, and inspectable.
- WW1 technology is the base language: rifles, wire, trenches, mortars, field guns, machine guns, signal lines, stretcher lines, and logistics.
- The TWB twist should be mechanical: aether, bone-salt, command resonance, robotics, warding, and grim resource tradeoffs should change behavior and costs rather than simply renaming ordinary guns.

Assumptions:

- The current war map remains 400 wide x 200 high with 10 x 10 base areas.
- The current first slice already has cells, units, obstacles, contact, scouting, combat, and trench dig-in.
- The current factory research includes these useful supply categories: Manpower/Bodies, Ammunition, Food/Morale, Energy/Fuel, Construction/Trench Materials, Medical, Machine/Robotics Support, Command/Communication, Obstacle Operations, and Bombardment/Base Destruction.
- Exact item counts should wait until playtesting. This report uses relative costs and required categories instead of hard caps.

Pushback:

- Do not implement all 25 unit types at once. Design the full roster now, then implement a narrow template slice with a few units, cover states, and one or two emplacements. Otherwise the prototype will become a grand parade of half-behavior.

## 2. Cover model: exposed, half cover, full cover, crouched, head-up/firing states

Cover should be two linked concepts:

- Terrain cover: what the cell or fortification provides.
- Unit posture: what the unit is doing with that cover.

### Terrain cover states

Exposed:

- Open ground, road, shallow mud, cleared field, base floor, or broken ground with no meaningful protection.
- Good movement and visibility.
- High chance to be spotted, hit, and suppressed.
- Useful for movement, bad for staying alive.

Half cover:

- Shell hole lip, rubble pile, low wall, sandbag scrape, shallow foxhole, wire-adjacent crater, or obstacle edge.
- Reduces incoming hit chance and suppression modestly.
- Still allows firing and spotting without requiring a full trench position.
- Good for scouts and early contact, unreliable against machine guns or artillery.

Full cover:

- Proper trench, reinforced trench, bunker firing slit, dugout entrance, heavy ruin, prepared gun pit, or deep foxhole.
- Strongly reduces direct-fire hit chance when crouched.
- Requires the unit to go head-up to spot or fire effectively.
- Protects morale and allows resupply/recovery more safely.
- Full cover does not mean invulnerable. Artillery, flanking, close assault, gas/pressure weapons later, and sustained suppression can still force units out.

### Posture states

Head-up / firing:

- Unit can spot, aim, fire, throw grenades, observe artillery, signal, or operate an emplacement.
- Unit receives only partial benefit from cover because it is exposed enough to act.
- Suppression and hit chance rise while head-up.
- Required for meaningful attacks and spotting.

Crouched / hunkered:

- Unit prioritizes survival, morale recovery, reloading, first aid, resupply, or waiting for suppression to fade.
- Unit has poor spotting, poor firing, and cannot operate most direct-fire weapons.
- Direct-fire danger drops sharply in half/full cover.
- In exposed cells, crouching helps only slightly. One cannot crouch behind optimism.

Braced / working:

- Optional middle state for builders and emplacement crews.
- Unit is not firing much, but is digging, wiring, repairing, loading, or setting up an emplacement.
- More vulnerable than crouched, safer than head-up in full cover.
- Good for engineers and machine-gun/mortar crews.

### Practical posture rules

- Units pop head-up when they need to spot, fire, signal, or operate a weapon.
- Units crouch automatically when suppression is high, ammo is low, morale breaks, artillery lands nearby, or an officer orders "hold."
- Officers, medics, rations, and command relays can reduce time spent pinned.
- Scouts spend more head-up time, so they reveal ground but die if unsupported.
- Machine-gun crews need braced/head-up states to fire; if suppressed, they crouch and stop projecting fire.
- Artillery observers and signal units become high-value targets because they must go head-up to do their job.

## 3. Three military progression tiers

### Tier I - Patrol And Scrape War

Unlocked by early manpower, rations, loose ammo, field dressings, hand tools, and sandbags.

Battlefield identity:

- Scouts, riflemen, basic officers, early sappers, and medics.
- Units move above ground, find contact, survive with half cover, and dig foxholes after winning.
- Emplacements are rare or crude.
- The player learns that food, ammo, bodies, and construction supplies all matter.

### Tier II - Industrial Trench Line

Unlocked by ammo crates, ration crates, medical crates, trench material crates, wire coils, replacement squads, signal kits, shell crates, and repair kits.

Battlefield identity:

- Machine-gun nests, mortars, reinforced trenches, wire, observation posts, trained engineers, signallers, and artillery observers.
- Local contacts become sector fights.
- Holding ground depends on trench networks and supply reach.
- The front can bog down if construction and command are neglected.

### Tier III - Arcane Siege War

Unlocked by aether batteries, automata support packs, heavy shell crates, command relay kits, clearing charges, stabilized energy, siege shells, targeting kits, and bombardment cores.

Battlefield identity:

- TWB twist units, robotic engineering support, aether searchlights, command resonance, heavy emplacements, and base-kill preparation.
- Magic and robotics solve specific problems at high upkeep cost.
- The player chooses between spending advanced goods to keep the front alive or reserving them for final enemy-base annihilation.

## 4. Frontline unit roster: 25 unit types

These are unit templates for the eventual roster. The first implementation should start with a smaller subset.

### Officers - 5

1. Patrol Corporal - Tier I
   - Role: small local command for scouts and riflemen.
   - Behavior: keeps nearby units from scattering, improves retreat discipline, marks first contact zones.
   - Strengths: cheap command, good early scouting support.
   - Weaknesses: weak combat power, vulnerable if head-up too long.
   - Upkeep: Manpower, Food, Command.

2. Trench Lieutenant - Tier II
   - Role: sector commander.
   - Behavior: assigns hold/advance/dig priorities, rallies suppressed units, improves trench capture.
   - Strengths: makes defended sectors coherent.
   - Weaknesses: draws fire, poor alone.
   - Upkeep: Manpower, Food, Command, Medical.

3. Artillery Observer - Tier II
   - Role: spotter for mortars, field guns, and later bombardment.
   - Behavior: goes head-up in observation posts or cover, marks targets, improves shell accuracy.
   - Strengths: turns artillery from noise into pressure.
   - Weaknesses: high exposure while spotting, needs sight lines and signal support.
   - Upkeep: Manpower, Food, Command, Signal Kits, Medical.

4. Quartermaster Captain - Tier II
   - Role: forward logistics officer.
   - Behavior: improves local resupply, prioritizes ammo/ration/medical distribution, reduces stalled-unit reasons.
   - Strengths: makes supply effects visible and local.
   - Weaknesses: poor combat, useless if transport lines are broken.
   - Upkeep: Manpower, Food, Command, Rations.

5. Choir-Major - Tier III
   - Role: TWB command officer using aether/bone-salt resonance.
   - Behavior: sends short command pulses, reduces suppression, coordinates attacks, stabilizes bombardment windows.
   - Strengths: powerful sector-wide coordination.
   - Weaknesses: consumes energy and command seals; instability risk if under-supplied.
   - Upkeep: Manpower, Food, Energy, Command, Bone-Salt/Wards.

### Normal soldiers - 5

6. Rifleman - Tier I
   - Role: baseline combat unit.
   - Behavior: scouts short distances, fires in contact, digs weak foxholes after winning.
   - Strengths: cheap, flexible, easy to replace.
   - Weaknesses: suffers badly in exposed ground and against machine guns.
   - Upkeep: Manpower, Food, Ammo, Medical.

7. Scout - Tier I
   - Role: reveal unknown ground and find contact.
   - Behavior: moves ahead of safe territory, prefers cover, retreats if outnumbered.
   - Strengths: high vision and movement.
   - Weaknesses: low staying power, spends time head-up.
   - Upkeep: Manpower, Food, Ammo, Medical.

8. Grenadier - Tier II
   - Role: close assault and trench-clearing.
   - Behavior: closes on half/full cover, uses bombs to dislodge crouched defenders.
   - Strengths: breaks foxholes, MG nests, and trench cells.
   - Weaknesses: short range, high ammo/explosive demand, vulnerable crossing open ground.
   - Upkeep: Manpower, Food, Ammo, Obstacle Ops, Medical.

9. Bayonet Stormer - Tier II
   - Role: assault infantry for taking damaged positions.
   - Behavior: advances when enemy is suppressed, fights adjacent, captures trenches.
   - Strengths: useful after artillery or MG suppression.
   - Weaknesses: costly if sent before suppression.
   - Upkeep: Manpower, Food, Ammo, Medical.

10. Trench Marksman - Tier II
   - Role: long sight-line pressure.
   - Behavior: fires from half/full cover at exposed head-up units, observers, and officers.
   - Strengths: punishes careless spotting and command exposure.
   - Weaknesses: low rate of fire, poor at assaulting, needs line of sight.
   - Upkeep: Manpower, Food, Ammo, Command.

### Engineers and support - 5

11. Sapper - Tier I
   - Role: dig, clear, and convert terrain.
   - Behavior: builds foxholes/trenches faster, clears rubble/wire, starts saps.
   - Strengths: essential for turning victories into held ground.
   - Weaknesses: poor if left unsupported in contact.
   - Upkeep: Manpower, Food, Construction, Obstacle Ops, Medical.

12. Field Engineer - Tier II
   - Role: build durable works and emplacements.
   - Behavior: reinforces trenches, places wire, prepares MG/mortar pits, repairs base cells.
   - Strengths: unlocks the real defensive game.
   - Weaknesses: slow build jobs and high material use.
   - Upkeep: Manpower, Food, Construction, Machine Support, Medical.

13. Wire Cutter - Tier II
   - Role: obstacle breach specialist.
   - Behavior: cuts wire, marks breach lanes, clears tangle under cover.
   - Strengths: opens attacks without requiring shelling every obstacle.
   - Weaknesses: highly vulnerable while braced/working.
   - Upkeep: Manpower, Food, Obstacle Ops, Construction.

14. Signaller - Tier II
   - Role: local communication and command relay.
   - Behavior: lays signal wire, improves response to contact, calls support through command posts.
   - Strengths: makes unit groups less stupid.
   - Weaknesses: fragile, dependent on wire/relay integrity.
   - Upkeep: Manpower, Food, Command, Copper/Wire, Medical.

15. Combat Medic - Tier I
   - Role: reduce permanent losses and restore morale.
   - Behavior: moves behind contact, stabilizes wounded, boosts recovery in dugouts/aid posts.
   - Strengths: turns casualties into recoverable wounded.
   - Weaknesses: not a combat solution; needs medical supply.
   - Upkeep: Manpower, Food, Medical.

### Heavy and emplacement crews - 5

16. Machine-Gun Crew - Tier II
   - Role: suppression and lane denial.
   - Behavior: deploys in MG nest or prepared trench cell, fires in arcs, suppresses exposed/head-up units.
   - Strengths: dominates open ground and wire lanes.
   - Weaknesses: setup time, ammo hungry, vulnerable to flanking, mortars, grenadiers, and artillery observers.
   - Upkeep: Manpower, Food, Ammo, Machine Support.

17. Trench Mortar Crew - Tier II
   - Role: short indirect fire.
   - Behavior: fires over cover at nearby trenches, MG nests, and obstacle clusters.
   - Strengths: breaks static local fights.
   - Weaknesses: needs ammo, spotting, and reload time.
   - Upkeep: Manpower, Food, Ammo/Shells, Command.

18. Field Gun Crew - Tier II
   - Role: direct/indirect heavy sector fire.
   - Behavior: occupies prepared gun pit, damages bunkers, trenches, and base-adjacent targets.
   - Strengths: high damage, foundation for bombardment.
   - Weaknesses: expensive, immobile once emplaced, needs observers.
   - Upkeep: Manpower, Food, Shell Crates, Machine Support, Command.

19. Bombardment Crew - Tier III
   - Role: base-destruction logistics and firing crew.
   - Behavior: operates siege guns or base-breach machinery once targeting and shells are ready.
   - Strengths: required for final victory path.
   - Weaknesses: consumes late-tier goods; weak without rangefinding and protection.
   - Upkeep: Manpower, Food, Bombardment, Energy, Command.

20. Pressure Projector Crew - Tier III
   - Role: short-range bunker/trench denial using steam/chemical/aether pressure.
   - Behavior: attacks full-cover cells at close range, forces crouched defenders to retreat.
   - Strengths: answers over-fortified cells.
   - Weaknesses: dangerous, short range, high fuel/energy cost, friendly-risk if mishandled.
   - Upkeep: Manpower, Food, Energy/Fuel, Chemical Reagent, Medical.

### TWB twist units - 5

21. Aether Lamp Scout - Tier III
   - Role: reveal concealed units, night/fog counters later.
   - Behavior: goes head-up with an aether lamp, reveals crouched enemies and hidden trenches in a cone/radius.
   - Strengths: counters ambush and improves artillery spotting.
   - Weaknesses: visible target, energy hungry.
   - Upkeep: Manpower, Food, Energy, Command.

22. Clockwork Trenchhand - Tier III
   - Role: robotic support builder.
   - Behavior: digs, hauls, repairs, and clears obstacles with low morale concerns.
   - Strengths: tireless engineering support under moderate fire.
   - Weaknesses: needs repair kits, energy, servo parts; vulnerable to heavy damage.
   - Upkeep: Energy, Machine Support, Repair Kits, Command.

23. Grave-Salt Warden - Tier III
   - Role: morale/warding specialist.
   - Behavior: stabilizes nearby units, reduces panic, protects dugouts and command posts from aether instability.
   - Strengths: keeps grim late-war machinery from collapsing morale and safety.
   - Weaknesses: little direct combat; rare resource dependence.
   - Upkeep: Manpower, Food, Bone-Salt/Wards, Energy.

24. Echo Runner - Tier III
   - Role: dangerous command courier.
   - Behavior: moves through trench networks carrying command echoes, improves response time where signal lines are cut.
   - Strengths: keeps isolated sectors active.
   - Weaknesses: fragile, high morale risk, limited use in open ground.
   - Upkeep: Manpower, Food, Command, Medical.

25. Bound Shell Cantor - Tier III
   - Role: final bombardment stabilizer.
   - Behavior: prepares siege shells and reduces bombardment variance/misfire chance.
   - Strengths: makes base destruction reliable.
   - Weaknesses: costly, late-game, poor battlefield value outside siege systems.
   - Upkeep: Manpower, Food, Energy, Bone-Salt/Wards, Bombardment.

## 5. Role behavior summary and resource upkeep

The war should not ask the player to build "25 units" as isolated collectibles. It should ask for roles that compete for the same production categories.

Role groups:

- Line combat: Rifleman, Grenadier, Bayonet Stormer, Trench Marksman.
- Recon/contact: Scout, Aether Lamp Scout, Patrol Corporal.
- Command/coordination: Patrol Corporal, Trench Lieutenant, Quartermaster Captain, Choir-Major, Signaller, Echo Runner.
- Digging/engineering: Sapper, Field Engineer, Wire Cutter, Clockwork Trenchhand.
- Recovery/sustain: Combat Medic, Quartermaster Captain, Grave-Salt Warden.
- Suppression/heavy fire: Machine-Gun Crew, Mortar Crew, Field Gun Crew, Pressure Projector Crew.
- Final victory support: Artillery Observer, Bombardment Crew, Bound Shell Cantor, Field Gun Crew.

Resource pressure by role:

- Manpower: all human units.
- Food/Morale: all human units, especially scouts, assault units, officers, and medics.
- Ammunition: riflemen, scouts, grenadiers, marksmen, machine guns, mortars, field guns.
- Construction: sappers, engineers, fortifications, gun pits, trench upgrades.
- Medical: keeps line units, officers, medics, and assault units from becoming permanent losses.
- Command/Communication: officers, observers, signallers, echo runners, bombardment operations.
- Energy/Fuel: TWB twist units, pressure projectors, searchlights, robotics, siege systems.
- Machine/Robotics Support: clockwork units, emplacements, field guns, bulk repair.
- Obstacle Operations: wire cutters, sappers, clearing charges, grenadiers.
- Bombardment: field gun escalation, bombardment crews, shell cantors, final base-breach chain.

Recommended rule:

- A unit can exist with minimum supply, but it should not perform all roles well unless its upkeep categories are available. For example, a Machine-Gun Crew without ammo becomes a frightened picnic table; very historical, but not useful.

## 6. Fortifications list and play effects

Foxhole:

- Built by Riflemen slowly; Sappers quickly.
- One-cell half cover; becomes near-full safety when crouched but weak against artillery.
- Good first dig-in after winning contact.

Shallow Scrape / Shell Scrape:

- Built quickly by any infantry.
- Temporary half cover.
- Low material cost, low durability.

Fire Trench:

- Built by Sappers/Engineers.
- One-cell full cover with firing position.
- Enables safer movement along connected trench cells.
- Units crouched inside are hard to hit; head-up units can fire and spot.

Communication Trench:

- Built by Sappers/Engineers.
- Full-cover movement link with worse firing value than fire trench.
- Improves reinforcement, retreat, and resupply.

Reinforced Trench:

- Built by Engineers with construction materials and concrete/revetment packs.
- Strong full cover, better artillery resistance, better morale recovery.
- Slower and more expensive.

Sandbag Wall / Parapet:

- Built by Riflemen/Sappers/Engineers.
- Half cover on cell edge or cell.
- Fast defensive improvement, vulnerable to artillery and pressure weapons.

Barbed Wire / Scrap Wire:

- Built by Engineers/Sappers with wire coils.
- Slows or blocks movement; poor cover.
- Strong with machine guns because it holds targets in exposed/head-up lanes.

Rubble Barricade:

- Built by Engineers or converted from obstacles.
- Half cover, partial line-of-sight blocker, movement penalty.
- Cheap if rubble exists.

Dugout:

- Built by Engineers/Sappers in trench cells.
- Full safety/recovery structure, not a firing position.
- Improves morale recovery, medical stabilization, and artillery survival.

Bunker / Pillbox:

- Built by Engineers with concrete packs, machine support, and time.
- Full cover with firing slit.
- Strong MG/marksman position, weak to artillery, grenadiers, pressure projectors, and flanking.

Observation Post:

- Built by Engineers/Signallers/Observers.
- Half/full cover depending quality.
- Increases spotting/rangefinding but requires head-up exposure.

Listening Post:

- Built by Scouts/Sappers.
- Concealed forward position.
- Improves contact detection before visual spotting.

Aid Post:

- Built by Medics/Engineers in safe trench network.
- Increases wounded stabilization and return rate.
- Requires medical supplies and food.

Ammunition Niche:

- Built by Engineers/Quartermasters.
- Local ammo buffer inside trench network.
- Risk: explosive if hit by artillery or pressure weapons.

Command Post:

- Built by Engineers/Signallers/Officers.
- Improves local orders, rally, response to contact, and sector diagnostics.
- Requires command supplies.

Aether Relay Shrine:

- Built by Engineers/Choir-Major/Grave-Salt Warden.
- Tier III command/energy node.
- Boosts coordination and TWB units but consumes/stores volatile energy.

## 7. Emplacements

Light Machine-Gun Nest:

- Built by Field Engineers or Sappers; operated by Machine-Gun Crew.
- Requires ammo crates, construction materials, machine support.
- Creates suppression cone/arc.
- Excellent against exposed or wire-stalled units.

Heavy Machine-Gun Bunker:

- Built by Engineers; operated by Machine-Gun Crew.
- Requires concrete/revetment packs, machine support, ammo, time.
- Stronger arc, full cover, high suppression.
- Expensive and vulnerable to mortars/field guns.

Trench Mortar Pit:

- Built by Engineers/Sappers; operated by Mortar Crew.
- Requires construction materials and shell/ammo supply.
- Indirect fire against cover, wire, and clustered contact zones.
- Needs spotter or recent sighting for accuracy.

Field Gun Pit:

- Built by Engineers; operated by Field Gun Crew.
- Requires concrete/revetment packs, shell crates, machine support, command.
- Damages bunkers, reinforced trenches, and later base-adjacent targets.
- Needs artillery observer/signaller support to be reliable.

Siege Gun Platform:

- Tier III; built by Engineers, Bombardment Crew, and Clockwork Trenchhands.
- Requires siege shells, bombardment cores, targeting kits, energy, command.
- Supports victory path against enemy base.
- Must be protected by trenches, wire, MGs, and logistics.

Signal/Spotter Post:

- Built by Signallers/Engineers; operated by Signaller or Artillery Observer.
- Requires copper/signal kits and command supply.
- Improves artillery accuracy and reinforcement response.

Aether Searchlight:

- Tier III; built by Engineers and Aether Lamp Scouts.
- Requires energy, copper, machine support, command.
- Reveals crouched/hidden units and improves night/fog/low-visibility spotting later.
- Makes its own cell a target.

Clockwork Loader Station:

- Tier III; built by Engineers/Clockwork Trenchhands.
- Requires automata support packs, repair kits, energy.
- Improves field gun, siege gun, and mortar reload speed.

Warded Shell Cache:

- Tier III; built by Engineers and Grave-Salt Wardens.
- Requires shells, ward plates/bone-salt, construction.
- Local bombardment stockpile with reduced misfire/explosion risk.

Pressure Projector Pit:

- Tier III; built by Engineers; operated by Pressure Projector Crew.
- Requires fuel/energy, chemical reagent, machine support.
- Forces defenders out of full cover at short range.
- Dangerous and expensive; should not replace normal assault planning.

## 8. Resource and production requirements mapped from crafting tiers

Tier I military support:

- Units: Rifleman, Scout, Patrol Corporal, Sapper, Combat Medic.
- Fortifications: scrape, foxhole, sandbag wall.
- Inputs: Recruits, Basic Rations, Loose Cartridges, Field Dressings, Hand Tools, Sandbag Bundles.
- Factory pressure: send these to front for survival or reserve for industrial chains.

Tier II military support:

- Units: Trench Lieutenant, Artillery Observer, Quartermaster Captain, Grenadier, Bayonet Stormer, Trench Marksman, Field Engineer, Wire Cutter, Signaller, Machine-Gun Crew, Mortar Crew, Field Gun Crew.
- Fortifications: fire trench, communication trench, reinforced trench, wire, bunker, observation post, aid post, ammunition niche, command post.
- Inputs: Ammo Crates, Ration Crates, Medical Crates, Trench Material Crates, Wire Coils, Signal Kits, Shell Crates, Field Hospital Kits, Repair Kits.
- Factory pressure: immediate front stability competes with reserving fuses, steam, precision gears, and reinforced frames for Tier III.

Tier III military support:

- Units: Choir-Major, Bombardment Crew, Pressure Projector Crew, Aether Lamp Scout, Clockwork Trenchhand, Grave-Salt Warden, Echo Runner, Bound Shell Cantor.
- Fortifications/emplacements: aether relay shrine, aether searchlight, clockwork loader station, siege gun platform, warded shell cache, pressure projector pit.
- Inputs: Aether Batteries, Stabilized Energy, Automata Support Packs, Command Relay Kits, Heavy Shell Crates, Clearing Charges, Siege Shells, Targeting Kits, Bombardment Cores, Bone-Salt/Wards.
- Factory pressure: using these at the front delays final annihilation machinery.

Recommended production structure:

- Manpower chain feeds all human units and replacement flow.
- Ammo chain splits into rifle ammo, machine-gun belts, grenades, shells, siege shells.
- Food chain feeds fatigue, morale, replacement training, and offensive stockpiles.
- Construction chain feeds cover, trenches, wire, bunkers, gun pits, and base repair.
- Medical chain feeds wounded recovery and casualty reduction.
- Command chain feeds officers, signallers, observers, relays, and bombardment control.
- Energy/robotics chain feeds TWB units, clockwork support, pressure weapons, searchlights, and siege systems.
- Bombardment chain consumes late-tier shells, targeting, energy, and command to destroy enemy base cells.

## 9. Build rules: who builds what, time, and resulting terrain

Build rules should be simple enough to simulate and inspect:

- Any infantry can build a scrape if it has time and is not under heavy suppression.
- Riflemen can build foxholes slowly.
- Scouts can build listening posts and emergency scrapes.
- Sappers build foxholes, fire trenches, communication trenches, wire breaches, and early obstacle conversions.
- Field Engineers build reinforced trenches, bunkers, gun pits, command posts, aid posts, ammunition niches, and advanced emplacements.
- Wire Cutters remove wire and create breach markers; they do not build heavy works.
- Signallers build or repair signal posts and command links.
- Medics build aid posts only if protected by nearby trench/control.
- Machine-Gun, Mortar, Field Gun, Pressure Projector, and Bombardment Crews can unpack/operate their weapons only in a prepared position.
- Clockwork Trenchhands accelerate engineering jobs but need energy/repair support.
- Grave-Salt Wardens and Choir-Majors are required for volatile Tier III relay/ward/bombardment structures.

Build time bands:

- Immediate: crouch, head-up, use existing cover.
- Fast: scrape, emergency foxhole, simple breach marker.
- Medium: foxhole, sandbag wall, wire, listening post.
- Slow: fire trench, communication trench, MG nest, mortar pit, aid post.
- Very slow: reinforced trench, bunker, field gun pit, command post, aether relay, siege platform.

Terrain result examples:

- Scrape: exposed cell becomes half cover.
- Foxhole: exposed/half cover cell becomes stronger half cover; crouched unit gains near-full safety.
- Fire trench: cell becomes full cover with firing value.
- Communication trench: cell becomes full cover with movement/resupply value.
- Wire: cell or edge becomes movement blocker/slow zone with poor cover.
- Bunker: cell becomes full cover firing position; may require multi-cell footprint later.
- Dugout: trench cell becomes recovery/protection cell with little firing value.
- Gun pit: cell becomes emplacement socket; crew and weapon consume supply to fire.

Suggested interruption rules:

- Suppression slows or pauses building.
- Direct damage can reduce progress.
- Officers/command posts can prioritize build jobs.
- Construction shortages downgrade builds: trench order may create only a scrape/foxhole if materials run dry.
- Building creates noise and can draw enemy scouting/contact.

## 10. Interaction with current agent-based war simulation

The current first slice already supports units, cells, obstacles, cover/trench state, contacts, and base zones. The next design step should extend those concepts, not replace them.

Recommended data extensions:

- Unit template: type, tier, role, supply needs, posture behavior, build skills, weapon profile.
- Posture state: head-up, crouched, braced/working.
- Cover state: exposed, half, full, plus source type.
- Fortification state: none, scrape, foxhole, trench, reinforced trench, bunker, etc.
- Emplacement state: unbuilt, building, built, crewed, supplied, firing, damaged.
- Build job: requested structure, builder unit id, material state, progress, interruption reason.
- Supply reach: local availability of ammo, food, medical, construction, command, energy.
- Reason strings: "crouched: suppressed by MG," "head-up: spotting for mortar," "building wire: construction available," "emplacement idle: no shell crates."

Simulation behavior:

- The "front" remains a derived summary from controlled cells, trench networks, contact zones, and base pressure.
- Unit combat uses cover and posture. A crouched unit in full cover should survive but contribute little fire.
- Machine guns and artillery should change behavior by suppressing or damaging cells, not by simply subtracting global health.
- Emplacements need crew, structure, ammo, sighting/command, and resupply.
- Fortifications should affect pathing, morale, resupply, firing, and spotting.
- Bombardment readiness should eventually depend on held positions, observer/targeting network, shell supply, energy, command, and siege emplacement state.

Performance warning:

- Do not run full-map scans for every unit. Use local neighborhoods, sector caches, contact markers, and event-driven updates. The 400 x 200 map is large enough to punish undisciplined loops, as it should.

## 11. UI and diagnostics needed for playtesting

Bottom-row war layer buttons:

- Units
- Cover
- Fortifications
- Emplacements
- Supply reach
- Contacts
- Build jobs
- Bombardment

Top bar:

- Player base health
- Enemy base health
- Active contacts
- Units active / wounded / pinned
- Ammo, Food, Construction, Medical, Command, Energy status
- Bombardment readiness

Right tracker:

- Selected sector status
- Pinned unit groups
- Current shortage effects
- Active build jobs
- Emplacements idle/firing/no-ammo/no-crew
- Fortifications under construction/damaged
- Recent combat explanation

Cell inspector:

- Coordinates
- Occupant
- Terrain cover
- Posture
- Fortification
- Emplacement
- Supply reach
- Last contact
- Build job progress

Unit inspector:

- Unit type and tier
- Health, morale, suppression, fatigue
- Posture: head-up/crouched/braced
- Current order
- Current reason string
- Upkeep shortages
- Build permissions
- Weapon/emplacement status

Essential diagnostic strings:

- "MG nest idle: no ammo crates."
- "Mortar inaccurate: no observer line."
- "Rifleman crouched: suppression high."
- "Sapper paused: construction supply empty."
- "Field gun firing: observer + shell supply available."
- "Bombardment delayed: targeting kit missing."

## 12. Balance risks and open questions

Risks:

- Too many unit templates too early will hide whether the core cover/posture model works.
- Machine guns can dominate the game if wire and suppression are strong but artillery/grenadiers/flanking are weak.
- Artillery can erase trench play if too accurate or too cheap.
- Full cover can create stalemates unless mortars, engineers, pressure projectors, and supply attrition matter.
- TWB units can become magical soup if aether solves scouting, command, building, and bombardment with one resource.
- Manpower spam can overwhelm tactical readability unless food, command, medical, and equipment gate unit quality.
- Emplacements can become set-and-forget turrets unless crew, ammo, visibility, and vulnerability are all modeled.
- Posture can become invisible unless the UI clearly shows crouched/head-up state.
- A slow organic war can feel dead if patrols, contact markers, build jobs, and reason strings are not visible.

Open questions:

- Should units represent individual soldiers or small squads? Recommendation: treat each visible unit as a small tactical counter, not one literal human, while keeping one unit per square.
- Should the player directly order units, or only supply/doctrine them? Recommendation: start with supply/doctrine plus sector priorities, not RTS micromanagement.
- Should enemy units use the full same roster? Recommendation: start with mirrored basic unit templates plus a simpler NPC supply curve.
- How deadly should artillery be against crouched full-cover units? Recommendation: damaging and suppressive, but not instantly deleting reinforced positions unless support chains are strong.
- Should pressure weapons be chemical, steam, aether, or all three? Recommendation: start with "pressure projector" as a dark industrial tool and decide exact flavor later.
- How many units should be active at once? Recommendation: stay in tens to low hundreds until pathing, diagnostics, and performance are proven.

## 13. Recommended first implementation slice

First slice goal: prove cover/posture, build jobs, and one emplacement loop. Do not add the full roster yet.

Recommended unit subset:

- Rifleman
- Scout
- Patrol Corporal
- Sapper
- Combat Medic
- Machine-Gun Crew
- Trench Mortar Crew
- Field Engineer

Recommended cover/fortification subset:

- Exposed
- Half cover
- Full cover
- Crouched
- Head-up/firing
- Scrape
- Foxhole
- Fire trench
- Wire
- Light Machine-Gun Nest
- Trench Mortar Pit

Recommended supply subset:

- Manpower
- Ammo
- Food
- Construction
- Medical
- Command

Recommended behavior checks:

- Units in exposed cells die/suppress faster than units in half cover.
- Crouched units in full cover survive but stop contributing much fire/spotting.
- Riflemen can dig weak foxholes after contact.
- Sappers build better trenches faster if construction supply exists.
- Wire slows enemy movement and makes machine-gun fire matter.
- Machine-Gun Crew requires nest, crew, ammo, and head-up/braced state to suppress.
- Mortar Crew can damage/suppress a covered cell if a scout/officer/observer has a recent sighting.
- Medics reduce permanent losses only if medical supply exists.
- Patrol Corporal reduces panic and improves local response to contact.

Success criteria:

- A playtester can click a unit and understand why it is crouching, firing, digging, pinned, or idle.
- A playtester can see why shipping construction materials changes the battlefield.
- Machine-gun and mortar emplacements feel powerful but conditional.
- The war looks like units contesting terrain, not a solid line dressed up as a battlefield.

## Context sources read

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-war-agent-simulation-design-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-war-agent-first-slice-implementation-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-crafting-logistics-design-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-crafting-logistics-tradeoff-addendum.md`

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-military-units-fortifications-design-report.md`

## Checks run

- Read required project memory context.
- Read the current war-agent design report.
- Read the current war-agent first-slice implementation report.
- Read the current crafting/logistics design report.
- Read the crafting/logistics trade-off addendum.
- Confirmed this pass is design-only and did not edit Unity source or permanent memory.

## Cleanup performed

No temporary files, screenshots, throwaway logs, or generated dev artifacts were created.

## Memory-worthy notes

- The next military design layer should add cover plus posture before adding many new weapons.
- Half cover and full cover should be distinct from crouched/head-up behavior.
- Machine guns, mortars, field guns, and siege weapons should require crew, built emplacement, supply, and spotting/command support.
- Unit costs should compete for the same factory categories that also feed higher-tier crafting.
- TWB twist units should solve specific tactical/logistical problems at high energy, command, warding, and maintenance cost.
- Final victory should depend on siege/bombardment support chains, not merely more frontline soldiers.

## Anything blocked

Nothing blocked.
