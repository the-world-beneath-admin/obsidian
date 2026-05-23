# TWB Trenchworks War AI Frontline Report And GPT Pro Brief

Date: 2026-05-16
Worker: Bob / Trenchworks playtest stabilization
Scope: TWB Trenchworks standalone Unity 2D prototype

## Purpose

This report summarizes the war section of TWB Trenchworks, what the AI is supposed to become, what has been attempted so far, what is currently split or fragile, and what GPT Pro should be asked to research and analyze next.

I cannot directly contact GPT Pro from this Codex window. The final section is therefore a ready-to-paste GPT Pro research prompt/package.

## Core War Fantasy

The player should not micro individual soldiers. The player builds and manages the factory/logistics side that feeds one faction's war machine. The war side should feel like an autonomous, grim, slow WW1-style front that emerges from contact, supply, terrain, and entrenchment.

Desired battlefield shape:

- player-supported force enters from the left side
- enemy force enters from the right side
- top, middle, and bottom entry lanes exist for both sides
- no man's land sits between both sides
- squads scout forward under uncertainty
- contact happens organically, not because two blobs are ordered to collide
- once contact creates a clear edge, units dig in instead of always pushing
- foxholes and local fighting positions grow into trench segments
- trench segments connect into lines
- communication/supply trenches connect fighting positions back to base/entry areas
- fortified trench slots support machine guns, mortars, artillery observers, aid posts, dugouts, ammo dumps, and eventually bombardment
- victory path remains eventual enemy-base bombardment and destruction

Locked design principle: outcomes should be roughly 80 percent supply-driven and 20 percent seeded-random variance.

## Current Project Reality

Live project:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

Primary visible war implementation:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`

Newer team/squad AI layer:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamSlice.cs`

The largest architectural issue is that there are currently two war-behavior layers:

1. `WarWorld` in `TrenchworksSimulation.cs`
   - visible Play Mode wave drill
   - per-unit positions, combat, trenches, terrain, wave spawns, bullets, status UI
   - many iterative fixes live here because this is what the user can see

2. `WarTeamSlice` in `Assets\Scripts\Simulation\War`
   - cleaner team-level AI model
   - leader + sub-units
   - candidate scoring, contact heat, supply, trench plans, diagnostics
   - not yet fully authoritative for the visible battlefield

This split explains the repeated "looks like blobs / stalls / not organic" problem. The smarter team brain exists, but the visible loop still has a legacy per-unit brain doing much of the action.

## What The War System Has Now

### Map And Scale

Current code state:

- `WarWorld.MapWidth = 800`
- `WarWorld.MapHeight = 600`
- `BaseSize = 10`
- three entry zones: top, middle, bottom
- player base/entry side on left
- enemy base/entry side on right
- war max zoom now targets `64px` per tile
- ordinary soldiers render as 2x2 visual tile footprints
- command/lieutenant units render as 2 wide x 4 tall visual tile footprints

This scale choice is for future sprite/art readability. It is currently a visual contract, not full collision/occupancy scale.

### Units And Squads

The visible `WarWorld` unit types:

- Rifle
- Sapper
- Engineer
- Medic
- Command

Visible unit state:

- Scouting
- Fighting
- DiggingIn
- ClearingObstacle
- SeekingCommand
- Recycling
- Retreating
- Holding
- Dead

The visible per-unit loop now tracks:

- squad id
- leader id
- formation index
- facing direction
- last move direction
- pending movement delay
- cover target
- commander missing timer
- active/static simulation status

The newer `WarTeamSlice` team templates are closer to the intended design:

- Scout Patrol: leader plus scouts/rifleman
- Assault Section: leader plus riflemen/sapper
- Fortify Engineer Crew: field engineer plus sapper/rifleman/medic
- Supply Team: quartermaster runner plus porters/rifleman

Each team has supplies:

- ammo
- food
- medical
- construction

Each team has behavior weights:

- cohesion radius
- caution
- aggression
- engineering

This is closer to the user's later direction: players should spawn teams, not individual soldiers.

### Terrain, Cover, Concealment, And Obstacles

War map cells include:

- obstacles
- obstacle integrity
- cover tier
- concealment tier
- movement tier
- trench owner/progress
- trench connector masks
- trench role
- fortification slot

Obstacle/terrain examples:

- rubble
- wire
- craters
- ruins
- mud
- shell craters
- berms/banks
- drainage gullies
- stones/boulders
- tall grass/reeds/woods

Cover/concealment distinction:

- cover reduces bullet damage
- concealment reduces spotting
- movement tier slows units in mud, craters, woods, etc.

Fog of war was attempted, then disliked, then disabled. The code still has fog-shaped infrastructure, but current render hiding returns false so the battlefield is visible.

### Spawning And Wave Drill

The visible test sequence currently uses a wave drill:

- clears units
- sends squad pulses from top/middle/bottom lanes
- initial burst pulses happen every 15 seconds
- then a 30-second loop cadence
- alive unit cap avoids infinite growth

This was created so the user could watch repeated waves and diagnose whether units scout, fight, and dig in.

### Movement And Scouting Attempts

Attempts so far:

- moved away from straight-line center charging
- added stable noise to movement
- added lane pull
- added cover-seeking targets
- added forward-but-not-straight scoring
- added movement delays from terrain
- added squad cohesion
- pinned members within a leader radius
- added commander replacement/recycling behavior if command dies
- command unit visual footprint increased
- added support response to heard contacts

Remaining problem:

The visible per-unit loop still makes local adjacent-cell decisions. It can look jittery, linear, or too static depending on weights. It lacks a unified operational objective like "secure this no-man's-land sector, then consolidate and connect it."

### Combat Attempts

Combat currently includes:

- ranged engagement through `WeaponRange`
- local combat resolution when enemies are in range
- combat power considers unit type, morale, health, ammo, cover, supply
- global outcome still uses supply/random weighting
- bullets/tracers render between active contacts
- contact cells are marked with age and contact winner
- active fight can reveal/contact-highlight both participants
- support units can respond within hearing range

Important correction already made:

Units should not need to touch before fighting. They now engage at range and use standoff/cover behavior.

Desired but incomplete:

- suppression/pinning
- fire arcs
- directional cover
- enfilade/flanking
- machine-gun area denial
- indirect fire
- morale shock that causes retreat/regroup without direct player micromanagement

### Digging And Trench Growth Attempts

The user clarified:

The "winner" of contact should not keep pushing. Once a unit gets a clear edge, it should start digging in. Once trenches are dug, the unit should stay and defend rather than push forward endlessly.

Implemented attempts:

- `ClearCombatEdge` threshold
- winning/advantaged units can call `TryDigCombatCover`
- engineers/sappers nearby can support digging
- units in `DiggingIn` call `DigCurrentCell`
- completed friendly trenches cause holding
- quiet-front recovery allows leaders to probe after all contact stops

Trench readability passes:

- trenches no longer meant to be giant blobs
- added trench pieces
- added connector endpoints
- added visible facing/bullets
- added trench depth colors
- recent pass added trench roles and fortification slots
- recent pass changed first fire-line seed to north/south
- recent pass made front/fire-line trenches 4 tiles wide and communication/traverse/diagonal pieces 3 tiles wide

Current trench pattern model:

- roles: fire line, communication, traverse, sap, emplacement
- slots: rifle step, machine-gun nest, mortar pit, artillery pocket, dugout, ammo dump, aid post, observation post, listening post
- kinds: straight, crook, zig-zag, tee, diagonal, traverse

Remaining problem:

The trench growth is still reactive and unit-driven. It is not yet a validated network generator that guarantees:

- no long straight kill corridors
- communication trenches back to base
- support/reserve trench bands
- no man's land stays meaningfully contested
- machine-gun/mortar slots have useful arcs

### Performance Attempts

The war map originally grew very large and slowed badly. Work attempted:

- map length reduced from the larger requested size
- visual LOD added
- squads aggregate into leader/count markers at far zoom
- fog/static optimization attempted, then fog visuals removed
- active/passive simulation ideas explored
- still not final

Current recommendation:

Do not pursue visual fog as the main optimization if the user dislikes it. Instead:

- decouple simulation resolution from rendering
- aggregate inactive/far units into team snapshots
- simulate individual soldiers only around active contact/observed/focal areas
- maintain trench/contact/supply fields as lower-resolution maps
- render grid lines sparsely at far zoom

## What We Have Attempted So Far, Chronologically

1. Basic Milestone 1 strategic war
   - factory supplies fed readiness/front progress/bombardment
   - abstract front progress could reach enemy-base destruction
   - this proved the supply-to-war loop but not organic combat

2. Unity entry-point stabilization
   - fixed project path and scene confusion
   - canonical live path became `TWB-TrenchWorks`

3. Larger war map and UI
   - added pan/zoom, bottom controls, right unit summary, top progress bars
   - added top/mid/bottom entry zones

4. Wave drill test mode
   - repeated squad pulses from each lane
   - built to watch AI behaviour without factory resource gating

5. Terrain/cover/concealment pass
   - random map props
   - cover and concealment distinction
   - slow terrain

6. Scouting and squad cohesion passes
   - forward-biased but noisy scouting
   - leaders and followers
   - 15-cell cohesion target in visible loop
   - missing commander replacement/recycling

7. Combat range and dig-in correction
   - ranged combat rather than melee collision
   - clear edge causes dig-in
   - engineers/sappers support trenching

8. Hearing/contact support
   - nearby units can respond to active fight noise
   - active combat reveals/highlights both sides

9. Fog and optimization experiments
   - fog added, then removed from visible render because user disliked look
   - visual LOD remains important

10. Battle stall recovery
   - completed trenches made units stop forever
   - added quiet-front probing after no-contact periods

11. Trench readability/depth/piece passes
   - trenches made more visible
   - added piece kinds, connector rules, bullet tracers, facing indicators

12. War tile scale pass
   - max zoom 64 px/tile
   - soldier visual footprint 2x2
   - command visual footprint 2x4

13. Trench pattern grammar pass
   - north/south fire-line bias
   - east/west communication connector possibility
   - 3-4 tile widths
   - fortification slot metadata

14. Newer team AI layer
   - `WarTeamSlice` adds leader decisions, team templates, blackboard, candidate scoring, contacts, trench plans, supply consumption
   - currently not fully authoritative for the visible battlefield

## Current AI Design Direction

The best direction is a hybrid:

1. Strategic layer
   - tracks front pressure, supply stock, bombardment readiness, base integrity
   - decides broad war tempo and enemy pressure

2. Operational team layer
   - squad leaders select objectives
   - objectives are scout, attack, dig in, resupply, connect trenches, hold, regroup
   - uses contact heat, supply state, trench value, cover, route risk, friendly support

3. Tactical local layer
   - individual soldiers maintain formation, fire, crouch, retreat, build, heal, carry supplies
   - individual decisions should obey the squad leader's current objective

4. Field maps / influence maps
   - contact heat map
   - danger/firepower map
   - cover/concealment map
   - trench value map
   - supply reach map
   - noise/hearing map
   - route-risk map

This matches the genre research direction: RTS AI is usually managed with abstractions, influence maps, and hierarchy rather than every unit making a fully independent genius decision.

## Lessons From External Genre Research

Preliminary source scan:

- RTS AI research emphasizes abstraction because full real-time state spaces are too large; good systems combine high-level choices with local tactical detail. See Barriga, Stanescu, and Buro's AIIDE paper on combining strategic learning with tactical search.
- Influence maps are especially relevant because Trenchworks is grid-based and spatial. Forgette/Smolikova-Wachowiak/Wachowiak describe influence maps for tactical engagement decisions, including prior-event memory such as casualties.
- StarCraft micro research often uses influence-map or potential-field representations to compress unit distributions and make real-time decisions feasible.
- Company of Heroes is a useful design reference for cover, suppression, flanking, and weapon arcs. Its manual states that cover affects suppression vulnerability, suppression slows movement and reduces accuracy, pinned squads cannot move or attack, and flanking can nullify directional cover or avoid weapon arcs.
- A GameDeveloper analysis of Company of Heroes highlights why directional cover and limited firing arcs create tactical geometry rather than mere stat trades.
- Behavior trees remain useful as readable hierarchy, but research on behavior trees notes FSMs scale poorly as complexity grows. Trenchworks should avoid a giant flat FSM.

Sources:

- [Combining Strategic Learning with Tactical Search in RTS Games](https://ojs.aaai.org/index.php/AIIDE/article/view/12922)
- [Influence Maps for Facilitating Tactical Decisions in RTS Games](https://www.sharcnet.ca/my/publications/show/2188)
- [Company of Heroes 2 Manual](https://www.feralinteractive.com/en/manuals/companyofheroes2/latest/steam/)
- [On Company of Heroes](https://www.gamedeveloper.com/design/on-company-of-heroes)
- [A Survey of Real-Time Strategy Game AI Research and Competition in StarCraft](https://experts.mcmaster.ca/scholarly-works/1941878)
- [A Survey of Behavior Trees in Robotics and AI](https://arxiv.org/abs/2005.05842)
- [Playing RTS games by imitating human micromanagement skills based on spatial analysis](https://cilab.gist.ac.kr/hp/wp-content/uploads/2018/12/7.-Playing-real-time-strategy-games-by.pdf)

## Key Diagnosis

The desired loop is not yet complete because the project is caught between:

- a visible per-unit simulation that has been patched repeatedly to react to playtest problems
- a better team/squad AI design that exists as a cleaner slice but does not yet fully own the visible war

The next milestone should not add more units, more props, or more UI until this is corrected.

## Recommended Completion Loop

Target loop:

1. Spawn teams from top/mid/bottom lanes.
2. Team leader receives broad order: scout, assault, fortify, supply, connect.
3. Leader samples field maps:
   - visible/known contacts
   - heard contact heat
   - cover/concealment
   - trench value
   - supply reach
   - route risk
4. Team moves as a cohesive group toward a candidate objective.
5. When suspected contact is near:
   - scouts slow/crouch/observe
   - assault team seeks covered firing line
   - engineers hang back unless fortification is viable
   - supply teams avoid direct contact
6. When confirmed contact happens:
   - both teams enter fire exchange at range
   - suppression/pinning starts accumulating
   - cover direction matters
   - MG arcs and artillery/mortar risk shape movement
7. If neither side gains an edge:
   - both hold, reposition, or call support
   - no one blindly charges
8. If one side gains a clear edge:
   - advantaged team digs in
   - engineers nearby accelerate trench work
   - fight becomes a held contact
9. Held contact becomes trench seed:
   - foxhole/scrape
   - fire trench
   - traverse/zig-zag
   - slot created for rifle/MG/mortar/aid/dugout
10. Trench network connects:
   - nearby trenches link laterally
   - communication trench links back to base/supply lane
   - supply reach improves
11. No man's land emerges:
   - area between opposing trench networks remains dangerous
   - scouts and assault teams probe gaps
   - artillery/mortar/MG slots punish exposed movement
12. Strategic layer reads aggregate front state:
   - held sectors
   - supply flow
   - casualties
   - trench depth
   - bombardment readiness
13. Victory path:
   - player supplies enough ammo/construction/food/medical/special resources
   - observers/emplacements/supply corridors unlock bombardment
   - enemy base integrity eventually reaches zero

## Recommended Next Implementation Milestones

### Milestone A: Make `WarTeamSlice` authoritative for visible movement

Do this before more content.

- visible `WarWorld` units should be members of teams or derived from team snapshots
- team decision should choose objective
- per-unit visible movement should execute that objective
- remove or downgrade independent per-unit scouting decisions
- every visible unit should be explainable by current team order/reason

Success test:

- click unit summary and see team/order/reason
- squads no longer behave like independent random dots
- changing team kind changes behavior visibly

### Milestone B: Add influence/contact maps as explicit data

Add maps updated once per strategic second or tactical substep:

- contact heat
- danger/firepower
- friendly support
- cover quality
- trench value
- supply reach
- no man's land pressure

Use low-resolution overlays if necessary. Do not simulate magic; just provide better shared senses.

Success test:

- debug overlay can show why a squad chose a cell
- no more mysterious stalls
- cover-to-cover movement becomes a consequence of map scoring

### Milestone C: Make combat produce states, not only damage

Add:

- suppression
- pinned
- retreat/regroup
- confidence/combat edge
- fire superiority

Combat should have outcomes:

- hold
- dig
- retreat
- call support
- attempt flank
- assault only if conditions are favorable

Success test:

- two equal squads in cover mostly hold
- squad caught in open gets pinned/retreats
- engineer near a held fight digs
- supply-depleted squad requests supply or pulls back

### Milestone D: Make trenches a network product

Keep current trench piece/slot work, but add validation:

- trench piece belongs to a network id
- network has owner, role, supply connection, depth
- fire trenches trend north/south
- communication trenches trend east/west
- connectors must remain reachable
- no disconnected random strips

Success test:

- after 5 minutes, map shows multiple organic trench clusters
- some clusters connect back to base
- unsupported advanced trenches become brittle

### Milestone E: Add first emplacement behavior

Do not add all equipment at once.

Start with:

- machine-gun slot
- mortar slot
- aid/dugout slot

These can be simple modifiers before they become buildable equipment.

Success test:

- MG slots create directional suppression/area denial
- mortar slots pressure static trenches
- aid/dugout slots reduce attrition and stabilize held positions

## Pushback / Design Warning

Do not make every unit too clever. The war should feel organic at the team/front level, not like 300 individual soldiers are each writing their memoirs before moving one tile.

The player needs readable causality:

- "these scouts found contact"
- "this assault section got pinned in open ground"
- "engineers dug in because they had a combat edge"
- "this trench failed because supply never connected"
- "this MG nest locked down the gap"

If we cannot explain the action in one sentence, the AI is not better; it is merely more expensive.

## GPT Pro Research Prompt / Handoff Package

Paste the following into GPT Pro:

```text
You are advising on the war AI design for TWB Trenchworks, a standalone Unity 2D grid-based factory/logistics + automated trench-war prototype under The World Beneath umbrella.

The player does NOT micro individual soldiers. The player builds the factory/logistics side that supplies one faction. The war side should run autonomously and visibly. The goal is an organic WW1-inspired front: two factions enter from opposite sides, no man's land emerges in the center, contact creates firefights, squads that gain a clear edge dig in, foxholes/trenches connect into networks, and supply trenches run back to base. Victory eventually comes from supply-enabled bombardment and enemy base destruction.

Locked decisions:
- Phase 1 is player vs NPC.
- Player supplies one faction.
- Multiplayer/shared accounts/pets are not phase 1.
- Tone is dark.
- Victory is total annihilation through enemy-base bombardment.
- Outcomes should be roughly 80% supply-driven and 20% seeded-random variance.
- The game should use old-school debuggable game AI, not black-box LLM AI.
- The map is a 2D grid; current war map is roughly 800x600.
- Unit art scale target is 64 px/tile at max zoom, base soldier 2x2 tiles, command/lieutenant 2x4 tiles.

Current implementation summary:
- Unity 2D, simulation-first C#.
- Current visible war loop is `WarWorld` in `TrenchworksSimulation.cs`.
- There is a newer `WarTeamSlice` with team templates and squad-leader decisions, but it is not yet fully authoritative over the visible battlefield.
- Visible units currently include Rifle, Sapper, Engineer, Medic, Command.
- Unit states include Scouting, Fighting, DiggingIn, ClearingObstacle, SeekingCommand, Recycling, Retreating, Holding, Dead.
- Team types in the newer slice include Scout Patrol, Assault Section, Fortify Engineer Crew, Supply Team.
- Teams have ammo, food, medical, construction supplies.
- Current AI attempts include cover-seeking, stable random scouting, squad cohesion, commander replacement/recycling, ranged combat, combat-edge dig-in, hearing-distance support, terrain cover/concealment, slow terrain, trench piece grammar, and wave drill spawning from top/mid/bottom lanes.
- Fog of war was attempted and removed visually because the user disliked it.
- Visual LOD and squad aggregation exist.
- Current trench model has roles: fire line, communication, traverse, sap, emplacement.
- Current trench slots include rifle step, machine-gun nest, mortar pit, artillery pocket, dugout, ammo dump, aid post, observation post, listening post.
- Current problem: the visible war loop can still look like blobs, can stall after initial contact, and does not yet consistently grow a readable no man's land / trench network from contact.

Research task:
Please do your own research across strategy/RTS/tactics games and game AI practice. Focus on RTS and tactical squad games, not FPS AI. Useful comparison areas include Company of Heroes, Men of War / Gates of Hell, Total War, RimWorld-style combat AI if relevant, AI War-style abstraction if relevant, StarCraft/microRTS research, influence maps, utility AI, behavior trees, hierarchical AI, squad AI, cover systems, suppression, front-line emergence, and performance/LOD approaches.

Deliver:
1. A high-level diagnosis of the current design problem.
2. The best AI architecture for this war loop.
3. How to structure squad/team decision-making.
4. How to make no man's land emerge rather than be scripted.
5. How contact should transition into firefight, dig-in, trench network, and supply line.
6. What maps/fields/influence layers should exist.
7. How to make units feel organic without making them individually expensive.
8. How to prevent blobs and stalls.
9. How to model suppression, cover, flanking, MG arcs, artillery/mortar pressure, and trench safety at prototype level.
10. How to handle performance for hundreds of units on a large grid.
11. What to implement next in 5-8 concrete milestones.
12. What NOT to implement yet.

Please return implementation guidance suitable for a Unity C# simulation-first prototype. Favor debuggable deterministic systems, clear data structures, and visible diagnostics. Avoid recommending black-box ML/LLM runtime AI for phase 1.
```

## Final Recommendation

The next code milestone should be called something like:

`War Team Authority And Frontline Field Maps`

It should:

1. make team orders drive visible units
2. add shared influence/contact maps
3. make combat produce suppression/hold/dig/retreat decisions
4. make trench networks persistent and connected
5. expose the AI reasons in the right-hand unit summary

That is the shortest path from "units doing stuff" to "a believable front line organically growing around no man's land."

## Memory-Worthy Notes

- Current war AI split is the main risk: `WarWorld` is visible; `WarTeamSlice` is conceptually cleaner.
- Trenchworks needs hierarchical squad AI plus influence maps, not pure individual-unit local decisions.
- Organic front-line growth should be a contact-to-entrenchment-to-network loop, not a moving front percentage or a line painter.
- Suppression, directional cover, and emplacement arcs are likely the missing tactical glue.
- The first complete loop should be one scout team, one assault team, one engineer team, and one supply team interacting around one contact area before scaling up.

## Follow-Up Recommendations

- Ask GPT Pro with the prompt above and save its response as a raw/intake source before promoting decisions.
- After GPT Pro returns guidance, convert it into a narrow implementation plan instead of immediately adding content.
- The next implementation pass should retire or subordinate legacy per-unit AI decisions to the team-order layer.

## Anything Blocked

- Directly asking GPT Pro is blocked in this Codex window because no GPT Pro tool/connector is available.
- Report and GPT Pro prompt are complete and ready for user/Bob/orchestrator handoff.
