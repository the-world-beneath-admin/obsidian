# 2026-05-16 TWB Trenchworks War Agent Simulation Design Report

## Scope

Standalone Unity 2D TWB Trenchworks prototype under The World Beneath umbrella.

This report does not cover The World Beneath main Unity game, Glassroot Garden, The Alchemy Lab, TWB-Marketing, shared platform/accounts, pets, sprite-sheet automation, multiplayer, or production art. No code was implemented.

## 1. Core loop for war simulation

The war should become an agent-and-cell simulation rather than a single front-progress value.

Core loop:

1. Each faction begins in a 10 x 10 base area on opposite sides of the 400 x 200 war map.
2. Units spawn above ground inside their base area, one unit per square.
3. Units scout outward from known safe cells, biased by doctrine, nearby allies, last sightings, obstacles, and supply state.
4. Fog-of-war and faction memory determine what each side knows. Units should not magically know the enemy location.
5. When scouts or patrols spot enemies, the local area becomes a contact zone.
6. Units in the contact zone fight, suppress, retreat, reinforce, or attempt to flank based on local state.
7. The side that holds the contact zone after the fight digs in and starts a trench/foxhole position.
8. Trenches connect into networks over time, creating safer movement and better defensive positions.
9. Factory supplies change how well the player faction scouts, fights, digs, recovers, reinforces, and eventually bombards the enemy base.
10. Victory remains total annihilation through enemy-base destruction, but the path to bombardment should emerge from local scouting, fighting, trenching, and supply pressure.

The important design correction: the "front" becomes a summary derived from units, trenches, control, and contact zones. It should not be the source of truth.

Recommended tick shape:

- Tactical tick: frequent, handles unit movement, scouting, spotting, combat, digging, obstacle clearing, and resupply.
- Strategic tick: slower, handles faction doctrine, supply allocation, spawn/requisition choices, sector priorities, and battle summaries.
- Renderer/UI tick: displays snapshots, events, overlays, and diagnostics without mutating simulation state.

The war should feel slow and organic. A good session should include probing, contact, withdrawals, partial trench creation, failed attacks, quiet sectors, sudden clashes, and eventual industrial pressure. Not a five-minute line race, if one may be spared such vulgarity.

## 2. Map model and starting layout

Use the current target war map size:

- Width: 400 cells.
- Height: 200 cells.
- Player base: 10 x 10 controlled area near the left side.
- Enemy base: 10 x 10 controlled area near the right side.

Recommended initial placement:

- Player base centered vertically, offset slightly in from the left edge.
- Enemy base centered vertically, offset slightly in from the right edge.
- Each base has an inner 10 x 10 spawn/control zone and a surrounding reserve/security ring.
- No randomly placed obstacle should fully block a base entrance.

Cell state should include:

- Surface terrain type.
- Obstacle type, if any.
- Cover value.
- Movement cost.
- Line-of-sight obstruction.
- Current controlling faction, if known.
- Faction influence values.
- Scouted/known state per faction.
- Last enemy sighting tick per faction.
- Trench/foxhole/dugout state.
- Occupying unit id, if any.
- Recent combat marker.
- Optional underground state later, even if the first slice uses surface only.

The base should not be a single abstract health number forever. It can retain a displayed integrity value for the top UI, but in the richer model that integrity should eventually derive from damage to cells, structures, depot nodes, and bombardment progress inside the 10 x 10 base area.

## 3. Unit model and per-tick behavior

One unit occupies one square. Friendly units should not overlap. Enemy units should not occupy the same cell unless the design explicitly adds close assault resolution, which should wait.

Recommended initial unit roster:

- Line infantry: basic scouting, fighting, and emergency digging.
- Sappers/diggers: faster trench work, obstacle clearing, sap/tunnel work later.
- Engineers: stronger fortifications, repairs, obstacle conversion, base repairs.
- Medics/quartermasters: recovery, morale, fatigue and local supply support.
- Command units: assign mission priorities and coordinate local groups; still occupy a cell.

Unit state should include:

- Faction.
- Unit type.
- Grid position.
- Health.
- Morale.
- Suppression.
- Fatigue.
- Ammo state.
- Local supply state.
- Current order/state.
- Current target cell or sector.
- Vision range.
- Noise/signature.
- Digging skill.
- Obstacle clearing skill.
- Last enemy sighting.
- Cooldowns for move, fire, dig, clear, resupply, and retreat.

Basic per-tick state machine:

1. Validate occupancy and whether the unit is alive, wounded, suppressed, or retreating.
2. Consume small amounts of local supply/fatigue budget as needed.
3. Observe nearby cells and update faction memory.
4. If enemy contact exists, resolve fight/retreat/reinforce/dig decisions.
5. If no contact exists, continue assigned scout/explore/hold/clear/dig behavior.
6. If the unit wins or holds a contested area, consider digging in.
7. If ammo, morale, or health drops too low, retreat toward friendly trench/base/supply.

Units should produce reason strings for diagnostics:

- "scouting unknown ground"
- "holding cover after contact"
- "digging foxhole after winning contact"
- "retreating: ammo low"
- "stalled: blocked by obstacle"
- "waiting: trench materials exhausted"

These reason strings are not ornamental. They are how the prototype avoids becoming a moody little box of secrets.

## 4. Scouting/exploration rules

Scouting should be semi-random, not purely random.

Each faction has map memory:

- Unknown cells.
- Scouted cells.
- Known obstacle cells.
- Recent enemy sightings.
- Known trenches.
- Known danger/contact zones.
- Friendly safe routes.

Scout behavior:

- Units start above ground inside base.
- Early units choose exploration targets at the edge of known safe/scouted territory.
- Movement is biased outward from base, but not always straight toward the enemy.
- Units avoid overcrowding by preferring cells with fewer nearby friendlies.
- Units prefer cover when moving through uncertain ground.
- Units investigate sound/contact markers if doctrine allows.
- Cautious doctrine sends smaller probes and digs earlier.
- Aggressive doctrine pushes farther before digging.
- Bombard doctrine still needs scouting to identify viable approach and pressure lanes.

Spotting/contact:

- A unit spots enemies within vision range if line of sight is not blocked.
- Obstacles, trenches, cover, weather later, and suppression can reduce spotting.
- First contact should create a contact marker rather than instantly dragging the whole army into a fight.
- Nearby units may respond to contact based on command priority, morale, and supply.

Scouting must be slow enough that the player watches sectors emerge. The first few minutes should feel like patrols probing a dangerous map, not two perfect swarms sprinting into the center.

## 5. Contact/fighting rules

Contact begins when a unit sees an enemy, takes fire, discovers an enemy trench, or attempts to move into a contested/blocked lane.

Combat should be local:

- Units fight across short range, not across the whole map.
- Adjacent or line-of-sight cells form a contact zone.
- Nearby allied units may join if they can path in and are not suppressed, exhausted, or blocked.
- Fights can end in death, retreat, suppression, stalled firefight, or one side holding the ground.

Suggested combat resolver:

- Build a local deterministic score from unit state and supplies.
- Apply a bounded seeded-random variance.
- Resolve casualties, suppression, morale loss, ammo usage, and retreat chance.

Deterministic factors should dominate:

- Ammo availability.
- Unit health and type.
- Number of participating units.
- Cover/trench protection.
- Morale and fatigue.
- Command support.
- Medical/ration support.
- Supply distance from base/trench network.
- Obstacle and terrain advantage.
- Flank exposure.

Random factor:

- Seeded, bounded, and logged.
- Target the locked design direction: roughly 80 percent supply/state driven and 20 percent variance.
- Randomness should change the texture of an encounter, not reverse every obvious advantage.

A useful formula shape:

```text
EffectivePower =
  UnitBasePower
  * HealthFactor
  * AmmoFactor
  * MoraleFactor
  * FatigueFactor
  * CoverOrTrenchFactor
  * CommandFactor
  * LocalSupplyFactor
  * SeededFrictionFactor
```

Battle reports should explain outcomes:

- "Contact won: two rifle units had cover, ammo was sufficient, enemy morale broke."
- "Advance stalled: enemy obstacle cover high, trench materials low, random friction minor."
- "Unit retreated: health low, no medic support, nearby command absent."

The player does not need every decimal. They need enough cause and effect to trust the machine.

## 6. Digging/trench creation rules

The winning side after contact should not simply own empty land. It should dig in.

Digging stages:

1. Scrape or foxhole: quick, weak cover.
2. Trench: slower, better cover and safer movement.
3. Reinforced trench: requires construction supplies and engineer/sapper help.
4. Dugout/support position later: stronger against bombardment and supports local resupply.

When units dig:

- After winning contact.
- When ordered to hold a sector.
- When under repeated fire.
- When waiting near a dangerous unknown edge.
- When command doctrine favors cautious or balanced advance.
- When supply pressure allows construction.

Digging costs:

- Time.
- Fatigue.
- Trench materials/construction supply for stronger stages.
- Exposure risk while digging.

Trench network rules:

- Adjacent friendly trenches connect into a network.
- Connected trenches improve movement safety, resupply, morale, and reinforcement speed.
- Captured trenches can be reused after a contested/capture delay.
- Bombardment and heavy fighting can damage trench strength.
- Abandoned trenches remain on the map as terrain, possibly cover for either side.

Important first-slice simplification:

- Let line infantry dig weak foxholes.
- Let sappers/engineers build stronger trenches faster.
- Do not add complex underground combat yet.
- Track underground-ready data later, but make the first implementation surface-only unless the code shape makes underground cheap.

## 7. Obstacle/cover/removal rules

Obstacles should create organic battle shape. They should not just be decorative clutter.

Obstacle types for the prototype:

- Rubble or ruined barricade: medium movement cost, good cover, partially blocks line of sight.
- Deadfall/tangle: slows movement, light cover, can be cleared.
- Wire/scrap tangle: blocks or strongly slows movement, poor cover, good defensive obstacle.
- Crater/mud: high movement cost, light cover, can channel movement.
- Ruined structure/rock pile: strong cover, blocks sight, slow or costly to clear.

Obstacle attributes:

- Movement cost.
- Blocks movement: yes/no.
- Cover value.
- Blocks line of sight: yes/no/partial.
- Clear time.
- Required unit skill or supply.
- Salvage chance.
- Noise/contact risk while clearing.

Generation rules:

- Seeded random placement.
- Use clusters and bands, not uniform confetti.
- Protect base spawn zones and initial exits from full blockage.
- Ensure at least several viable corridors across the map.
- Place some obstacles in no man's land to encourage uneven contact and flanking.
- Avoid perfect symmetry; the enemy can have different terrain advantages as long as supply and command can answer them.

Removal rules:

- Sappers and engineers clear fastest.
- Line infantry can clear simple obstacles slowly.
- Clearing consumes time and may consume construction/tool supply.
- Clearing creates noise and may attract scouting/contact response.
- Some obstacles should be convertible into defensive works instead of removed.
- Heavy bombardment later may destroy or worsen obstacles.

Cover rules:

- Cover reduces hit chance and suppression.
- Cover increases ambush/spotting difficulty.
- Cover does not make units immortal.
- Trenches should generally beat ordinary cover, but strong ruins/rock should matter early.

## 8. How supplies from the factory affect behavior and outcome

Factory supplies should not merely add a flat combat bonus. They should change what units can safely attempt and how long they can sustain pressure.

Existing supply categories can map cleanly:

- Ammo: firing effectiveness, suppression output, willingness to attack, defensive staying power.
- Trench materials: dig speed, trench quality, obstacle clearing, base repair, reinforced positions.
- Rations: fatigue recovery, scouting range endurance, morale stability, retreat threshold.
- Medical supplies: wounded recovery, casualty conversion to wounded instead of dead, morale recovery, unit return time.

Factory supply influence:

- Better ammo means units can hold contact longer and win more firefights.
- Better trench materials means the winner of contact consolidates faster.
- Better rations means scouting parties range farther before fatigue/retreat.
- Better medical supply means losses do not permanently hollow out the faction as quickly.
- Balanced supply matters: ammo without rations creates brittle assaults; materials without ammo creates builders who cannot hold; medical without forward success only slows collapse.

The 80/20 rule should be preserved by combat and mission scoring:

- Roughly 80 percent of outcome comes from supply, unit state, cover, command, trench, and position.
- Roughly 20 percent comes from seeded randomness/friction.

Recommended behavior gates:

- Low ammo: units avoid attacks, retreat sooner, fire less effectively.
- Low rations: units fatigue faster, scout less far, morale breaks sooner.
- Low medical: wounded stay out longer, death rate rises.
- Low trench materials: units can win ground but fail to hold it.
- Strong supply: command units authorize larger probes, faster dig-in, more reinforcement, and later bombardment preparation.

Enemy side:

- Phase 1 NPC can use a baseline scripted supply income.
- It should obey the same resolver, but the player faction receives factory-driven variation.
- This makes the player's factory legible without requiring multiplayer or a second factory.

## 9. UI/diagnostics needed for playtesting

The UI should make the agent simulation inspectable from day one.

War map overlays:

- Unit occupancy.
- Fog/scouted/known cells.
- Current contact zones.
- Obstacles and cover.
- Trench strength/network.
- Faction influence/control.
- Supply reach.
- Recent battle markers.
- Pathing/stalled-unit markers for debug mode.

Top bar:

- Player base integrity.
- Enemy base integrity.
- Active contacts.
- Active units per side.
- Supply status: ammo, trench materials, rations, medical.
- Bombardment readiness/progress when unlocked.

Right-hand tracker:

- Current contact reports.
- Recent battle log.
- Pinned sectors.
- Unit losses/wounded.
- Digging/trench progress.
- Obstacles being cleared.
- Units stalled and why.
- Supply shortages affecting behavior.

Cell inspector:

- Coordinates.
- Terrain/obstacle.
- Cover value.
- Trench state.
- Current occupant.
- Last seen enemy.
- Control/influence.
- Movement cost.

Unit inspector:

- Unit type.
- Health/morale/suppression/fatigue.
- Ammo/local supply.
- Current order.
- Current reason string.
- Last contact.
- Assigned command/sector.

Playtest diagnostics:

- Seed value.
- Tick/time.
- Unit count and active units.
- Contacts started/won/lost.
- Trenches created/captured/destroyed.
- Obstacles cleared.
- Supply consumed per minute.
- Combat outcome summaries with deterministic/random contribution.

The current minimalist bottom/top/right UI direction can support this by making overlays bottom-row buttons, base/supply summaries top-bar references, and detailed inspection the right tracker.

## 10. Risks/open questions

Risks:

- Scale risk: 400 x 200 is 80,000 cells. Do not run expensive full-map scans per unit per tick.
- Pathfinding risk: many units need cached, local, or sector-level pathing rather than constant full-grid A*.
- Opaqueness risk: autonomous war will feel unfair unless units and reports explain themselves.
- Boredom risk: slow scouting can feel dead unless visible patrol movement, contact markers, and reports exist.
- Snowball risk: early contact victories can cascade too hard unless retreat, trenches, medics, and regrouping work.
- Random-map risk: obstacles can accidentally create bad starts or fully blocked approaches unless generation validates corridors.
- UI overload risk: showing every unit and stat can become unreadable. Use layers and inspectors.
- Design risk: one unit per square is readable, but too many units will visually clog the map. Start with tens, not thousands.
- Tone risk: dark trench-war tone can become oppressive. The prototype should be grim, not gratuitously unreadable.

Open questions:

- Should initial factions spawn with equal unit counts, or should the enemy start stronger and the player catch up through factory supply?
- Should units represent individual soldiers, fireteams, or abstract squad counters? The user said "1 unit should take up a square"; the report recommends treating each visible unit as a small tactical unit/counter for sanity.
- Should player-built supplies directly spawn units, improve existing units, or both?
- How much direct player influence should exist over war doctrine beyond supply and broad stance?
- Should fog-of-war be strict for both sides, or should the player see enemy movement for playtest readability?
- Should obstacles generate symmetrically enough for fairness or asymmetrically enough for drama?
- How long should a normal battle take at real-time speed before the player can influence it meaningfully from the factory?

## 11. Recommended first implementation slice for the current prototype

Keep this first slice small. The objective is to prove organic contact and trench creation, not finish the whole war.

Recommended first slice:

1. Add a real `WarCell` surface grid for the current 400 x 200 map.
2. Add `WarUnit` records with faction, type, position, health, morale, ammo, current state, and reason string.
3. Create 10 x 10 player and enemy base zones.
4. Spawn a modest number of units per faction above ground inside their bases, such as 20 to 40 units each.
5. Add seeded obstacle generation with base-exit validation.
6. Add a simple scouting state:
   - pick nearby unknown edge cell,
   - move one cell at a time,
   - avoid blocked cells and overcrowding,
   - reveal/scout cells.
7. Add contact detection:
   - spot enemy within short range and line of sight,
   - mark contact zone,
   - pull in nearby units slowly.
8. Add a small local combat resolver:
   - health, morale, ammo, cover, obstacle, supply, and seeded friction,
   - winner/retreat/suppression outcomes,
   - event log.
9. Add dig-in after victory:
   - winning unit starts a foxhole/trench progress value on its cell,
   - trench materials increase speed/quality,
   - render trench cells.
10. Update war UI:
   - draw units, obstacles, contact markers, and trench cells,
   - show selected cell/unit details in the right tracker,
   - keep the top base-health bars.
11. Keep the old strategic front/base integrity summary temporarily as a derived/debug layer until the agent simulation can drive bombardment.

Suggested smoke tests:

- Seeded map generation creates two valid 10 x 10 bases and at least one route between them.
- No two units start on the same cell.
- Units scout unknown cells within N ticks.
- Contact occurs under a known seed within N ticks.
- Combat produces casualties, retreat, or suppression without overlapping units.
- Winning units create at least one trench/foxhole after contact.
- Extra ammo/material/rations/medical improves expected outcomes over repeated seeded test runs.

This slice gives the user the requested direction: real units, real cells, exploration, contact, cover, and trenches. It also leaves bombardment, underground complexity, advanced command units, and full balancing for later, where they may arrive properly dressed rather than tumbling through the window.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-war-agent-simulation-design-report.md`

## Checks run

- Read current project memory and Trenchworks architecture/context.
- No Unity project files were edited.
- No code compile or Unity smoke test was needed for this design-only worker pass.

## Cleanup performed

- No temporary files or generated artifacts were created.

## Memory-worthy notes

- The war should migrate from a single front-progress source of truth to an agent-and-cell model.
- Each faction should use a 10 x 10 base zone on the 400 x 200 map.
- Units should be real occupants: one unit per cell.
- Scouting, contact, fighting, and trench creation should be local and inspectable.
- Obstacles should provide both cover and movement/pathing problems, and should be removable or convertible.
- Factory supplies should affect unit behavior and tactical sustainability, not only raw combat score.

## Anything blocked

Nothing blocked.
