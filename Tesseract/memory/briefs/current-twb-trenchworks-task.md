# Current TWB Trenchworks Task

## Status

Active - updated 2026-05-23 after war-side readiness follow-up audit.

## Scope

Standalone TWB-tagged Unity 2D game: TWB Trenchworks.

This is not the main TWB Unity project, not Glassroot Garden, not Alchemy, not shared platform/account work, and not a request to edit the raw GPT Pro package in Obsidian.

## Project

- Live Unity project folder: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`
- Canonical scene: `Assets\Scenes\TrenchworksPrototype.unity`
- Art generation scripts/docs: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-art-generation`
- Recommended adapted catalog output: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\art-pipeline\10_asset_catalog_twb_trenchworks.md`
- Raw GPT Pro package, read-only: `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\raw\game-dev\twb-codex-art-pipeline-package\2026-05-21\extracted\twb_codex_art_pipeline_package`
- Obsidian memory: `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory`

## Latest Worker Reports

The command/general/mission plan was tailored from:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\implementation-packets\command-system-2026-05-22\19_twb_plan_fit_audit_and_tailored_implementation.md
```

The 2026-05-22 command-plan implementation reports say the tailored command-plan gates are implemented in scoped form through Gate 11. The 2026-05-22 combat/general/squad-tasking closure audit passed compile and simulation smokes, and the 2026-05-23 war-side readiness audit says the war side is now ready for controlled systems testing, not full play-ready certification.

The 2026-05-23 war-art runtime wiring report gave generated MG/rifle/support/hardpoint/trench-overlay art a real runtime rendering path. The 2026-05-23 front-establishment certification report fixed the stale seed `6107` certification failure and passed the full simulation and command-plan smokes, while leaving two broader seed-sweep residuals for later hardening: seed `6109` front-line MG socket coverage and seed `6116` hardpoint pad density.

The 2026-05-22 Tier 1, Tier 2, and Tier 3 trench-art reports still define the lower-priority trench-art candidate proof queue.

Confirmed:

- The project-local Trenchworks asset catalog exists at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\art-pipeline\10_asset_catalog_twb_trenchworks.md`.
- Contract-v3 Tier 1 `field_trench` candidates exist for desert, temperate forest, and tropical jungle.
- Fresh procedural contract-v3 Tier 2 `field_trench` sandbag candidates exist for desert, temperate forest, and tropical jungle; manifests record that old Tier 2 visual inputs were not used.
- Fresh procedural contract-v3 Tier 3 `field_trench` candidates exist for desert, temperate forest, and tropical jungle; manifests record that old Tier 1, Tier 2, and Tier 3 visual inputs and image generation were not used.
- All three candidate tiers passed their reported pixel/socket QA and produced combined overview review images.
- Unity import, Play Mode, F9 placement, resolver selection, seams, sorting, and live readability are still unverified.
- The raw GPT Pro package hash remained unchanged in the reports.

## Current Gate

War-side first-pass art-kit candidate coverage is complete from the current catalog evidence, and selected generated art now has runtime rendering hooks. Do not keep generating war-side art by default; move the lane to visible Unity Play Mode/F9 validation and controlled gameplay integration unless Bob explicitly requests a new visual category.

Current readiness boundary:

- Controlled in-editor systems-test ready, not full play-ready certification.
- The four legacy opening-drill profiles still work: Scout Patrol, Assault Section, Fortify Engineer Crew, and Supply Team.
- The broader 50 planned squad-template roster is command-spawnable and carries mission snapshots through the current command-plan smoke.
- Command-plan, man-emplacement, support-emplacement, enemy-general budget/difficulty, and full simulation smokes pass through the batch autorun harness.
- Seed `6107` front-establishment certification passes after the latest diagnostic fix.
- The broader `6100-6120` seed sweep is still `19/21`, with residual seed `6109` front-line MG socket coverage and seed `6116` hardpoint pad density failures.
- Live Play Mode/F9 visual proof is still needed for broad art/UI/VFX runtime acceptance, especially sorting, scale, anchors, state switching, minimap readability, and packaged-player loading.

Completed latest art targets:

- Trench Utilities V1: duckboard walkway, trench ladder access, drainage pump sump, firestep platform.
- Field Hazards V1: blasted brush screen, smoke-stained hedge line, flooded mud crater, rubble choke point.
- Hardpoint Pads V1: empty, MG, mortar, aid, and command pads across Tier 1 rough, Tier 2 reveted, and Tier 3 reinforced upgrades.
- Hardpoint Structures V1: MG nest, mortar emplacement, aid shelter, and command dugout structures across Tier 1 field, Tier 2 reveted, and Tier 3 reinforced upgrades.
- Rifle Fighting Positions V1: short rifle bay, long rifle bay, firestep pair, and prone scrape pair across Tier 1 rough, Tier 2 reveted, and Tier 3 reinforced trench-line upgrades, with north/east/south/west orientation variants.
- Frontline MG Sockets V1: single MG socket, wide MG slot, and recessed MG pocket overlays across empty socket, prepared firing bay, light MG nest, reinforced linked nest, and warded redoubt upgrade stages, with north/east/south/west orientation variants.
- MG Dugout Orientation V1: completed directional side-bulge MG dugout overlays across desert, temperate forest, and tropical jungle with Tier 1 field, Tier 2 timber-reveted, and Tier 3 reinforced-redoubt upgrades, north/east/south/west orientations, and explicit barrel-front/rear-entry metadata.
- Tactical Role Props V1: remaining role-bearing cover, concealment, slow, and blocking battlefield prop candidates across desert, temperate forest, and tropical jungle.
- Support Trench Lines V1: support trench line, service trench line, rear trench line, access trunk mouth, supply link strip, spawn link strip, communication connector, aid dugout niche, ammo dugout niche, command signal niche, and rear indirect line layered trench-state overlays across Tier 1 dug, Tier 2 reveted, and Tier 3 reinforced upgrades.
- Command And Map Markers V1: command/order/status/emplacement world overlays, war-map markers, minimap pips, and NESW route-state pieces for command readability, fog-aware awareness, supply/spawn/comms/front-map state, and debug-only hidden-plan overlays.
- Terrain Transitions V1: terrain transition overlays for biome edges, road/track edges, crater-to-ground, mud-to-dry, impassable, waterlogged, resource-node surround, and cover/concealment readability, plus war-map/minimap terrain swatches for desert, temperate forest, and tropical jungle.
- Persistent Morale VFX V1: persistent smoke/fire/gas/dust loops, morale rally/inspired/pinned/wavering/broken/command loops, faction/frontline readability loops, emplacement crew-state loops, and far-zoom substitutes.
- War HUD Chrome V1: player-facing war-mode HUD panel chrome, button states, gauge bars, tier-tree controls, status chips, and weapon/unit-role silhouettes for non-IMGUI RTS-style UI.
- Trench Variation Overlays V1: non-solid visual repetition breakers for long front-line, support, service, rear, supply, spawn, communication, and rear-indirect trench lines across desert, temperate forest, and tropical jungle.
- Combat Feedback V1: rifle muzzle, MG muzzle, mortar launch, bullet tracer, grenade burst, artillery impact, dirt impact, sandbag hit, metal spark, smoke puff, fire puff, suppression marker, casualty marker, and bombardment warning burst/readability VFX.
- Battlefield Decals V1: persistent terrain damage, combat aftermath, construction layout, repair patch, and hardpoint damage/destruction overlays across desert, temperate forest, and tropical jungle biome tints.
- Each generated asset has gameplay-state variants: blueprint, under-construction, active, damaged, destroyed.
- Hardpoint Pads V1 additionally includes the `foundation` state requested by the catalog hardpoint contract.
- Hardpoint Structures V1 also includes the `foundation` state requested by the catalog hardpoint contract.
- Rifle Fighting Positions V1 includes 336 transparent 192x192 PNGs covering 4 position families, 3 tiers, 4 orientations, and 7 visual states: blueprint, foundation, under-construction, active-empty, active-occupied, damaged, and destroyed.
- Frontline MG Sockets V1 includes 420 transparent 192x192 PNGs covering 3 socket families, 5 upgrade stages, 4 orientations, and 7 visual states: blueprint, foundation, empty, claimed, debug-front-arc, damaged, and destroyed. Manifest entries explicitly mark these as not completed MG nests and as containing no machine-gun barrel or operator.
- MG Dugout Orientation V1 includes 288 transparent 192x192 PNGs covering 3 biomes, 3 tiers, 4 orientations, and 8 visual states: blueprint, foundation, under-construction, active-empty, active-claimed, debug-front-arc, damaged, and destroyed. Manifest entries explicitly record `front_vector`, `rear_entry_vector`, `barrel_tip_canvas`, `crew_socket_canvas`, and `rear_opening_canvas`; the barrel points over the closed front parapet and the crew entry remains open at the rear.
- Tactical Role Props V1 includes 165 transparent 192x192 PNGs covering 11 role-bearing prop families, 3 biomes, and 5 visual states: blueprint, under-construction, active, damaged, and destroyed. Families cover sandbag-pile cover, timber-wall cover, boulder cover, stone-outcrop blocking, wrecked-field-gun cover, tall-reed concealment screen, broken-tree-shadow concealment screen, deep-mud slow patch, churned-mud slow field, stake-line slow/blocking obstacle, and timber-deadfall blocker. Manifest entries explicitly record gameplay role, footprint, movement blocking, concealment weight, slow weight, solid-asset classification, and not-decoration-only status.
- Support Trench Lines V1 includes 3,840 transparent 192x192 PNGs covering 11 support/rear/service/access/supply/spawn/communication/niche/indirect-line families, 3 tiers, 10 visual states, 16 NESW masks for true line families, and north/east/south/west directional variants for trunk/niche families. Manifest entries explicitly mark these as not base field-trench replacements, not completed hardpoints, not weapons, not operators, and not decoration-only props.
- Command And Map Markers V1 includes 4,278 transparent PNGs across `128x128`, `64x64`, `32x32`, and `24x24` canvases. It covers command aura/dispatch overlays, order/status/emplacement world markers, war-map markers, minimap pips, and NESW route-state masks. Manifest entries explicitly mark these as not soldier sprites, not combat VFX bursts, not decoration props, and not final HUD chrome.
- Terrain Transitions V1 includes 2,736 transparent PNGs across `128x128`, `64x64`, and `24x24` canvases. It covers 8 terrain-transition families, 3 biomes, 7 terrain states, 16 NESW masks for transition overlays, and simplified war-map/minimap terrain swatches. Manifest entries explicitly mark these as not base terrain tiles, not field-trench tiles, not solid props, not decoration, and not battlefield decals.
- Persistent Morale VFX V1 includes 554 transparent PNGs across `128x128`, `192x192`, `64x64`, `32x32`, `1024x128`, and `1536x192` canvases. It covers 20 looping persistent, morale, faction, frontline, and emplacement-state effects with individual frames, horizontal strips, and far-zoom substitutes. Manifest entries explicitly mark these as not burst combat feedback, not battlefield decals, not command/map markers, and not HUD icons.
- War HUD Chrome V1 includes 440 transparent PNGs across `32x32`, `48x48`, `64x64`, `80x80`, `96x32`, `160x160`, `176x112`, `192x32`, `192x192`, `256x16`, `256x32`, `256x96`, `256x384`, `320x32`, `320x80`, `384x64`, `384x104`, `384x256`, and `512x96` canvases. It covers 12 panel shells, 288 button-state sprites, 90 gauge-state sprites, 32 weapon/unit-role silhouettes, 10 tier-tree controls, and 8 status chips. Manifest entries explicitly mark these as final HUD chrome candidates, not world-space markers, not combat VFX, and not soldier sprites.
- Trench Variation Overlays V1 includes 1,152 transparent 256x256 PNGs covering 8 trench-line families, 3 biomes, 3 tiers, and the full 16-mask NESW set. Families cover front-line field trench, support line, service line, rear line, supply link, spawn link, communication connector, and rear indirect line visual variation. Manifest entries explicitly mark these as non-solid overlays, not base trench replacements, not support-line replacements, not terrain transitions, not battlefield decals, not hardpoints, not emplacements, not decoration props, and not gameplay/pathing/supply/comms behavior.
- Combat Feedback V1 includes 56 transparent 128x128 frame PNGs, 14 horizontal strip PNGs, a manifest with first-pass anchors, a README, and review sheets.
- Battlefield Decals V1 includes 162 transparent 192x192 PNGs covering 18 decal types, three biomes, and three severity variants, plus a manifest, README, overview, and per-biome contact sheets.
- Output includes transparent PNGs, review/contact sheets, and manifest/README notes with canvas size, anchors, state names, and caveats.
- Treat these as solid assets because they have gameplay footprint/state/task meaning, unlike decoration assets such as rocks, trash, or trees.
  Combat Feedback V1 and Battlefield Decals V1 are not solid assets; treat them as world-space feedback/overlay art that still needs runtime emitter/decal validation.
  War HUD Chrome V1 is not a solid asset; treat it as player-facing UI art that still needs live UI anchoring, scale, state-switching, and packaged-build loading validation.

Current handoff target:

- Treat the next gate as visible controlled runtime proof, not more war-side art production.
- Keep the asset catalog current with all generated solid-asset packs.
- Record likely gameplay roles before exposing assets through the build UI.
- Pick one low-risk first integration slice, preferably Shell-Crater Cover, Supply Niche, Drainage Pump Sump, Flooded Mud Crater, or Empty Hardpoint Pad tier/state preview.
- Do not expose Duckboard Walkway or Firestep Platform as ordinary blocking objects until walkable-overlay/trench-upgrade rules are settled.
- Do not expose MG or Mortar hardpoint pads as functional weapons until orientation, manning, ammunition, mission, and emplacement-brain rules are explicit.
- Do not expose MG Nest or Mortar Emplacement structures as functional weapons until orientation, manning, ammunition, targeting, mission, and emplacement-brain rules are explicit.
- Do not treat Rifle Fighting Positions V1 as runtime-accepted until Unity/F9 proves trench attachment, orientation, scale, pivot, sorting, socket preservation, and whether active-occupied variants stay debug-only.
- Do not treat Frontline MG Sockets V1 as runtime-accepted until Unity/F9 proves trench attachment, orientation, scale, pivot, sorting, socket preservation, and later growth into completed MG nest structures without flipping the front/rear relationship.
- Do not treat MG Dugout Orientation V1 as runtime-accepted until Unity/F9 proves trench attachment, `FrontlineMGSockets/V1` pairing, orientation, scale, pivot, sorting, muzzle anchor, crew socket, ammunition/manning state mapping, and front/rear firing relationship in all four orientations.
- Do not treat Tactical Role Props V1 as runtime-accepted until Unity/F9 proves placement footprint, collision/pathing, cover/LOS/projectile rules, concealment modifiers, slow modifiers, sorting, damage-state switching, minimap visibility, and build-menu exposure rules.
- Do not treat Support Trench Lines V1 as runtime-accepted until Unity/F9 proves NESW mask connections, trench attachment, route readability, supply/spawn/comms state mapping, walkability, sorting, minimap markers, and normal-play exclusion of debug-connection variants.
- Do not treat Command And Map Markers V1 as runtime-accepted until Unity/F9 proves sorting, fog/visibility rules, minimap scaling, war-map readability, command/order attachment, and normal-play exclusion of debug-only hidden-plan markers.
- Do not treat Terrain Transitions V1 as runtime-accepted until Unity/F9 proves terrain resolver mapping, NESW edge seams, sorting above base terrain and below trenches/units, zoom readability, fog/minimap scaling, and interaction with trenches/hardpoints.
- Do not treat Persistent Morale VFX V1 as runtime-accepted until Unity/F9 proves loop timing, emitter pooling, sorting, smoke/fire scale, zoom substitution, faction readability, fog visibility, and whether smoke affects LOS/detection/accuracy.
- Do not treat War HUD Chrome V1 as runtime-accepted until Unity/F9 proves canvas anchoring, nine-slice behavior where used, opacity over the map, click target sizes, UI state switching, scale at supported resolutions, silhouette consistency with unit/emplacement art, and packaged-build-safe loading.
- Do not treat Trench Variation Overlays V1 as runtime-accepted until Unity/F9 proves mask resolver selection, long-line randomization, seams, sorting above base trenches and below units/hardpoints/VFX, socket preservation, and that the overlays reduce repetition without duplicating decals, terrain transitions, or base trench art.
- Do not treat Combat Feedback V1 as accepted runtime VFX until emitters, anchors, timing, sorting, and zoomed-out readability have been checked in Unity.
- Do not treat Battlefield Decals V1 as accepted runtime overlay art until sorting layer, pooling/stack caps, persistence lifetime, zoom readability, and interaction with hardpoints/soldiers are checked in Unity.

Queued trench-art gate, currently lower priority until Bob redirects:

Review the fresh contract-v3 `field_trench` candidate overviews with Bob, then run a narrow one-biome Unity/F9 runtime proof for the selected direction.

The proof should confirm atlas import, resolver selection for `biome + tier + family + neighborMask`, seams, orientation, sort order, and live readability before expanding to all three biomes or all tiers.

Do not promote the new candidate atlases as accepted runtime art until this proof passes.

## Read First

- [[hot]]
- [[index]]
- [[wiki/game-dev/project-hierarchy]]
- [[wiki/game-dev/slynyrd-pixelblog-reference]]
- [[wiki/game-dev/external-game-dev-resource-index]]
- [[wiki/game-dev/twb-codex-art-pipeline-package]]
- [[wiki/twb-trenchworks/overview]]
- [[wiki/twb-trenchworks/architecture]]
- [[wiki/twb-trenchworks/open-questions]]
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-twb-trenchworks-tier1-trench-art-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-twb-trenchworks-tier2-trench-art-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-twb-trenchworks-tier3-trench-art-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-twb-trenchworks-worker-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\raw\game-dev\twb-codex-art-pipeline-package\2026-05-21\extracted\twb_codex_art_pipeline_package\CODEX_START_HERE.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\raw\game-dev\twb-codex-art-pipeline-package\2026-05-21\extracted\twb_codex_art_pipeline_package\MANIFEST.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\raw\game-dev\twb-codex-art-pipeline-package\2026-05-21\extracted\twb_codex_art_pipeline_package\docs\art_pipeline\10_ASSET_CATALOG.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\raw\game-dev\twb-codex-art-pipeline-package\2026-05-21\extracted\twb_codex_art_pipeline_package\docs\art_pipeline\README.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\AGENTS.md`

## Catalog Reference

The adapted catalog should remain the source map for current, missing, failed/reference-only, source-generation, cleanup, runtime-validation, and priority-milestone assets. The current worker should use it as context, not redo the catalog pass unless a runtime proof reveals a specific correction.

## Locked Decisions

- Tone: dark on the war side.
- Victory condition: total annihilation through eventual enemy-base bombardment.
- Phase 1: player versus NPC.
- The player supplies one faction at first.
- Multiplayer is desired later but not phase 1.
- Shared pets/accounts are not phase 1.
- Outcomes should be roughly 80 percent supply-driven and 20 percent seeded random variance.
- GPT/image generation provides source/material/layer references; Codex owns geometry, masks, atlas generation, runtime placement, and validation.
- Do not ask image generation for finished trench sprites, final trench maps, completed dominoes, or full final masks.
- Raw GPT Pro package content is preserved evidence and must not be edited in place.

## Allowed Write Paths

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\research\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\`

## Forbidden Write Paths

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\raw\game-dev\twb-codex-art-pipeline-package\2026-05-21\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\log.md`
- Main TWB Unity project folders.
- The Garden, Alchemy Lab, TWB-Marketing, website, shared-platform, or sprite-sheet automation source folders.
- Old `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype` folders unless only reading to confirm they are obsolete.

## Hard Rules

- Do not modify the raw GPT Pro package stored in Obsidian.
- Do not treat the raw `10_ASSET_CATALOG.md` as already specific enough for TWB Trenchworks.
- Do not resume broad Tier 1/Tier 2/Tier 3 generation before one selected biome path is proven in Unity/F9 unless Bob explicitly redirects.
- Do not promote the fresh procedural candidate sets as final runtime art until Unity/F9 validation passes.
- Do not promote failed corner-rotation attempts, checkerboard MG attempts, recolored MG variants, or old May 20 full-art source sheets.
- If generated art is referenced, separate accepted/current assets from failed/reference-only assets.
- If project files are changed, preserve review evidence and report exact checks.

## Done Criteria For Next Report

When the user asks the worker to report/decommission:

1. The visible Play Mode/F9 war-side proof is run or the blocker is reported.
2. Scout, Assault, Fortify Engineer, and Supply runtime squads are spawned or blocked with evidence.
3. General dispatch text, front establishment, contact/combat, ammo/health/stress, fallback/regroup, and open-ground-charge behavior are addressed.
4. Rifle bay, MG point, mortar, aid, command, and supply support brains are observed or their blocker is reported.
5. Generated runtime art acceptance is limited to what was actually seen in Unity/F9; candidate-only assets remain labeled as such.
6. The residual seed `6109` and `6116` certification failures are fixed, deferred, or reported as current risk.
7. The raw GPT Pro package remains unmodified.
8. Files touched and checks run are listed.
9. A short-term report is written.

## Report Destination

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\YYYY-MM-DD-twb-trenchworks-worker-report.md
```
