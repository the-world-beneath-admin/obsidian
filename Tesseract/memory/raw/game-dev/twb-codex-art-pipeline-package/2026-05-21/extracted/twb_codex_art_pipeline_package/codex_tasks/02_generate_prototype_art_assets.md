# Codex Task 02 — Generate Prototype Art Assets

Read:

- `docs/art_pipeline/03_TERRAIN_AND_TRENCHES.md`
- `docs/art_pipeline/04_PROPS_AND_WEAPONS.md`
- `docs/art_pipeline/05_UNITS_AND_ANIMATION.md`
- `docs/art_pipeline/06_VFX_AND_PARTICLES.md`
- `docs/art_pipeline/07_UI_AND_ICON_STYLE.md`
- `docs/art_pipeline/10_ASSET_CATALOG.md`
- `docs/codex_implementation/03_GENERATED_ART_SPEC.md`
- `docs/codex_implementation/04_UNITY_EDITOR_ART_GENERATOR.md`

## Task

Implement the procedural art generator that creates the first usable complete art pass.

## Requirements

Create or complete:

```text
Assets/TWB/Scripts/Editor/ArtPipeline/TwbPrototypeArtGenerator.cs
Assets/TWB/Scripts/Editor/ArtPipeline/TwbTextureDrawUtility.cs
Assets/TWB/Scripts/Editor/ArtPipeline/TwbSpriteImportUtility.cs
```

Generate PNG assets for:

- terrain
- trenches
- sandbags
- craters
- decals
- props
- weapons
- units
- vehicles
- VFX
- UI icons/markers

## Art standard

Assets must be:

- readable
- muted battlefield palette
- top-down
- simple 2.5D shading
- transparent where needed
- not just debug blocks

## Technical standard

- Use consistent pixels-per-unit.
- Import all PNGs as sprites.
- Avoid fragile package dependencies.
- Generate individual animation frames if sprite-sheet slicing is risky.
- Write generated asset paths into `Assets/TWB/Docs/ART_PIPELINE_GENERATED_ASSETS.md`.

## Done when

- generated PNGs exist under `Assets/TWB/Art/Generated/`
- assets import as sprites
- generator can be rerun
- reports list the outputs
