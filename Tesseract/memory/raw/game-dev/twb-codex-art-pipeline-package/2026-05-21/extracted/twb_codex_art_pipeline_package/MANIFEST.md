# Package Manifest

## Root files

- `CODEX_START_HERE.md`  
  Main entry point for Codex.

- `MANIFEST.md`  
  This file.

- `ONE_SHOT_CODEX_PROMPT.md`  
  Single prompt to paste into Codex if you want Codex to attempt the whole package in one run.

## Art pipeline documents

Located in `docs/art_pipeline/`.

These define the art direction, visual rules, asset categories, and source-generation strategy.

Recommended read order:

1. `README.md`
2. `01_ART_DIRECTION_BIBLE.md`
3. `02_PIPELINE_RULES.md`
4. `03_TERRAIN_AND_TRENCHES.md`
5. `04_PROPS_AND_WEAPONS.md`
6. `05_UNITS_AND_ANIMATION.md`
7. `06_VFX_AND_PARTICLES.md`
8. `07_UI_AND_ICON_STYLE.md`
9. `08_FILE_STRUCTURE_AND_EXPORT.md`
10. `09_CODEX_WORK_ORDER.md`
11. `10_ASSET_CATALOG.md`
12. `11_IMAGE_GENERATION_BRIEF_TEMPLATES.md`

## Codex implementation documents

Located in `docs/codex_implementation/`.

These tell Codex what to actually build in Unity.

Recommended read order:

1. `README.md`
2. `00_MASTER_CODEX_TASK.md`
3. `01_PROJECT_AUDIT_AND_SAFETY.md`
4. `02_FOLDER_STRUCTURE_AND_NAMING.md`
5. `03_GENERATED_ART_SPEC.md`
6. `04_UNITY_EDITOR_ART_GENERATOR.md`
7. `05_TERRAIN_TRENCH_GENERATOR.md`
8. `06_PROP_WEAPON_PREFABS.md`
9. `07_UNIT_ANIMATION_SYSTEM.md`
10. `08_VFX_SYSTEM.md`
11. `09_UI_ICONS_AND_OVERLAYS.md`
12. `10_VERTICAL_SLICE_SCENE.md`
13. `11_VALIDATION_AND_ACCEPTANCE.md`
14. `12_PROMPTS_TO_RUN_IN_ORDER.md`
15. `13_DONE_DEFINITION.md`
16. `14_VISUAL_RECIPE_DETAILS.md`

## Codex task prompts

Located in `codex_tasks/`.

Run these in order if Codex performs better with smaller task batches.

1. `01_audit_and_foundation.md`
2. `02_generate_prototype_art_assets.md`
3. `03_build_terrain_trench_system.md`
4. `04_build_props_weapons_units.md`
5. `05_build_vfx_ui_vertical_slice.md`
6. `06_validation_polish_report.md`

## Expected final Unity outputs

Codex should create or update:

```text
Assets/
  TWB/
    Art/
      Source/
      Generated/
      Processed/
      Atlases/
    Prefabs/
      Terrain/
      Props/
      Weapons/
      Units/
      VFX/
      UI/
    Scenes/
    Scripts/
      Editor/
      Runtime/
    Docs/
```

Codex should also create a final implementation report inside:

```text
Assets/TWB/Docs/ART_PIPELINE_IMPLEMENTATION_REPORT.md
```
