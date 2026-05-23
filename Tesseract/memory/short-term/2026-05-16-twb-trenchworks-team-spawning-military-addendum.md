# 2026-05-16 TWB Trenchworks Team-Spawning Military Addendum

## Scope

Standalone Unity 2D TWB Trenchworks prototype under The World Beneath umbrella.

This is a design-only addendum to `2026-05-16-twb-trenchworks-military-units-fortifications-design-report.md`. No Unity code was implemented. No permanent memory, wiki, index, hot, or log files were edited.

## 1. Directional summary: team-spawning replaces individual-spawning

The military-unit report should be refined so the player does not spawn or manage individual frontline units directly. The player should spawn teams.

New direction:

- Player-facing object: team.
- Simulation-facing object: individual sub-units may still occupy cells, fight, dig, crouch, spot, and die.
- Each team has one leader and at least three sub-units.
- Each team has a tasking family: scouting, fortify/dig-in, assault/no-man's-land, or supply/logistics.
- Each team takes the combined resource cost, upkeep, and carried-supply load of its members and assigned kit.
- The player should assign broad priorities and production support, not click dozens of individual soldiers.

This preserves the one-unit-per-square simulation while making the war playable at scale. A battlefield should not be managed like a dinner seating chart, even if one has standards.

## 2. Team model: leader + sub-units, team inventory, morale, orders, cohesion, casualties

Recommended team record:

- Team id
- Faction
- Tier
- Tasking family
- Team template
- Leader unit type
- Sub-unit list
- Current order
- Target sector or target cell
- Formation shape
- Cohesion radius
- Team morale
- Team suppression
- Team fatigue
- Team inventory
- Casualty state
- Current reason string

Leader:

- Provides command, order quality, morale recovery, and behavior bias.
- If killed or wounded, the team does not instantly vanish. It loses cohesion, responds slower, and may auto-retreat unless a deputy is present.
- Leader type defines team flavor: Patrol Corporal for early teams, Trench Lieutenant for disciplined sector teams, Quartermaster Captain for logistics, Artillery Observer for spotter teams, Choir-Major for late TWB command teams.

Sub-units:

- Occupy individual cells when deployed.
- Retain their unit role: rifleman, scout, sapper, medic, machine-gun crew, signaller, clockwork trenchhand, etc.
- Execute team orders locally: a scout reveals, a sapper digs, a medic treats, a rifleman covers.

Team inventory:

- Ammo carried
- Food/rations carried
- Medical carried
- Construction carried
- Obstacle tools/charges carried
- Command/signal kit carried
- Energy/fuel carried
- Machine/repair kit carried
- Bombardment/shell load if applicable

Team inventory matters because teams should consume supplies while fighting and working. A well-equipped assault team can push; a starving one crouches in a hole and writes a complaint to history.

Morale and cohesion:

- Team morale is shared, with individual modifiers.
- Cohesion measures whether members are close enough and connected enough to act as a team.
- Low cohesion causes slower reactions, poor focus fire, bad scouting, delayed digging, and higher retreat chance.
- Cohesion drops from casualties, suppression, isolation, leader loss, supply shortage, and broken communication.
- Cohesion recovers in trenches, near officers, near command posts, or when supplied.

Orders:

- Scout sector
- Probe contact
- Hold and dig
- Build fortification
- Breach obstacle
- Assault contact
- Man emplacement
- Resupply sector
- Recover wounded
- Retreat/regroup

Casualties:

- Individual sub-units can be healthy, suppressed, wounded, dead, missing, or routed.
- Team remains on the map as long as it has a leader or enough surviving members to function.
- Medical supply converts some dead outcomes into wounded outcomes.
- Manpower and replacement supply can refill depleted teams at base or forward aid/command posts.

## 3. Tiered team progression: how Tier 1/2/3 teams specialize without losing tier clarity

Tier I - Patrol And Scrape Teams:

- Small, cheap, fragile teams with four to five members.
- Focus: scouting, first contact, emergency foxholes, porter supply, basic survival.
- Common leaders: Patrol Corporal, Sapper, Scout.
- Common kits: loose cartridges, basic rations, field dressings, hand tools, sandbags.
- Typical failure: they find trouble faster than they can solve it.

Tier II - Industrial Trench Teams:

- More specialized teams with five to seven members.
- Focus: trench networks, wire, machine guns, mortars, signal posts, trained assault, forward logistics.
- Common leaders: Trench Lieutenant, Quartermaster Captain, Artillery Observer, Field Engineer.
- Common kits: ammo crates, medical crates, trench materials, wire coils, signal kits, shell crates, repair kits.
- Typical failure: they become expensive if the factory cannot keep them supplied.

Tier III - Arcane Siege Teams:

- High-upkeep specialist detachments with four to eight members or mixed human/robotic sub-units.
- Focus: siege prep, aether spotting, command resonance, robotics, pressure weapons, warded shell handling.
- Common leaders: Choir-Major, Bombardment Crew Chief, Grave-Salt Warden, Aether Lamp Scout.
- Common kits: aether batteries, stabilized energy, automata support packs, command relay kits, heavy shells, clearing charges, bombardment cores.
- Typical failure: powerful teams stall or destabilize without energy, command, and warding support.

Tier clarity rule:

- Higher tiers should not make lower tiers obsolete. Tier III teams need Tier I/II teams to scout, hold trenches, carry supplies, and protect emplacements.

## 4. Tasking families and team examples

### Scouting teams

Purpose:

- Probe unknown ground, reveal obstacles, spot enemies, find safe approaches, mark contact zones, and survive long enough to report.

Examples:

- Tier I Listening Patrol
  - Leader: Patrol Corporal.
  - Members: Scout, Scout, Rifleman.
  - Role: early map reveal and cautious contact.
  - Kit: rations, loose ammo, field dressings.

- Tier I Probe Patrol
  - Leader: Scout.
  - Members: Rifleman, Rifleman, Combat Medic.
  - Role: slightly tougher scouting that can survive first contact.
  - Kit: loose ammo, rations, medical.

- Tier II Observer Team
  - Leader: Artillery Observer.
  - Members: Scout, Signaller, Trench Marksman.
  - Role: spot for mortars/field guns and punish exposed head-up enemies.
  - Kit: signal kit, ammo, rations, medical.

- Tier II Counter-Scout Picket
  - Leader: Trench Lieutenant.
  - Members: Trench Marksman, Scout, Rifleman, Signaller.
  - Role: protect friendly trenches from enemy probes.
  - Kit: ammo crates, command, medical.

- Tier III Aether Lantern Section
  - Leader: Aether Lamp Scout.
  - Members: Scout, Echo Runner, Rifleman, Grave-Salt Warden.
  - Role: reveal concealed units, hidden trenches, and dangerous contact pockets.
  - Kit: energy, command, rations, medical, warding.

### Fortify/dig-in teams

Purpose:

- Build foxholes, trenches, wire, bunkers, dugouts, aid posts, command posts, gun pits, relays, and repair damaged defenses.

Examples:

- Tier I Scrape Crew
  - Leader: Sapper.
  - Members: Rifleman, Rifleman, Combat Medic.
  - Role: turn first contact wins into foxholes and shallow cover.
  - Kit: hand tools, sandbags, rations, medical.

- Tier I Emergency Dig-In Team
  - Leader: Patrol Corporal.
  - Members: Sapper, Rifleman, Rifleman.
  - Role: stabilize a dangerous sector after contact.
  - Kit: construction, loose ammo, field dressings.

- Tier II Trench Works Section
  - Leader: Field Engineer.
  - Members: Sapper, Sapper, Rifleman, Signaller.
  - Role: build fire trenches and communication trenches.
  - Kit: trench materials, signal kit, rations, medical.

- Tier II Wire And Bunker Crew
  - Leader: Field Engineer.
  - Members: Wire Cutter, Rifleman, Combat Medic, Machine-Gun Crew.
  - Role: build wire, bunker cells, and MG-ready defensive lanes.
  - Kit: wire coils, concrete/revetment packs, ammo crates, machine support.

- Tier III Clockwork Fortification Detachment
  - Leader: Field Engineer.
  - Members: Clockwork Trenchhand, Clockwork Trenchhand, Grave-Salt Warden, Signaller.
  - Role: build or repair heavy works under pressure.
  - Kit: automata support, repair kits, energy, construction, warding.

### Assault/no-man's-land teams

Purpose:

- Cross exposed ground, breach obstacles, win contact zones, clear trenches, and create openings for follow-up dig-in teams.

Examples:

- Tier I Rifle Push
  - Leader: Patrol Corporal.
  - Members: Rifleman, Rifleman, Sapper.
  - Role: basic attack against weak contact.
  - Kit: loose ammo, rations, field dressings, hand tools.

- Tier II Grenade Breach Team
  - Leader: Trench Lieutenant.
  - Members: Grenadier, Rifleman, Sapper, Combat Medic.
  - Role: clear foxholes, trenches, and obstacle-adjacent defenders.
  - Kit: ammo crates, obstacle ops, medical, rations.

- Tier II Wire Break Assault Team
  - Leader: Trench Lieutenant.
  - Members: Wire Cutter, Grenadier, Bayonet Stormer, Combat Medic, Rifleman.
  - Role: breach wire and take the cell beyond it.
  - Kit: clearing tools, ammo, medical, construction.

- Tier II Suppressed Advance Team
  - Leader: Trench Lieutenant.
  - Members: Bayonet Stormer, Bayonet Stormer, Rifleman, Signaller.
  - Role: advance only when MG/mortar/artillery support is suppressing the target.
  - Kit: ammo crates, command, rations, medical.

- Tier III Pressure Breach Section
  - Leader: Pressure Projector Crew Chief.
  - Members: Pressure Projector Crew, Field Engineer, Rifleman, Combat Medic, Grave-Salt Warden.
  - Role: force defenders out of full cover or bunkers at short range.
  - Kit: energy/fuel, chemical reagent, medical, command, warding.

### Supply/logistics teams

Purpose:

- Move ammo, food, medical, construction, command, energy, shells, and repair goods from base or depots to forward teams.

Examples:

- Tier I Porter Team
  - Leader: Quartermaster Runner or Patrol Corporal.
  - Members: Porter, Porter, Rifleman.
  - Role: carry small loads from base to safe forward cells.
  - Kit: carried goods, rations, light ammo.
  - Note: "Porter" can be a logistics sub-unit type added to the prior roster.

- Tier I Stretcher And Aid Team
  - Leader: Combat Medic.
  - Members: Stretcher Bearer, Stretcher Bearer, Rifleman.
  - Role: carry medical supply forward and bring wounded back.
  - Kit: medical, rations, field dressings.
  - Note: Stretcher Bearer can be a logistics sub-unit type.

- Tier II Forward Quartermaster Team
  - Leader: Quartermaster Captain.
  - Members: Signaller, Rifleman, Rifleman, Porter.
  - Role: create local supply handoff near trenches.
  - Kit: ammo crates, ration crates, medical crates, command/signal.

- Tier II Shell Runner Team
  - Leader: Signaller.
  - Members: Rifleman, Porter, Porter, Combat Medic.
  - Role: move mortar/field-gun shells to emplacements.
  - Kit: shell crates, rations, medical.

- Tier III Clockwork Hauler Team
  - Leader: Quartermaster Captain.
  - Members: Clockwork Trenchhand, Clockwork Trenchhand, Rifleman, Grave-Salt Warden.
  - Role: heavy forward supply under fire.
  - Kit: energy, repair kits, carried goods, warding.

- Tier III Warded Siege Supply Team
  - Leader: Bound Shell Cantor.
  - Members: Porter, Signaller, Grave-Salt Warden, Rifleman, Clockwork Trenchhand.
  - Role: move volatile siege goods to bombardment positions.
  - Kit: bombardment, energy, command, warding, repair.

## 5. How team composition maps to individual unit types from the prior report

The prior 25-unit roster remains useful as the sub-unit catalog.

Mapping rules:

- Officer unit types usually become team leaders.
- Normal soldiers become combat sub-units.
- Engineers/support become task specialists.
- Heavy/emplacement crews are sub-units that require a built or buildable emplacement.
- TWB twist units are late-tier specialists that add a specific behavior and upkeep burden.
- New logistics sub-units can be added: Porter, Stretcher Bearer, Shell Runner. These should be simple, low-combat units tied to the supply team family.

Examples:

- Listening Patrol = Patrol Corporal + Scout + Scout + Rifleman.
- Scrape Crew = Sapper + Rifleman + Rifleman + Combat Medic.
- Grenade Breach Team = Trench Lieutenant + Grenadier + Rifleman + Sapper + Combat Medic.
- Trench Works Section = Field Engineer + Sapper + Sapper + Rifleman + Signaller.
- Observer Team = Artillery Observer + Scout + Signaller + Trench Marksman.
- Clockwork Fortification Detachment = Field Engineer + Clockwork Trenchhand + Clockwork Trenchhand + Grave-Salt Warden + Signaller.

Important rule:

- The player should see the team card first and the member list second. Individual members matter for diagnostics and combat, but they should not become the primary interface.

## 6. Aggregate resource costs and upkeep from the production system

Team cost should be computed from:

```text
Team Cost =
  Leader Unit Cost
  + Sum(Sub-Unit Costs)
  + Tasking Kit Cost
  + Initial Carried Inventory
  + Tier Unlock/Training Cost if applicable
```

Team upkeep should be computed from:

```text
Team Upkeep =
  Human Food/Morale drain
  + Ammo use from firing
  + Medical use from casualties
  + Construction use from building/repair
  + Command use from orders/coordination
  + Energy/repair use from TWB and robotic units
  + Shell/bombardment use from heavy weapons
```

Cost categories:

- Manpower/Bodies: every human member.
- Food/Morale: every human member, extra for scouts and assault teams.
- Ammo: riflemen, scouts, marksmen, grenadiers, MG crews, assault teams.
- Construction: sappers, engineers, fortification teams, emplacements.
- Medical: all teams benefit; assault and scouting need more.
- Command/Communication: leaders, officers, signallers, observers, coordinated assaults.
- Obstacle Operations: wire cutters, sappers, grenadiers, breach teams.
- Machine/Robotics Support: MGs, field guns, clockwork units, loader stations.
- Energy/Fuel: aether teams, pressure projectors, robotics, relays, siege support.
- Bombardment: field guns, siege teams, shell cantors, base-breach teams.

Tier pressure:

- Tier I teams are cheap enough to deploy often, but weak without supplies.
- Tier II teams are tactically decisive but punish poor factory allocation.
- Tier III teams should be rare, expensive, and powerful in narrow roles.

Design warning:

- Avoid exact numeric costs until the first implementation is measurable. Use relative costs, then tune by playtest.

## 7. Supply team behavior and front-line resupply rules

Supply teams should be real entities, not invisible bonuses.

Basic behavior:

1. Spawn at base or supply depot.
2. Load inventory according to assigned supply mission.
3. Pick a route through known/scouted/controlled cells.
4. Prefer trenches, communication trenches, cover, and friendly-controlled lanes.
5. Avoid known contact zones unless marked as emergency supply.
6. Deliver supplies to teams, caches, emplacements, aid posts, or command posts.
7. Return, reroute, or hold depending on danger and inventory.

Frontline consumption:

- Teams carry local supplies and consume them as they act.
- Rifle fire consumes ammo.
- MG fire consumes ammo faster.
- Mortar/field-gun fire consumes shell supply.
- Digging consumes construction.
- Treating casualties consumes medical.
- Long scouting consumes food.
- Command pulses and coordinated assaults consume command.
- Robotics and aether systems consume energy and repair/warding goods.

Resupply rules:

- A frontline team requests supplies when any inventory category falls below its task threshold.
- Supply teams prioritize urgent shortages unless ordered otherwise.
- A forward cache can hold supplies near trenches, but risks capture or explosion.
- Aid posts pull medical and food.
- Emplacements pull ammo/shells/machine support.
- Command posts pull command/signal goods.
- A supply team under fire may drop cargo, retreat, crouch, or call for cover.

Good diagnostic examples:

- "Assault Team 3 stalled: ammo empty, medical low."
- "Porter Team 2 rerouting: contact zone ahead."
- "MG Nest supplied: 18 ammo ticks delivered."
- "Trench Works Section paused: construction not delivered."
- "Warded Siege Supply Team waiting: energy crate missing."

## 8. How teams deploy onto the current one-unit-per-square simulation grid

The current grid rule can remain: one sub-unit occupies one square.

Deployment rules:

- When a team spawns, each member gets an individual `WarUnit` record.
- The team owns those unit ids.
- Members spawn in a formation near the base, depot, or deployment point.
- The leader chooses the team target and path preference.
- Members move as a loose group, not as one stacked counter.
- The team has a cohesion radius. Members outside it are stragglers and get worse morale/order response.
- If the target area has insufficient empty cells, the team queues, stretches, or picks a nearby staging cell.

Formation examples:

- Patrol line: scouts forward, rifleman behind, leader central.
- Dig crew: sapper/engineer forward, riflemen covering flanks, medic behind.
- Assault wedge: assault units forward, sapper/breach unit central, medic behind.
- Supply column: leader front, carriers middle, rifleman rear/escort.
- Emplacement crew: builder and crew occupy adjacent cells around the emplacement socket.

Player-facing map display:

- At normal zoom, show the team icon/card marker at its centroid or leader.
- At close zoom, show individual member pips in their cells.
- Clicking a team selects the whole team; a second inspect layer can show members.

Simulation-facing behavior:

- Individual combat still resolves per cell.
- Team order biases individual state machines.
- Casualties and suppression update both individual state and team aggregate state.
- If a team is reduced below a minimum functioning size, it becomes depleted and retreats or waits for replacement.

## 9. UI/diagnostics changes for spawning and tracking teams

Spawn UI:

- Bottom row should show team tasking buttons rather than individual unit buttons.
- Suggested tasking buttons: Scout, Dig, Assault, Supply.
- Add tier filter: T1, T2, T3.
- Team card shows: leader, member icons, cost, carried inventory, task, estimated upkeep, current unlock requirements.
- Spawn queue shows teams training/loading, not individual bodies.

War map UI:

- Team icon on map with task color and small status ring.
- Optional close-zoom member pips.
- Supply route overlay for logistics teams.
- Build-job overlay for fortify teams.
- Contact/spotting overlay for scouting teams.
- Breach/assault overlay for assault teams.

Right tracker:

- Pinned teams.
- Team inventory bars: ammo, food, medical, construction, command, energy.
- Team morale/cohesion/suppression.
- Casualty list by healthy/wounded/dead/missing.
- Current order and reason string.
- Member list collapsed by default.

Top bar:

- Active teams by family.
- Depleted teams.
- Supply teams en route.
- Current most painful shortage.
- Bombardment readiness once siege teams exist.

Useful diagnostic strings:

- "Listening Patrol: probing unknown cells, avoiding contact."
- "Scrape Crew: building foxholes, construction 42 percent."
- "Grenade Breach Team: waiting for MG suppression."
- "Porter Team: delivering ammo and medical to Contact Zone C."
- "Clockwork Hauler: stalled, repair kits exhausted."

## 10. Balance risks and open questions

Risks:

- Team abstraction can hide important sub-unit behavior if the inspector is too shallow.
- Too many team templates can become as messy as too many individual units.
- Supply teams can become tedious if every crate needs manual orders.
- Supply teams can become meaningless if they teleport goods or ignore danger.
- Team costs can feel unfair if aggregate resource requirements are not explained.
- Leader death can be either too punishing or too invisible.
- Large teams can clog the one-unit-per-square grid.
- Small teams can evaporate too fast under MG/artillery rules.
- Tier III teams can become "magic solves everything" unless energy, repair, command, and warding costs remain sharp.

Open questions:

- Should teams be player-designed from unit slots, or chosen from fixed templates first? Recommendation: fixed templates first.
- How large should teams be? Recommendation: start with four-member teams for Tier I, five to six for Tier II, and four to eight for Tier III specialist detachments.
- Should teams auto-request supply or require player-prioritized logistics? Recommendation: auto-request by default, with player priority overrides.
- Should depleted teams be refilled in place or only at base/aid posts? Recommendation: base first; forward refit later.
- Should enemy teams use the same abstraction? Recommendation: yes internally, but with simpler NPC spawn/supply rules during phase 1.

## 11. Recommended first implementation slice

Goal: prove team spawning, group movement, aggregate cost, and supply consumption without implementing the full roster.

Recommended first team templates:

- Scout Patrol
  - Patrol Corporal + Scout + Scout + Rifleman.
  - Task: reveal and avoid/survive first contact.

- Dig-In Crew
  - Sapper + Rifleman + Rifleman + Combat Medic.
  - Task: build scrapes/foxholes after contact.

- Assault Section
  - Patrol Corporal + Rifleman + Rifleman + Sapper.
  - Task: attack weak contact and breach simple obstacles.

- Porter Team
  - Quartermaster Runner or Patrol Corporal + Porter + Porter + Rifleman.
  - Task: move ammo/food/medical/construction from base to forward teams.

Recommended mechanics:

- Add a team wrapper that owns existing `WarUnit` ids.
- Spawn teams from the base instead of spawning individual unit types from UI.
- Give each team a small inventory of ammo, food, medical, and construction.
- Let teams consume inventory while fighting, scouting, digging, or treating casualties.
- Add team cohesion and aggregate morale.
- Render team icons at normal zoom and member pips at close zoom.
- Add right-panel team inspector.
- Keep the current one-unit-per-square rule.
- Do not add Tier III, heavy emplacements, or custom team design until this works.

First pass success criteria:

- The player spawns a Scout Patrol, Dig-In Crew, Assault Section, and Porter Team from clear UI buttons.
- Each team deploys as multiple sub-units occupying separate cells.
- The player can click a team and see leader, members, inventory, morale, cohesion, order, and reason.
- Porter Team delivery changes another team's ability to fight/dig/treat.
- The war remains readable at scale because the player tracks teams first and individuals second.

## Context sources read

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-military-units-fortifications-design-report.md`

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-team-spawning-military-addendum.md`

## Checks run

- Read required project memory context.
- Read the base military units and fortifications design report.
- Confirmed this pass is design-only and did not edit Unity source or permanent memory.

## Cleanup performed

No temporary files, screenshots, throwaway logs, or generated dev artifacts were created.

## Memory-worthy notes

- Player-facing war spawning should use teams rather than individual units.
- Teams have leaders, sub-units, inventory, morale, cohesion, orders, and casualties.
- Individual units can still exist inside the simulation for occupancy and combat.
- Supply teams should be real map actors that carry and deliver consumable supplies.
- The first implementation should prove four team families before adding advanced units.

## Anything blocked

Nothing blocked.
