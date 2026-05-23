# Prompts To Run In Order

## Purpose

Codex may perform better with smaller task batches.

Use the prompts in `codex_tasks/` in order.

## Recommended sequence

### Prompt 1

```text
codex_tasks/01_audit_and_foundation.md
```

Creates safe foundation.

### Prompt 2

```text
codex_tasks/02_generate_prototype_art_assets.md
```

Creates procedural art generator.

### Prompt 3

```text
codex_tasks/03_build_terrain_trench_system.md
```

Creates terrain/trench visual system.

### Prompt 4

```text
codex_tasks/04_build_props_weapons_units.md
```

Creates props, weapons, units, animations.

### Prompt 5

```text
codex_tasks/05_build_vfx_ui_vertical_slice.md
```

Creates VFX, UI, and vertical slice scene.

### Prompt 6

```text
codex_tasks/06_validation_polish_report.md
```

Validates, fixes, and reports.

## If Codex can handle one large task

Use:

```text
ONE_SHOT_CODEX_PROMPT.md
```

## If Codex gets stuck

Do not abandon the pipeline.

Reduce scope in this order:

1. keep folder structure
2. keep generator tool
3. keep terrain/trench assets
4. keep props/weapons
5. keep units
6. keep VFX/UI
7. keep scene

The trench + sandbags + weapons + helmeted units are the highest-value visual elements.
