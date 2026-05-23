# TWB Trenchworks Architecture

## Status

Milestone 1 plus Phase 1 staged front-establishment, project-specific asset catalog, runtime-wired war art, and controlled war-side proof gate - updated after the 2026-05-23 runtime wiring and readiness reports.

## Core Recommendation

Build TWB Trenchworks as a simulation-first Unity 2D game with two linked simulation domains:

- factory/logistics grid
- automated trench-war grid

The simulation should be plain C# data and systems. Unity should handle rendering, input, UI, audio, animation, and editor tooling around that simulation.

## Engine Direction

- Use Unity 2D.
- Use a hybrid grid approach:
  - Tilemaps for static terrain, factory floor, resource-node markings, trench/terrain visualization, underground visualization, and ownership overlays.
  - Custom grid data for occupancy, machines, belts, inventories, units, missions, trenches, tunnels, control, and save state.
  - Pooled custom renderers for dynamic belts, moving items, machines, units, mission arrows, and overlays.
- Do not use Tilemap or GameObjects as the source of truth for simulation state.

## Data Direction

Use data-driven definitions for:

- items
- recipes
- machines
- belts
- inserters
- supply categories
- unit types
- command-unit types
- mission types
- terrain and trench types
- factions

ScriptableObjects are suitable authoring assets, but runtime state should use immutable catalog records and serializable plain C# save data.

## Tick Model

Use a fixed-step simulation with seeded randomness:

- factory tick for belts, inserters, machines, and shipping
- war tactical tick for unit movement and local combat
- war strategic/mission tick for command choices, front summaries, and battle reports

Renderer state should interpolate or display snapshots. Player input should become commands queued into the simulation rather than directly mutating rendered objects.

## Factory System

Phase 1 factory scope should prove throughput, bottlenecks, and shipping:

- edge resource nodes
- central open build grid
- extractors
- belts
- inserters
- processors/assemblers
- storage bins
- shipping depot
- a few shippable supply categories

Do not add power, fluids, trains, robots, circuits, blueprints, or late-game sprawl until the factory-war loop is proven.

## War System

Phase 1 war scope should prove that supply production changes the front:

- player-supported faction versus NPC faction
- two factions start on opposite sides
- old-school debuggable AI, not black-box AI
- command units assemble teams and pursue missions
- autonomous units dig, fight, reinforce, build outposts, and tunnel
- above-ground and underground layers exist in data from the start
- outcomes target roughly 80 percent supply-driven and 20 percent seeded random variance
- battle reports explain why the front changed
- tone is dark
- victory is total annihilation by reducing the enemy base to zero integrity after bombardment becomes available

## Integration Layer

The prototype now has a stable contract-and-facade stack:

- `CatalogIds`, `CatalogIntegrationManifest`, and `CatalogIntegrationMapper` define stable ids and mappings for production, research, and war integration.
- `ProductionIntegrationFacade`, `ResearchIntegrationFacade`, and `WarIntegrationFacade` provide pure C# adapter surfaces with deterministic smoke entry points.
- The live integration pass wires those facades into `TrenchworksSimulation` and exposes Play Mode tracker/UI hooks for research, logistics, war diagnostics, and team spawning.
- Recent scale passes added readable fog states, strategic visual LOD for zoomed-out squads, and a first shared squad-leader decision model inside `WarTeamSlice`.
- Recent war-side passes also added telemetry CSV / summary output, grenade anti-stalemate pressure, directional rifleman v2 source sheets, and a gameplay-role rule for multi-tile props larger than `1x1`.
- Recent terrain passes group the war map into deterministic, seeded biome patches over 8x8 chunks, with the renderer falling back to older terrain textures if beta biome files are missing.
- Recent playtest harness changes add biome override/regeneration controls and an `F8` manual opposing-squad spawn path; automatic front-wave spawning is disabled on play by default so the harness stays readable.
- Hardpoint access trunks now use vertical utility-line patterns that terminate at pad mouths/edges, which keeps the access geometry consistent with the later empty-pad contract.
- The live project now has V3 interface/logistics icon packs wired into prototype UI controls for editor Play Mode. This is not yet the final packaged-build asset pipeline.
- The 2026-05-17 live Play Mode review confirmed the current icon-wired UI is clean enough for the next pass.
- The 2026-05-18 worker/playtest report superseded immediate renderer integration as the next gate. The opening phase now needs a hidden paired front blueprint generator so both factions receive fair trench-front plans before squads claim/build/defend pieces.
- The 2026-05-19 decommission report says that staged front generation is now partially implemented: two actual front lines, clean no-man's-land except intended protrusions, access/support/supply trenches, empty hardpoint pads, front-line MG sockets, and additive F9 diagnostic overlays.
- The 2026-05-19 tileset failure audit superseded the earlier single-tile proof gate. Trench art now needs a semantic autotile contract before any more trench images are generated.
- The 2026-05-21 final decommission report accepts Tier 2 sandbag trenches as good enough after restoring the less-broken corner baseline.
- The 2026-05-22 worker report created the project-local Trenchworks asset catalog at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\art-pipeline\10_asset_catalog_twb_trenchworks.md` by adapting the preserved GPT Pro package into live project docs.
- The 2026-05-23 war-side art-kit completion audit found the current catalog has full first-pass generation coverage; the remaining Trenchworks work is runtime validation/integration, factory/logistics art, or later polish rather than more war-side generation.
- The 2026-05-23 war-art runtime wiring report gives generated MG/rifle/support/hardpoint/trench-overlay art a real runtime rendering path, while keeping simulation authority in `WarTeamSlice`, assignments, and blueprint snapshots.
- The 2026-05-23 front-establishment certification report fixed the stale seed `6107` certification failure and passed simulation plus command-plan smokes; the broader `6100-6120` diagnostic sweep still has two residual failures, seed `6109` front-line MG socket coverage and seed `6116` hardpoint pad density.
- The 2026-05-23 war-side readiness audit says the war side is controlled-systems-test ready, not play-ready: the live runtime set is four squad profiles, while the larger 50-template/33-role command plan remains partly catalog/future coverage.
- The 2026-05-22 Tier 1, Tier 2, and Tier 3 trench-art reports created contract-v3 `field_trench` candidate atlas/manifest sets for desert, temperate forest, and tropical jungle. Tier 2 and Tier 3 were generated as fresh procedural sets and report that old visual inputs were not reused.
- Superseded/Context - The 2026-05-21 Tier 3 definition was Tier 2 / v7.2 sandbags plus additive dirt berm and decor overlays generated by `generate_v7_3_tier3_sandbag_dirt_berm_assets.py`; the 2026-05-22 Tier 3 candidate set moved to a fresh procedural contract-v3 approach and still needs Unity/F9 acceptance.
- Tier 3 outputs belong under `tier3/field_trench` and `Review/{biome}/tier3`, not mixed into Tier 2 output folders.
- The GPT Pro art-pipeline package is preserved intact in Obsidian raw memory; workers should adapt copies into project docs rather than modifying raw source material.
- The GPT Pro factory-side package is also preserved intact in Obsidian raw memory for later factory/logistics-side work; it should not interrupt the current active art-catalog gate unless scope is explicitly shifted.
- Warning - Generated PNG alpha is not trustworthy for this pipeline. Continue using cyan-key cleanup and luminance-derived masks where applicable.
- Warning - MG dugout cutouts still need runtime anchor, scale, rotation, and all-orientation validation before they become final runtime assets.
- Battlefield renderer integration should resume only after the Phase 1 front-establishment contract is visually verified. Rendering must not expose unclaimed hidden blueprints in the normal player-facing view.

## Milestone 1 Prototype Shape

Milestone 1 is implemented as a playable proof loop, not the full game:

- factory screen has resource nodes, a build grid, simple belts/machines/storage, and a shipping depot
- player produces and ships a few supply categories
- war screen shows a stylized tactical map with two fronts, trenches, command units, and enemy-base integrity
- player sets doctrine and supply priorities; command units choose missions autonomously
- supply performance changes trench progress, casualties, readiness, and eventual bombardment progress
- success condition is enemy-base integrity reaching zero
- failure condition can remain provisional, but own-front collapse should be visible

Implementation facts from milestone 1 and later live project migration:

- live project folder is `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`
- canonical scene is `Assets\Scenes\TrenchworksPrototype.unity`
- old prototype folder `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype` is obsolete
- active Unity folder is not currently a git repository
- Unity version used is `6000.3.8f1`
- simulation tick is `0.1s`
- supply categories are ammo, trench materials, rations, and medical supplies
- war state tracks front progress, readiness, casualties, trench progress, tunnel/sap progress, bombardment progress, enemy-base integrity, doctrine, and autonomous command missions
- command missions include refit, push forward, extend trench, treat wounded, and prepare bombardment
- smoke test reported first shipment at tick `45`, first front gain at tick `679`, final front progress `67.5`, and enemy-base integrity `0.0`
- assembler transfer bugs were found and fixed during smoke testing: raw inputs no longer transfer onto output belts before crafting, and assembler input buffers now limit one input type from blocking the second ingredient

Recommended phase-one units:

- rifle infantry: basic combat pressure
- sappers/diggers: trench/tunnel progress
- engineers: fortifications/outposts
- medics/quartermasters: attrition reduction and readiness recovery
- command units: assemble mission teams and pick objectives

## Memory Items

- Decision - TWB Trenchworks should use a pure C# simulation layer with Unity as presentation/editor tooling.
- Decision - Tilemap is useful for static grid presentation, but custom grid data owns gameplay state.
- Decision - Phase 1 should postpone power, fluids, trains, robots, circuits, blueprints, multiplayer, shared accounts, and shared pets.
- Decision - War outcomes should target roughly 80 percent supply-driven and 20 percent seeded random variance.
- Decision - Command units are a promising phase-one AI structure: they assemble non-command units into autonomous mission teams.
- Decision - Tone is dark.
- Decision - Victory is total annihilation through enemy-base bombardment and destruction.
- Decision - Milestone 1 defaults to a bounded single-player scenario, doctrine-level control, readable war-industrial resources, a small unit roster, and a stylized tactical map.
- Superseded - An earlier post-milestone gate emphasized placement ergonomics, diagnostics, and pure C# tests; current immediate work is hidden front-establishment blueprints.
- Fact - Playtest stabilization expanded the factory to `500 x 500`, the war map to `1000 x 600`, and the UI to a bottom tray, map pan/zoom, and a clickable unit summary.
- Fact - Visible war units now have structural squad identity and a 15-cell commander cohesion radius; the default wave-drill speed is `5x` for readability.
- Fact - First-set war map props are terrain cell effects: cover reduces incoming bullet damage, concealment reduces spotting until contact, and slow terrain delays movement.
- Fact - Strategic zoom should show squad/team summaries rather than every individual soldier marker.
- Fact - The current `WarTeamSlice` AI direction is shared leader tree plus role-specialization overlays, not bespoke trees per leader.
- Fact - The latest `WarTeamSlice` squad pass broadens candidates to cover, contact, trench, resupply, and fallback cells, then scores them with combat-edge and route-risk weighting rather than pure forward pressure.
- Fact - Beta biome terrain uses deterministic seeded patching over 8x8 chunks with a read-only `WarWorld.Seed`.
- Fact - `F5` / `F6` / `F7` now regenerate temperate forest, tropical jungle, and desert war maps, `F8` spawns a single opposing squad pair on a random front lane, and automatic front-wave spawning is disabled by default for the harness.
- Fact - Vertical hardpoint access trunks must meet the pad mouth/edge rather than sit beside the pad.
- Fact - The war telemetry recorder outputs CSV plus a rolling Markdown summary and uses stall flags such as `QUIET_FRONT` and `CONTACT_NO_PROGRESS` for analysis.
- Fact - War-side art now follows directional source-sheet batching for rifleman v2 instead of one all-purpose sheet.
- Fact - Multi-tile war props must be tactically meaningful, not pure clutter.
- Fact - V3 UI/interface packs cover squad buttons, command orders, supply/resources, and war research icons.
- Fact - Unity icon validation and simulation smoke passed on 2026-05-17 after icon wiring.
- Fact - Live Unity Play Mode review passed on 2026-05-17; the icon-wired UI, hover tooltips, war map activity, right-side unit tracker, panning/zoom, and WASD-style controls were usable enough for continued work.
- Decision - Simulation and rendering LOD should stay separate: full simulation can continue while far-zoom rendering collapses grid and unit detail.
- Superseded - Battlefield renderer integration was the immediate post-Play-Mode-review gate, but the 2026-05-18 worker report redirected the lane to hidden front-establishment blueprints first.
- Decision - Gate 1 should implement a hidden paired front blueprint generator: no-man's-land curve, faction fighting lines, support/rear/service lines, communication connectors, and role-bearing trench pieces.
- Decision - Hidden front blueprints are simulation authority/input for squad claims, not player-facing decoration.
- Decision - Normal trench rendering should show claimed/started/built trench pieces, not unclaimed hidden preferred plans.
- Decision - Hardpoint pads should be generated last as empty access-trench-plus-pad sites; node identity stays undecided until engineer construction and specialist claiming.
- Decision - Hardpoint pads should remain visibly empty and non-functional in blueprint form so completed nodes emerge only after build/claim steps.
- Decision - Front-line MG points should be empty sockets anchored to actual Wave 1 front trench cells; they are not rear/support hardpoints and should not begin as manned nests.
- Decision - Old `CommandDugout` / `MortarPit` Phase 1 anchors should stay out of initial generation. Command and mortar functions should return through the empty hardpoint-pad claim/build path.
- Decision - Trench art should use reusable autotile/source-tile pieces rather than generated per-domino sheets.
- Decision - The immediate trench-art gate is contract-first: define the semantic autotile contract, then generate tiles against it.
- Decision - For trench art, source/image generation should provide material and layer references; Codex should own geometry, masks, atlas generation, runtime placement, and validation previews.
- Decision - The next Trenchworks art gate is runtime proof of the existing `field_trench` resolver path for `biome + tier + family + neighborMask` in Unity/F9, starting with one biome before broadening out.
- Decision - The immediate Trenchworks gate is visible controlled war-side proof in Unity Play Mode/F9 before any broader play-ready or runtime-art acceptance claim.
- Fact - Contract-v3 Tier 1, fresh procedural Tier 2, and fresh procedural Tier 3 `field_trench` candidate atlases exist for desert, temperate forest, and tropical jungle.
- Superseded - Tier 2 desert sandbag repair was the active gate before the 2026-05-21 final decommission report; Tier 2 is now accepted as good enough for the next pass.
- Decision - Tier 3 dirt-berm/decor overlays are additive to the Tier 2/v7.2 sandbag baseline and should remain in separate Tier 3 output folders.
- Decision - The raw GPT Pro art-pipeline package must remain unmodified in Obsidian; project-specific adaptations belong in live project docs.
- Decision - The raw GPT Pro factory-side package must remain unmodified in Obsidian; future factory-side adaptations belong in live project docs.
- Superseded - The first trench-art proof should be one individual `512x512` source tile, beginning with desert tier1 `trench_straight_ns`, before batch-producing the full 16-mask core.
- Decision - Approved individual tiles should be mechanically assembled into sheets, atlases, manifests, and previews after QA instead of asking image generation for complete sheet layouts.
- Decision - Squad movement should include lateral, cover, trench, contact, and resupply candidates; x-first movement made teams look too linear.
- Decision - Grenades are the first anti-stalemate tool for strong-cover deadlocks; they should remain visible and debuggable in the simulation.
- Warning - The first-pass map-prop generator still uses tuned random patch budgets rather than final route-validation.
- Warning - Current factory logistics are simplified; no splitters, rich inserter/lane logic, power, fluids, trains, robots, circuits, or blueprints yet.
- Warning - Current UI is IMGUI debug/prototype presentation, not final UI direction.
- Warning - `Application.dataPath` icon loading is an editor-prototype convenience and should not be treated as the final packaged-build asset pipeline.
- Warning - The war art package is a first-pass prototyping kit, not proof that runtime battlefield animation/tilemap rendering is complete.
- Warning - The beta biome patch size is still tuning territory and may change after live visual review.
- Warning - Do not treat the existing multi-depth front assignment graph as a substitute for the hidden paired front blueprint contract.
- Warning - Do not claim the front-establishment issue is solved until Gate 1 has a smoke/Play Mode check proving fair, in-bounds, hidden paired plans.
- Warning - Do not treat `dotnet build` as enough for this gate; the next check must include live Unity/F9 visual verification or an equivalent Unity-side validation.
- Warning - Old non-soldier war art should be considered legacy/reference until runtime callers and replacement needs are mapped. Do not delete it wholesale.
- Warning - Whole-sheet/tileset prompts tend to produce labelled presentation art or self-contained finished sheets, not reliable raw runtime source tiles.
- Warning - A runtime autotile resolver from occupied trench cells to `biome + tier + family + neighborMask` is still required before the art pipeline can drive final map rendering.
- Warning - Current Tier 2/Tier 3 trench art is pipeline-progress art, not finished runtime proof; Unity/F9 validation and runtime integration still matter.
- Warning - The 2026-05-22 contract-v3 candidate atlases passed reported pixel/socket QA, but should not be called accepted runtime art until Unity import, resolver selection, seams, sorting, and live readability pass.
- Warning - Runtime-wired generated art is not automatically accepted art; Unity/F9 must still prove scale, pivots, anchors, sorting, state switching, and packaged-build-safe loading.
- Warning - MG dugout prompts must avoid duplicate main trench lines and produce side-bulge modules with correct access openings.
- Source: [[short-term/2026-05-15-twb-trenchworks-research-plan]]
- Source: [[short-term/2026-05-15-twb-trenchworks-milestone-1-prototype-report]]
- Source: [[short-term/2026-05-17-twb-trenchworks-live-playmode-review-report]]
- Source: [[short-term/2026-05-18-twb-trenchworks-worker-report]]
- Source: [[short-term/2026-05-18-twb-trenchworks-extended-hardpoint-node-plan]]
- Source: [[short-term/2026-05-19-twb-trenchworks-worker-final-decommission-report]]
- Source: [[short-term/2026-05-19-trenchworks-final-decommission-report]]
- Source: [[short-term/2026-05-21-twb-trenchworks-worker-final-decommission-report]]
- Source: [[short-term/2026-05-21-twb-trenchworks-final-decommission-report]]
- Source: [[short-term/2026-05-22-twb-trenchworks-worker-report]]
- Source: [[short-term/2026-05-22-twb-trenchworks-tier1-trench-art-report]]
- Source: [[short-term/2026-05-22-twb-trenchworks-tier2-trench-art-report]]
- Source: [[short-term/2026-05-22-twb-trenchworks-tier3-trench-art-report]]
- Source: [[reports/memory-curation/2026-05-21-twb-trenchworks-art-pipeline-package-intake]]
- Source: [[reports/memory-curation/2026-05-21-twb-trenchworks-factory-side-package-intake]]
- Source: Official Factorio Wiki transport and inserter references.
- Source: Unity Tilemap, ScriptableObject, fixed update, and JSON serialization documentation.
