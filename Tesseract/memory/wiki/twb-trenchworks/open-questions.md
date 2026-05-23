# TWB Trenchworks Open Questions

## Product Scope

- Is `TWB Trenchworks` the final title or only a working name?
- Is this intended as a standalone game, a TWB companion game, or a future integrated mode?
- Should it use the shared pet/account system later, or not at all? Phase 1 does not include shared pets/accounts.

## Core Design

- Should the player choose which faction to support, or is the player faction fixed in phase 1?
- Session shape default for milestone 1: bounded single-player scenario. Should later versions become long campaign, endless war, or roguelite fronts?
- Victory condition is total annihilation through eventual enemy-base bombardment. What loss condition should punish the player: own base destroyed, supply collapse, time pressure, or enemy breakthrough?
- Tone is dark. Should this be grim historical-industrial, TWB weird-fiction dark, or a blend?
- Command-control default for milestone 1: player sets doctrine and supply priorities while command units choose missions autonomously. Should later versions allow direct mission orders?
- War view default for milestone 1: stylized tactical map with readable unit/front icons. Should later versions show small soldiers or stay abstract?
- What is the eventual multiplayer destination: synchronous PvP, co-op supply factory, asynchronous front competition, or another shape?

## Factory System

- How complex should belts/inserters be compared with Factorio?
- Are recipes strictly war supplies or also infrastructure, power, tools, and upgrades?
- Should resource nodes deplete, regenerate, or require expansion/efficiency upgrades?
- How much manual harvesting remains after early automation?

## War Simulation

- Phase-one unit roster default: rifle infantry, sappers/diggers, engineers, medics/quartermasters, and command units. Is this too many for the first playable slice?
- Phase-one supply categories default: ammo, trench materials, rations, and medical supplies. Should fuel or explosives be included in the first slice?
- How should underground and above-ground layers interact?
- Are trenches built by units, by abstract orders, or by supply thresholds?

## Technical

- Superseded - Which Unity Hub project entry should be canonical after stabilization: `prototype`, migrated `prototype\My project`, or a cleaned single project layout? The live project home is now `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
- Should the legacy strategic war loop remain alongside the new team-war facade, or should one become authoritative before the next phase?
- Should team spawn buttons debit production inventory by team resource cost in the next integration pass, or stay prototype-level for now?
- Should entry-lane choice become per-team spawn orders once team spawning exists, instead of resetting the whole scenario?
- Should milestone 2 add explicit inserter/adjacent-transfer devices, or keep simplified belt transfer until Trenchworks' identity is clearer?
- What diagnostics are needed first: production-rate display, bottleneck markers, hover tooltips, supply ledger, or command-mission explanations?
- What pure C# tests should become the first formal test suite: recipes, transfer rules, shipping, command mission selection, seeded war outcomes, or all of these?
- When should the prototype move from IMGUI debug presentation to a proper Unity UI/Tilemap visual pass?
- Should a standalone player build be produced for early review, or is Unity Editor play mode enough for the next gate?
- Should the playtest control surface for biome regeneration and manual squad spawning stay hotkey-only, tray-only, or both?
- Should automatic front-wave spawning remain disabled by default now that `F8` manual pair spawning exists?
- Should the beta 8x8 biome patch sizing stay as-is, or be tuned after live visual review?
- Should grenades become a dedicated supply item instead of reusing generic ammo once the anti-stalemate role settles?
- What asset loading pipeline should replace `Application.dataPath` before packaged builds: Resources, Addressables, sprite atlases, or another approach?
- Superseded - Should battlefield sprite/tile renderer integration start with units, trenches, terrain, or combat FX first? Start with unit sprite rendering for existing war units, then trench/terrain tile rendering, then restrained combat FX, while preserving simulation authority.
- Superseded - Is battlefield renderer integration the immediate next gate after the 2026-05-17 live Play Mode review? No; the 2026-05-18 worker report makes hidden paired front blueprint generation the immediate gate first.
- How much debug-only visibility should the hidden front blueprint generator expose to developers without leaking preferred trench plans into normal player-facing play?
- What exact completion threshold should move Phase 1 from initial trench-line establishment into Phase 2 active war?
- What fairness/power score should define a balanced paired front: piece count, distance, cover, trench depth, hardpoint roles, sector weight, or a combined score?
- What size should empty hardpoint pads default to: 4x4, 8x8, or mixed by node scale?
- How many hardpoint pads per sector are enough to stay readable without cluttering the map?
- Should the active Unity project be placed under git before the next large implementation pass?
- Do the current F9 overlays show the staged front generator clearly enough after the MG/CMD/MTR cleanup, or does the generator need another implementation pass before art production?
- Should old trench stamps be used as temporary runtime placeholders, or kept strictly as visual reference while a new Phase 1 sprite pack is produced?
- Which runtime callers still depend on the older non-soldier war art package?
- Which unit/squad count is authoritative after the latest asset/runtime pass: older docs saying `24` roles or the newer reported `33` war member roles?
- How many trench families should exist beyond `field_trench` once hardpoint pads, MG sockets, dugouts, support trenches, and supply-width variants are implemented?
- What is the first runtime proof path for mapping occupied trench cells to `biome + tier + family + neighborMask` against the new contract-v3 candidate atlases?
- Should the current contract-v3 `field_trench` standard stay at 16-mask cardinal, or does Unity/F9 proof show that a richer 47/48-tile, Wang, marching-squares, or RuleTile contract is needed later?
- Which candidate should be proven first in-engine: Tier 1, fresh procedural Tier 2, or fresh procedural Tier 3, and for which biome?
- Should Tier 2 desert sandbag outside/convex corners be solved with explicit convex-corner masks/templates rather than transformed concave templates?
- Should the six current sandbag source layers be preserved as row/junction templates only, or should a new clean individual straight/corner/cap template sheet be requested later?
- What is the final runtime anchor, scale, rotation, and orientation contract for MG dugout assets?
- What assets are required for rifle fighting positions, and should they be generated as separate modules from trenches and MG dugouts?
- Superseded - Which items from the GPT Pro `10_ASSET_CATALOG.md` belong in the actual Trenchworks phase-one asset catalog? The project-local catalog now exists; future questions should target specific catalog corrections revealed by runtime proof.
