# TWB Trenchworks

## Status

Phase 1 front/trench/terrain work has moved from broad war-side generation into controlled runtime proof. The 2026-05-22 command-system package covers Gates 0-9 in the live bridge, including compatibility aliases, mission profiles, player/enemy assignment, member-task effects, the catalog-driven unit tree, and Gate 9 support/medical loops. Helper-portrait dispatch UI is wired. Staged hidden front generation, empty hardpoint pads, front-line MG sockets, F9 diagnostics, deterministic beta biome patches, the playtest biome/squad harness, and the trench autotile source-tile strategy were advanced in the 2026-05-19 reports. The project-local asset catalog now exists, the 2026-05-23 war-side art-kit audit found first-pass generation coverage, and the 2026-05-23 runtime wiring report gave selected generated MG/rifle/support/hardpoint/trench-overlay art a real runtime rendering path. The current war side is controlled-systems-test ready, not play-ready: four runtime squad profiles are live, command/emplacement smokes pass, seed `6107` front-establishment certification passes, and the broader seed sweep still has `2/21` residual failures. Fresh contract-v3 Tier 1, Tier 2, and Tier 3 `field_trench` candidates exist for desert, temperate forest, and tropical jungle; they remain review/runtime-proof candidates, not Unity/F9-accepted art yet.

## Summary

TWB Trenchworks is a proposed standalone Unity 2D game under the The World Beneath umbrella. It is not a browser World Key and should not be planned as a Phaser/Vite project.

The core concept is a top-down, grid-based factory/logistics game feeding an automated two-faction trench war. The player designs and operates production systems; the armies consume the resulting inputs and fight through an autonomous war simulation.

## Scope

- Umbrella project: The World Beneath.
- Proposed project type: standalone Unity 2D game.
- Local project folder: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
- Canonical scene: `Assets\Scenes\TrenchworksPrototype.unity`.
- Shared pet/account integration: possible later; explicitly out of phase 1.
- Current phase: run a visible Unity Play Mode/F9 controlled war-side proof, then return to narrower art or seed-sweep hardening based on what fails.
- Prototype project folder: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype` is obsolete.

## Core Fantasy

The player is not manually fighting the war. The player builds the industrial/logistics machine that feeds the war.

Factory side:

- resource nodes around the build-area edge
- central open factory build area
- grid-based machines, belts, inserters, storage, recipes, and shipping
- a shipping/export point that sends war supplies to the front

War side:

- two factions start on opposite sides
- old-school game AI controls both armies
- armies dig toward each other, build trenches, and fight
- war simulation uses above-ground and underground layers
- supplies produced by the player affect combat readiness and outcomes
- player may inspect the war on a second screen and possibly a minimap on the factory screen

## Current Design Bias

Use Unity 2D with a simulation-first C# architecture:

- tile/grid simulation separate from rendering
- factory grid and war grid as distinct simulation domains
- deterministic or semi-deterministic tick loop
- data-driven recipes, machines, supply crates, faction needs, and war actions
- Unity Tilemap or equivalent 2D grid presentation for early prototypes

See [[wiki/twb-trenchworks/architecture]] for the current architecture recommendation.

## Phase 1 Decisions

- Phase 1 is player versus NPC.
- The player supplies one faction at first.
- Multiplayer is desired eventually but is not phase 1.
- Shared account systems and shared pet systems are not phase 1.
- Tone is dark.
- Victory condition is total annihilation: the player-supported side eventually unlocks the ability to bombard and destroy the enemy base.
- War outcomes should be approximately 80 percent supply-driven and 20 percent seeded random variance.
- Player unit choice should be requisition/spawn strategy, not direct tactical control.
- Command units can assemble non-command units into autonomous mission teams.

## Milestone 1 Defaults

These are Bob/orchestrator defaults unless the user revises them before implementation:

- Session shape: one bounded single-player scenario that can be restarted, with save/load postponed unless Unity setup makes it cheap.
- Command-control level: player sets supply priorities and broad doctrine; command units choose missions autonomously.
- Phase-one unit roster: rifle infantry, sappers/diggers, engineers, medics/quartermasters, and command units.
- Resource naming: readable war-industrial names first, with TWB flavor added after the loop is proven.
- War view style: stylized tactical map with readable unit/front icons, plus a minimal factory-screen war status panel.

## Next Gate

The active 2026-05-23 gate is visible controlled war-side proof in Unity Play Mode/F9.

The preserved GPT Pro package remains raw evidence in:

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\raw\game-dev\twb-codex-art-pipeline-package\2026-05-21\extracted\twb_codex_art_pipeline_package
```

Do not edit the raw package. The adapted project-local catalog is:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\art-pipeline\10_asset_catalog_twb_trenchworks.md
```

The immediate worker should spawn the four live runtime squad profiles, confirm general dispatch/front/contact/combat behavior, observe rifle/MG/support emplacement brains, and capture screenshots/logs. Treat generated art as accepted only where Unity/F9 actually proves scale, pivot, sorting, anchor, state, and loading behavior. The lower-priority trench-art queue remains: review Tier 1/Tier 2/Tier 3 overviews with Bob, then prove one selected `biome + tier + family + neighborMask` resolver path in Unity/F9 before accepting the candidates as runtime art.

## Memory Items

- Fact - The user wants this project to be a Unity game, not a browser game.
- Fact - The concept combines Factorio-style factory/logistics planning with automated trench warfare.
- Fact - The first research/planning report is complete and reviewed.
- Fact - Current live project home is `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
- Fact - Canonical live scene is `Assets\Scenes\TrenchworksPrototype.unity`.
- Fact - The live Unity folder is not currently a git repository.
- Fact - `SampleScene.unity` still exists, so workers must verify the prototype scene before Play Mode testing.
- Superseded - The old `prototype` path is obsolete and should not be treated as the working home.
- Fact - Milestone 1 uses Unity `6000.3.8f1`.
- Fact - Milestone 1 includes a pure C# simulation layer with Unity IMGUI presentation/input.
- Fact - Milestone 1 demonstrates factory shipping affecting readiness, casualties, front movement, bombardment progress, and enemy-base integrity.
- Fact - Milestone 1 smoke test reached enemy-base integrity `0.0` through sustained supply advantage.
- Fact - The user reported that importing through Unity Hub and pressing Play showed no visible prototype behavior.
- Fact - The live integration pass wires `CatalogIntegrationContracts`, `CatalogIntegrationManifest`, `CatalogIntegrationMapper`, `ProductionIntegrationFacade`, `ResearchIntegrationFacade`, and `WarIntegrationFacade` into `TrenchworksSimulation` with Play Mode UI hooks.
- Fact - The integrated no-window smoke passed; the remaining check is a visible Play Mode smoke after Unity refresh/recompile.
- Fact - Playtest stabilization expanded the factory to `500 x 500`, the war map to `1000 x 600`, and the UI to a bottom tray, map pan/zoom, and a clickable unit summary.
- Fact - Fog readability now uses grey unseen ground, brighter remembered/visible states, full-cell known-ground rendering, and larger role-based vision radii.
- Fact - Strategic visual LOD collapses squads into aggregate markers with count badges when zoomed out, while preserving fog fairness for enemy counts.
- Fact - The first squad-leader AI model in `WarTeamSlice` uses shared leader decisions plus role-specific scoring for scout, assault, engineer, and supply teams.
- Fact - The latest squad-leader pass adds a shared blackboard, utility-style candidate scoring, combat-edge bias toward hold/dig-in, lateral movement, and formation collision avoidance.
- Fact - The war map now has a telemetry recorder, grenade anti-stalemate pressure, clearer casualty markers, trench-channel readability, render smoothing, and cached influence-map sampling.
- Fact - War-side source art now uses directional rifleman v2 sheets for movement, crouch, crawl, primary rifle fire, and secondary grenade action.
- Fact - The war-side asset pipeline now treats any map decoration larger than `1x1` as gameplay-relevant cover, concealment, slow terrain, blocking terrain, or a mixed tactical role.
- Fact - The telemetry recorder writes CSV plus rolling Markdown summaries and watches `CONTACT_NO_PROGRESS`, `QUIET_FRONT`, and `NO_MATERIAL_CHANGE`.
- Fact - Grenade bursts plus a small full-cover leak are the current anti-stalemate tools for strong-cover deadlocks.
- Fact - Trench cells now carry `TrenchNetworkId` and `TrenchSupplyConnected`; supplied trench networks draw a visible strip and selected units expose field-map reasoning.
- Fact - Trench grammar now prefers north-south fire lines, east-west communication connectors, 3-4 tile widths, and visible slot markers for trench roles.
- Fact - Trench readability now treats shallow trenches, deep trenches, and soldiers inside friendly trenches as distinct states rather than one blob.
- Fact - Quiet-front recovery lets squad leaders probe out from held trenches after the front goes silent.
- Fact - Command units are 2-cell vertical anchors, and orphaned units can seek replacement command or recycle at base.
- Fact - Fog visuals are removed from the visible war map.
- Fact - V3 interface/logistics icon package has `4/4` packs and `64` labelled icons.
- Fact - Unity batchmode icon validation and simulation smoke both passed on 2026-05-17 after the latest UI icon wiring.
- Fact - The first-pass war-side asset package includes prototype-ready source sheets, transparent sheets, cutouts, multi-tile pieces, terrain tiles, v2 unit sheets/frames, and V3 interface icon packs.
- Fact - The bottom/action UI controls now use V3 icon art with hover tooltips.
- Fact - The live Unity Play Mode visual review passed on 2026-05-17. The icon-wired UI, hover tooltips, right-side tracker, war map activity, panning/zoom, and WASD-style controls were readable and usable enough for the next pass.
- Fact - Screenshot evidence for the live Play Mode review is preserved under `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\live-playmode-review-2026-05-17-*.png`.
- Superseded - Immediate battlefield sprite/tile renderer integration was the next gate after the 2026-05-17 live Play Mode review, but the 2026-05-18 worker/playtest report redirected the lane to Phase 1 front establishment first.
- Fact - Seven prior unit-tactics gates were implemented before the 2026-05-18 report: contact anti-stall/hold reasons, multi-depth front assignment graph, socket occupation/anti-blob, construction/hardpoint roles, combat range/spotting/terrain/elevation/posture, support requests/stalled-sector recovery, and legacy war-unit loop retirement.
- Fact - The current prototype start sequence now uses an integrated front drill instead of the old visible legacy wave-unit drill. It unlocks integrated squads/entry lanes, clears legacy war units, spawns one random integrated squad from each top/mid/bottom entry point per side, repeats every 30 strategic seconds, and caps at 24 teams per faction.
- Fact - Team supply consumption was adjusted so food/construction are not passively burned while teams merely move; food/ammo drain under contact pressure through the existing `ConsumeForTeam` path.
- Decision - Phase 1 opening should generate hidden preferred trench-front blueprints for both sides before squads improvise.
- Decision - Hidden front blueprints must be balanced/fair by scoring, include fighting/support/rear/service lines plus communication connectors, and stay invisible to the normal player-facing renderer until squads claim/start pieces.
- Decision - Phase 2 should begin only after enough of the initial trench line is complete; the exact threshold remains a tuning/open question.
- Decision - The next implementation gate is Gate 1: hidden paired front blueprint generator.
- Fact - The 2026-05-19 worker advanced the hidden front blueprint model into a staged trench-generation system with two front lines, clean no-man's-land except intended front-line protrusions, access trenches, support lines, supply/spawn-link branches, empty 4x4/8x8 hardpoint pads, front-line MG sockets, and additive F9 diagnostics.
- Fact - Front-line MG points should be empty sockets attached directly to Wave 1 front trench cells and protruding into no-man's-land; they should not spawn as pre-filled or manned MG nests.
- Fact - `CMD` and `MTR` were old explicit `CommandDugout` and `MortarPit` Phase 1 anchors and were removed from Phase 1 generation. Command/mortar functionality should return later through empty hardpoint pads and specialist claim/build flows.
- Fact - Beta biome base terrain now ships as accepted temperate forest, tropical jungle, and desert sets, rendered as deterministic 8x8 chunk patches with fallback to the older terrain textures when beta files are unavailable.
- Fact - Playtest control coverage now includes biome regeneration/override and a manual opposing-squad harness: `F5` / `F6` / `F7` regenerate temperate forest, tropical jungle, and desert maps, `F8` spawns one player and one enemy integrated squad on a random top/mid/bottom lane, and automatic front-wave spawning stays off by default for that harness.
- Fact - Hardpoint access trunks now use vertical utility-line pieces and must terminate into the pad mouth/edge rather than lying beside the pad as horizontal bars.
- Fact - F9 debug snapshots now preserve explicit construction waves, and additive wave views prioritize MG sockets, front skeletons, empty pads, and hardpoint access markers before heavy spawn-link filler.
- Fact - Soldier V2 sprites appear to be the war-side asset class to keep. Older non-soldier war art is mostly legacy/reference after the hardpoint redesign.
- Decision - Do not delete old non-soldier war art wholesale until runtime callers are mapped and replacements exist.
- Warning - Some broader smoke failures were still reported around fighting-distance and staged-route reachability expectations. Do not declare the current front visuals final before live Unity/F9 verification.
- Warning - `dotnet build TWB-TrenchWorks.sln --no-restore` passing is useful but does not prove Unity import, Play Mode, or F9 visual correctness.
- Warning - The biome patch sizing and control surface are still beta review tools; live Unity Play Mode should confirm the shortcuts are received cleanly and do not fight the editor.
- Superseded - Fresh Trenchworks worker should run live Unity/F9 verification first and then commission `Phase 1 Front Blueprint Sprite Pack v4`; the later 2026-05-19 final decommission report shifted the immediate gate to one-tile autotile proof.
- Fact - The 2026-05-19 final worker pivoted trench art direction from per-domino prompt packs to reusable autotile/source-tile pieces.
- Fact - The minimum functional field-trench autotile core is `16` cardinal N/E/S/W neighbor-mask tiles.
- Fact - The old one-tile prompt lane began with `docs\trench-autotile-tile-prompts\desert\tier1\trench_straight_ns.md`, but it is now reference-only.
- Decision - Per-domino prompt files are deprecated for generation and should be retained only as mapping/footprint references.
- Decision - Define the semantic autotile contract before asking image generation for any more trench art.
- Superseded - Prefer one individual `512x512` tile per image-generation prompt, then mechanically assemble approved tiles into sheets, atlases, manifests, and previews.
- Warning - Prompting for a whole "sprite sheet" or "tileset sheet" tends to produce labelled presentation art or finished assembled sheets rather than reliable source tiles.
- Warning - Avoid artificial 18-20 tile ceilings; create as many tiles/variants as needed for clean full tilesets per biome, tier, and trench family.
- Warning - Renderer support for autotile lookup is not implemented yet; Trenchworks still needs a resolver from occupied trench cells to `biome + tier + family + neighborMask`.
- Fact - Wide-bottom trench generation/rendering now uses deterministic floor, perimeter/berm, corner/notch, and spill atlas concepts rather than finished domino sprites.
- Decision - For trench art, GPT/image generation should provide source/material/layer sheets; Codex should own geometry, masks, atlas generation, and runtime placement.
- Fact - The 2026-05-21 final decommission report accepts Tier 2 sandbag trenches as "good enough" after restoring the less-broken corner baseline.
- Decision - Tier 3 now means Tier 2 / v7.2 sandbags plus additive dirt berm and decor overlays, generated by `generate_v7_3_tier3_sandbag_dirt_berm_assets.py`.
- Decision - Tier 3 outputs belong only under `tier3/field_trench` and `Review/{biome}/tier3`.
- Fact - Correct Tier 2 biome material source sheets are the May 21 desert, temperate forest, and tropical jungle images listed in [[briefs/current-twb-trenchworks-task]].
- Decision - Forest and jungle Tier 2 generation now use `material_library: True`.
- Superseded - Old May 20 full-art source sheets are no longer used for Tier 2.
- Warning - Generated PNG alpha should not be trusted; cyan-key cleanup and luminance-derived dirt masks remain required for asset production.
- Warning - MG dugout prompts must forbid duplicate main trench lines and keep the west-facing side-bulge asset open on the east/right access side until runtime orientation validation is done.
- Open Question - Final MG dugout anchor, scale, rotation, and all-orientation behavior still need runtime validation.
- Open Question - Rifle fighting positions need their own asset-generation pass.
- Fact - GPT Pro art-pipeline package is preserved intact at `memory/raw/game-dev/twb-codex-art-pipeline-package/2026-05-21/`.
- Fact - GPT Pro factory-side package is preserved intact at `memory/raw/game-dev/twb-codex-factory-side-package/2026-05-21/` for future factory/logistics work.
- Fact - The Trenchworks-specific project-local art catalog exists at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\art-pipeline\10_asset_catalog_twb_trenchworks.md`.
- Fact - Contract-v3 Tier 1, fresh procedural Tier 2, and fresh procedural Tier 3 `field_trench` candidate atlases now exist for desert, temperate forest, and tropical jungle.
- Warning - These contract-v3 candidate atlases passed reported pixel/socket QA but are not Unity/F9-accepted runtime art until import, resolver selection, seams, sorting, and live readability are validated.
- Fact - The 2026-05-23 war-art runtime wiring report gives selected generated MG/rifle/support/hardpoint/trench-overlay art a real runtime rendering path, but Play Mode/F9 visual acceptance and packaged-build-safe loading remain unproven.
- Fact - The 2026-05-23 front-establishment certification report fixed the stale seed `6107` certification failure and passed simulation plus command-plan smokes; the broader `6100-6120` sweep still has seed `6109` front-line MG socket coverage and seed `6116` hardpoint pad density residuals.
- Warning - The war side is controlled-systems-test ready, not play-ready; only four runtime squad profiles are live by default.
- Next Gate - Run visible Unity Play Mode/F9 proof for the four live squad profiles and support/emplacement behavior, with screenshots/logs, before broader playtest-readiness claims.
- Warning - Do not confuse the existing multi-depth front assignment graph with the new hidden paired front blueprint requirement.
- Warning - Do not claim the opening/front issue is fixed until Unity Play Mode or an equivalent simulation smoke validates the new blueprint-driven opening.
- Warning - Renderer integration should preserve hidden-plan secrecy; unclaimed hidden trench plans must not appear in the normal play view.
- Fact - Worker verification on 2026-05-18: `dotnet build TWB-TrenchWorks.sln --no-restore` passed with 0 warnings/0 errors, but the solution is minimal and is not a Unity compile substitute. Unity batchmode smoke was blocked because the Unity project was already open.
- Warning - The current icon-loading path uses `Application.dataPath`, which is acceptable for editor Play Mode but not a final packaged-build asset pipeline.
- Warning - Do not confuse asset package completeness with final runtime sprite, tilemap, animation, or packaged-build integration.
- Warning - The old nested prototype path is obsolete; future checks should stay on the live `TWB-TrenchWorks` project home.
- Decision - Phase 1 is player-versus-NPC, with the player supplying one faction.
- Decision - Shared pet/account integration is optional later and must not drive phase 1.
- Decision - Multiplayer is desired later but should not be built in phase 1.
- Decision - Tone is dark.
- Decision - Victory is total annihilation through eventual bombardment and destruction of the enemy base.
- Decision - Milestone 1 should use a bounded scenario shape, doctrine-level command control, a small readable unit roster, and a stylized tactical war map unless revised by the user.
- Open Question - Final title is not locked; `TWB Trenchworks` is the working lane name.
- Open Question - Whether the game is a separate paid/standalone product, internal prototype, or later TWB companion release remains unresolved.
- Source: User request, 2026-05-15.
- Source: [[short-term/2026-05-15-twb-trenchworks-research-plan]]
- Source: [[short-term/2026-05-15-twb-trenchworks-milestone-1-prototype-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-fog-readability-reveal-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-visual-lod-rendering-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-squad-leader-ai-implementation-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-war-team-authority-field-map-pass-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-trench-network-supply-fieldmap-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-trench-pattern-grammar-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-trench-readability-depth-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-battle-stall-recovery-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-command-footprint-orphan-behavior-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-fog-of-war-removal-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-run-telemetry-pass-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-cover-grenade-combat-pass-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-visual-clarity-pass-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-visual-quality-pass-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-playtest-stabilization-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-field-map-cache-performance-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-trench-network-diagnostics-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-anti-stall-quiet-probe-report]]
- Source: [[short-term/2026-05-16-twb-trenchworks-unsupported-trench-behavior-report]]
- Source: [[short-term/2026-05-17-twb-trenchworks-worker-final-decommission-report]]
- Source: [[short-term/2026-05-17-twb-trenchworks-live-playmode-review-report]]
- Source: [[short-term/2026-05-18-twb-trenchworks-worker-report]]
- Source: [[short-term/2026-05-19-twb-trenchworks-worker-final-decommission-report]]
- Source: [[short-term/2026-05-19-trenchworks-final-decommission-report]]
- Source: [[short-term/twb-trenchworks-autotile-no-tile-limit-2026-05-19]]
- Source: [[short-term/twb-trenchworks-raw-module-prompt-hardening-2026-05-19]]
- Source: [[short-term/twb-trenchworks-trench-overlay-cutout-prompts-2026-05-19]]
- Source: [[short-term/2026-05-21-twb-trenchworks-worker-final-decommission-report]]
- Source: [[short-term/2026-05-21-twb-trenchworks-final-decommission-report]]
- Source: [[short-term/2026-05-22-twb-trenchworks-worker-report]]
- Source: [[short-term/2026-05-22-twb-trenchworks-tier1-trench-art-report]]
- Source: [[short-term/2026-05-22-twb-trenchworks-tier2-trench-art-report]]
- Source: [[short-term/2026-05-22-twb-trenchworks-tier3-trench-art-report]]
- Source: [[reports/memory-curation/2026-05-21-twb-trenchworks-art-pipeline-package-intake]]
- Source: [[reports/memory-curation/2026-05-21-twb-trenchworks-factory-side-package-intake]]
