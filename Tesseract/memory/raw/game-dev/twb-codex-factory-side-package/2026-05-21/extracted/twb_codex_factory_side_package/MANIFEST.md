# Manifest

## Package name

`twb_codex_factory_side_package`

## Purpose

This package defines the factory/logistics half of the game.
It is designed to work alongside the trench battlefield art pipeline package.

The package is self-contained, but it assumes the game direction is:

- top-down / 2.5D tactical war logistics game
- Unity project
- Codex-only production
- no human artist dependency
- procedural/modular generated art
- first priority: a complete playable prototype

---

## Folder contents

### Root files

- `CODEX_START_HERE.md` — first file to read
- `MANIFEST.md` — package structure
- `ONE_SHOT_CODEX_PROMPT.md` — one large prompt for Codex

### Codex task prompts

- `codex_tasks/01_audit_and_foundation.md`
- `codex_tasks/02_factory_art_generator.md`
- `codex_tasks/03_grid_floor_and_placement.md`
- `codex_tasks/04_belts_pipes_and_items.md`
- `codex_tasks/05_machines_recipes_and_power.md`
- `codex_tasks/06_ui_vfx_and_feedback.md`
- `codex_tasks/07_factory_vertical_slice.md`
- `codex_tasks/08_validation_polish_report.md`

### Factory art/pipeline docs

- `docs/factory_pipeline/README.md`
- `docs/factory_pipeline/01_FACTORY_ART_DIRECTION_BIBLE.md`
- `docs/factory_pipeline/02_FACTORY_PIPELINE_RULES.md`
- `docs/factory_pipeline/03_GRID_FLOORS_AND_TERRAIN.md`
- `docs/factory_pipeline/04_BELTS_INSERTERS_AND_PIPES.md`
- `docs/factory_pipeline/05_MACHINES_AND_BUILDINGS.md`
- `docs/factory_pipeline/06_ITEMS_RESOURCES_AND_CONTAINERS.md`
- `docs/factory_pipeline/07_POWER_FLUIDS_AND_OVERLAYS.md`
- `docs/factory_pipeline/08_FACTORY_ANIMATION_AND_VFX.md`
- `docs/factory_pipeline/09_FACTORY_UI_AND_FEEDBACK.md`
- `docs/factory_pipeline/10_FILE_STRUCTURE_AND_EXPORT.md`
- `docs/factory_pipeline/11_FACTORY_CODEX_WORK_ORDER.md`
- `docs/factory_pipeline/12_FACTORY_ASSET_CATALOG.md`
- `docs/factory_pipeline/13_IMAGE_GENERATION_BRIEF_TEMPLATES.md`
- `docs/factory_pipeline/14_GAMEPLAY_INTEGRATION_RULES.md`
- `docs/factory_pipeline/15_TRENCH_FACTORY_BRIDGE.md`

### Codex implementation docs

- `docs/codex_implementation/README.md`
- `docs/codex_implementation/00_MASTER_CODEX_TASK.md`
- `docs/codex_implementation/01_PROJECT_AUDIT_AND_SAFETY.md`
- `docs/codex_implementation/02_FOLDER_STRUCTURE_AND_NAMING.md`
- `docs/codex_implementation/03_GENERATED_FACTORY_ART_SPEC.md`
- `docs/codex_implementation/04_UNITY_EDITOR_FACTORY_ART_GENERATOR.md`
- `docs/codex_implementation/05_GRID_PLACEMENT_AND_TILE_PREVIEW_SYSTEM.md`
- `docs/codex_implementation/06_CONVEYOR_BELT_AND_PIPE_SYSTEM.md`
- `docs/codex_implementation/07_MACHINE_PREFABS_AND_RECIPE_VISUALS.md`
- `docs/codex_implementation/08_ITEM_ICONS_AND_RESOURCE_ART.md`
- `docs/codex_implementation/09_POWER_FLUIDS_AND_STATUS_OVERLAYS.md`
- `docs/codex_implementation/10_ANIMATION_AND_VFX_SYSTEM.md`
- `docs/codex_implementation/11_FACTORY_VERTICAL_SLICE_SCENE.md`
- `docs/codex_implementation/12_VALIDATION_AND_ACCEPTANCE.md`
- `docs/codex_implementation/13_PROMPTS_TO_RUN_IN_ORDER.md`
- `docs/codex_implementation/14_DONE_DEFINITION.md`
- `docs/codex_implementation/15_VISUAL_RECIPE_DETAILS.md`

---

## Implementation rule

Codex should not merely create documents.
Codex should implement the factory side inside the Unity project where possible.

The documents are the instruction set.
The output should be usable game systems, generated prototype art, prefabs, data, and a playable vertical slice.
