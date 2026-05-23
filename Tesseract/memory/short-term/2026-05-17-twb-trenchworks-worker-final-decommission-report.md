# TWB Trenchworks Worker Final Decommission Report

Date: 2026-05-17
Worker scope: standalone Unity 2D factory/logistics and automated trench-war game under The World Beneath umbrella.

## 1. Current working context

- Project path: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks`
- Active Unity project/folder: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`
- Unity version used by the project/checks: `6000.3.8f1`
- Intended active scene: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scenes\TrenchworksPrototype.unity`
- Secondary/default Unity sample scene still present: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scenes\SampleScene.unity`
- Orchestration workspace for this worker window: `C:\Users\yrred\Documents\New project 2`
- Git/branch state: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks` is not a git repository; `git status` returns `fatal: not a git repository`.

Active scripts and systems of note:

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksWarAssetImportSettings.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\IntegratedPrototypeSystems.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarIntegrationFacade.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamEntities.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamTypes.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Production\ProductionWorldSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Research\ResearchTreeFactory.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\TrenchworksCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\ResearchCatalog.cs`

## 2. What changed

This worker window took the prototype from an unclear Unity entry-point/project-folder state into a visibly playable Unity prototype with a large factory map, automated trench-war map, early production/research/war systems, and a complete first-pass war-side asset package.

Major project/setup changes:

- The canonical Unity Hub project path is now `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
- The intended playable scene is `Assets\Scenes\TrenchworksPrototype.unity`.
- `PrototypeBootstrap` has a runtime fallback so Play Mode can create the prototype bootstrap if a scene lacks one.
- `TrenchworksProjectSetup` has editor menu helpers for opening/recreating/validating the prototype scene and running the simulation smoke test.
- The prototype scene/build entry point was made obvious enough that pressing Play in the active project displays the game UI rather than doing nothing.

Major systems touched:

- Factory grid size and navigation.
- War grid size, entry zones, wave drill, camera pan/zoom, WASD controls.
- Bottom builder-style UI rail and category tray.
- Top war tracker and right-side unit summary/tracker.
- Production-side starter context: worker house, hiring office, workers, resource nodes, shipping lanes, blueprint/build workflow.
- Research tree and research production scaffolding.
- War team/squad authority layer, squad templates, entry lanes, orders, contact/dig/hold/connect concepts.
- War run telemetry recorder and smoke/diagnostic hooks.
- Trench readability and trench network/supply-field state.
- First pass of visual clarity, combat/status markers, and war-side asset generation.

Play mode status:

- Play Mode visibly worked during user-observed live testing: the prototype rendered the TWB Trenchworks UI, war map, units, right-side unit summary, bottom rail, and top tracker.
- Latest post-icon-wiring Play Mode was not visually re-reviewed by the user in the editor; however Unity batchmode compile/import and simulation smoke passed after the wiring.

Nested `prototype\My project` folder:

- The old suspicious nested project was part of the initial diagnosis only.
- The user later moved/destroyed the old prototype location and declared the new home: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
- This final worker pass did not write to `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype` or `prototype\My project`.
- Do not assume the old `prototype` folder still exists or is useful.

## 3. Current prototype state

Currently working:

- Unity Hub should be pointed at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
- `TrenchworksPrototype.unity` is the canonical scene.
- Pressing Play starts a visible OnGUI prototype with top tracker, map view, right tracker, bottom controls, pause/speed/reset controls, mouse wheel zoom, mouse drag pan, and WASD map movement.
- Factory side has starter resources, worker house, hiring office, five workers, blueprint construction, starter component stockpile concepts, varied machine footprints, shipping areas for top/middle/bottom lanes, and supply routing diagnostics.
- War side has a large automated wave-drill battlefield with top/middle/bottom entry zones, seeded terrain/obstacles, squads, contact logic, trench/digging behavior, trench cells/networks, unit summary UI, telemetry, grenade anti-stalemate pressure, and basic LOD/aggregation behavior.
- War-side prototype asset package exists and is imported/validated for editor Play Mode:
  - `16` war source sheets.
  - `16` war transparent sheets.
  - `356` war cutout PNGs.
  - `44` war multi-tile PNGs.
  - `16` terrain tiles.
  - `120` v2 unit transparent sheets.
  - `1,920` v2 unit animation frames.
  - V3 UI/interface packs: `4/4` packs, `64` labelled icons.
- Bottom/action UI controls now use V3 icon art with hover tooltips.

Partially working / prototype quality:

- The war AI is a prototype, not final strategy-game AI. It has team/squad authority concepts, field-map reasoning, contact/dig/hold behavior, support concepts, and diagnostics, but still needs live tuning.
- Trench growth is more structured than the earliest blob behavior, but still needs visual tilemap/gameplay integration and tuning against real playtest observations.
- Unit art exists as v2 directional/action sheets, but the battlefield runtime still relies heavily on IMGUI-style prototype drawing rather than fully animated sprite rendering.
- The UI is functional and now icon-backed, but the layout is still an OnGUI prototype, not a finished production UI.
- Unity import settings for war/terrain runtime PNGs are now handled by an editor script, but packaged-build asset loading is not solved.

Broken, blocked, or unverified:

- No final packaged build has been made.
- No post-icon-wiring live Play Mode visual review has been completed by the user.
- No sprite atlas/Addressables/Resources pipeline has been chosen.
- No permanent memory promotion has been done by this worker after the final decommission request.
- Unity batchmode logs show a licensing access-token refresh error, but both tested commands exited with return code `0`.

Exact Unity Hub/open/play instructions:

1. Open Unity Hub.
2. Add/open this project folder:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

3. Use Unity `6000.3.8f1`.
4. Open scene:

```text
Assets\Scenes\TrenchworksPrototype.unity
```

5. If Unity opens the wrong/sample scene, use:

```text
TWB Trenchworks > Open Prototype Scene
```

6. Press Play.
7. Expected visible result: top bar reads `TWB Trenchworks`, map renders, bottom rail appears, right-side tracker appears, tick counter advances unless paused.
8. Useful editor menu checks:

```text
TWB Trenchworks > Validate Prototype Entry Point
TWB Trenchworks > Run Simulation Smoke Test
TWB Trenchworks > Assets > Apply War Sprite Import Settings
TWB Trenchworks > Assets > Validate War Icon Pack
```

## 4. Tests/checks run

Unity/editor checks:

- Batchmode icon validation command:

```powershell
& 'C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Unity.exe' -batchmode -quit -projectPath 'C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks' -executeMethod TWB.Trenchworks.Editor.TrenchworksWarAssetImportSettings.ValidateWarIconPack -logFile 'C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unity-war-icon-pack-validation.log'
```

Result: passed. Log includes `TWB Trenchworks war icon validation passed: 4/4 packs, 64 labelled icons.` and return code `0`.

- Batchmode simulation smoke command:

```powershell
& 'C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Unity.exe' -batchmode -quit -projectPath 'C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks' -executeMethod TWB.Trenchworks.Editor.TrenchworksProjectSetup.RunSimulationSmokeTest -logFile 'C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unity-war-asset-integration-smoke.log'
```

Result: passed. Log includes `TWB Trenchworks smoke test passed. Resources: 216. Shipping areas: 3. Workers: 5/5. TOP stored/routed ammo: 2/2. Wave drill pulses/cycle/units/contacts/trenches/maxLeaderDistance: 16/4/192/0/219/14. integrated smoke passed=True, ready=True, rp=972, completed=6, teams=2, productionRp=2` and return code `0`.

Command-line/source checks:

- `git -C 'C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks' status --short` returned not-a-repository.
- V3 icon path source check: `53` references, `30` unique icon files, `0` missing.
- V3 folder check: `4/4` packs, `16` labelled cutouts each, manifests present.
- Runtime PNG `.meta` check: `432` war/terrain PNGs checked, `0` missing `.meta` files.
- Prior asset validation: `2,456` non-source war PNG outputs scanned, `0` bright-cyan residue files.

Play Mode checks:

- Live Play Mode was user-observed during prior iterations and visibly displayed the prototype.
- Latest icon-wired UI was not live-reviewed by the user after batchmode validation.

Checks not run:

- No packaged build check.
- No automated screenshot/canvas check after icon wiring.
- No performance profiling pass after final asset integration.

## 5. Files touched

Primary Unity project/code paths:

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\README.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scenes\TrenchworksPrototype.unity`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksWarAssetImportSettings.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\IntegratedPrototypeSystems.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Production\ProductionWorldSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Production\ProductionIntegrationFacade.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Production\ProductionScenarioFactory.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Production\ResearchProductionSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Production\ResearchProductionScenarioFactory.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Research\ResearchTreeFactory.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Research\ResearchIntegrationFacade.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Research\ResearchRuntimeState.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarIntegrationFacade.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamEntities.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamTypes.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamScenariosDiagnostics.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarUnlockEffects.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarUnlockSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\TrenchworksCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\ResearchCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Data\CatalogIntegrationContracts.cs`

Primary war/terrain asset directories touched:

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Sheets\Source\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Sheets\Transparent\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Sheets\Normalized64\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Cutouts\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\MultiTile\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Accepted\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Transparent\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Cutouts\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\Terrain\Tiles\`

Specific V3 icon pack directories:

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Cutouts\war-squad-button-icons-v1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Cutouts\war-command-order-icons-v1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Cutouts\war-supply-resource-icons-v1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Cutouts\war-research-icons-v1\`

Documentation and reports touched:

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-asset-output-index-v1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-asset-master-style-v1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-side-asset-completion-v1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-side-asset-completion-v2.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-side-asset-completion-v3.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-v2-clarity-kit-plan.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-v3-interface-logistics-kit-plan.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-asset-unity-integration-v1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-directional-batching-v2.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-sheets-v2-index.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-squad-button-icons-v1-key.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-command-order-icons-v1-key.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-supply-resource-icons-v1-key.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-research-icons-v1-key.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unity-war-icon-pack-validation.log`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unity-war-asset-integration-smoke.log`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-17-twb-trenchworks-war-v3-interface-logistics-assets-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-17-twb-trenchworks-war-asset-unity-integration-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-17-twb-trenchworks-worker-final-decommission-report.md`

Unity also generated/imported `.meta` files for war/terrain PNG assets during batchmode import.

## 6. Cleanup performed

- Removed `64` temporary anonymous V3 cleaner row cutouts after stable labelled cutouts and manifests were created.
- Preserved cyan source sheets for evidence and future regeneration review.
- Preserved generated Unity validation logs in `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\`:
  - `unity-war-icon-pack-validation.log`
  - `unity-war-asset-integration-smoke.log`
- Did not delete the old `prototype\My project` nested folder because the user had already destroyed/moved the old location and deletion was outside the final active project path.
- Did not remove Unity `Library`, `Logs`, generated `.meta` files, or source evidence.

Leftover artifacts Bob should know about:

- Codex generated-image originals remain under `C:\Users\yrred\.codex\generated_images\`.
- Source cyan sheets intentionally remain under `Assets\Art\War\Sheets\Source\`.
- Rejected/candidate unit sheets remain in the project where earlier asset work preserved evidence.
- Unity batchmode logs contain access-token refresh errors from licensing but successful return code `0`.

## 7. Risks

- This is not a git repository; there is no easy branch diff, commit, or rollback point unless Bob creates one externally.
- `SampleScene.unity` still exists. The editor setup should auto-open the prototype scene when appropriate, but workers should always verify `Assets\Scenes\TrenchworksPrototype.unity` before Play Mode testing.
- The old `prototype\My project` confusion must not be resurrected. The active project is `TWB-TrenchWorks`, not `prototype`.
- The UI icon loading in `PrototypeBootstrap` uses `Application.dataPath`, which is acceptable for editor Play Mode but not final packaged builds.
- War-side visuals are still partly IMGUI/prototype-rendered; do not assume the new asset sheets are fully wired into battlefield unit animation or tilemap rendering.
- Performance at scale still needs live profiling and likely renderer architecture work.
- AI behavior is improved but not final. The next worker should not assume the war loop is strategically complete just because the smoke test passes.
- Unity licensing token refresh errors appeared in batchmode logs; they did not block current checks but should be noted if future batchmode fails.
- Permanent memory was not updated during this decommission step; Bob must promote durable notes if desired.

## 8. Memory-worthy notes for Bob

- Durable fact: active Trenchworks Unity project is `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
- Durable fact: intended scene is `Assets\Scenes\TrenchworksPrototype.unity`.
- Durable fact: the old nested `prototype\My project` was an initial problem and is no longer the active project path.
- Durable fact: Play Mode now visibly runs the prototype when the correct project/scene is opened.
- Durable fact: war-side prototype asset package is complete for first-pass prototyping, not final game art.
- Durable fact: V3 UI/interface asset package has `4/4` packs and `64` labelled icons.
- Durable fact: Unity icon validation and simulation smoke both passed on 2026-05-17.
- Durable warning: the project is not currently under git in the active Unity folder.
- Durable warning: do not confuse prototype asset completeness with final runtime sprite/tilemap integration.
- Durable next gate: live Unity Play Mode visual review of the icon-wired UI, followed by a narrow battlefield asset-renderer integration pass.

## 9. Do-not-promote notes

- Do not promote any one-off AI weight/tuning value as final design.
- Do not promote early trench-visual experiments as the final trench art direction.
- Do not promote the current OnGUI icon-loading approach as the final packaged-build asset pipeline.
- Do not promote the current wave-drill numbers as final balance.
- Do not promote old `prototype\My project` details beyond the warning that the nested project caused confusion.
- Do not promote rejected/candidate sprite sheets as approved art unless separately reviewed.
- Do not promote this report's file-count snapshot as permanent truth after future asset passes; counts will change.

## 10. Recommended next worker brief

Recommended narrow recommissioning brief:

```text
You are the TWB Trenchworks Unity integration worker.

Scope: standalone Unity 2D Trenchworks prototype only.
Project: C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
Scene: Assets\Scenes\TrenchworksPrototype.unity

Read first:
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\twb-trenchworks\overview.md
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\twb-trenchworks\architecture.md
- C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-asset-output-index-v1.md
- C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-asset-unity-integration-v1.md
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-17-twb-trenchworks-worker-final-decommission-report.md

Task:
1. Open the active project and run a live Play Mode visual review.
2. Confirm the icon-wired bottom rail/action tray is readable at desktop scale.
3. Confirm the war map still visibly runs and has no new UI overlap.
4. Do not add new systems.
5. If Play Mode is clean, propose the next narrow pass: battlefield sprite/tile renderer integration for units, trenches, terrain, and combat FX.
6. If Play Mode is not clean, fix only the smallest UI/import issue.

Allowed write paths:
- C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
- C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term

Forbidden:
- Do not edit memory/wiki, memory/index.md, memory/hot.md, or memory/log.md.
- Do not touch main TWB Unity, Garden, Alchemy, Marketing, shared platform, or old prototype folders.
```

