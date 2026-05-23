# File Structure and Export Rules

## Purpose

This document defines how art files should be organized, named, and exported.

Without this, the art pipeline will become unusable.

## 1. Root structure

Recommended Unity structure:

```text
Assets/
  TWB/
    Art/
      Source/
        Materials/
        Masks/
        Props/
        Units/
        VFX/
        UI/
        Buildings/
        Decals/
      Generated/
        Materials/
        Terrain/
        Props/
        Weapons/
        Units/
        VFX/
        UI/
        Buildings/
        Decals/
      Processed/
        Terrain/
        Props/
        Units/
        VFX/
        UI/
        Buildings/
      Atlases/
    Prefabs/
      Terrain/
      Props/
      Weapons/
      Units/
      VFX/
      UI/
      Buildings/
    Scenes/
    Scripts/
      Editor/
      Runtime/
    Docs/
```

## 2. Source vs generated vs processed

### Source

Original generated or externally produced image sources.

### Generated

Codex/Unity-generated art assets that are immediately usable.

### Processed

Cleaned, sliced, assembled, import-ready game art.

Never mix them.

## 3. Naming rules

Use lowercase snake_case for art assets.

### Examples

- `biome_temperate_material_sheet_v001.png`
- `trench_mask_straight_h_v001.png`
- `trench_shadow_corner_outer_v001.png`
- `sandbag_strip_straight_h_v001.png`
- `prop_ammo_crate_small_a_v001.png`
- `unit_rifleman_sheet_v001.png`
- `vfx_muzzle_flash_mg_v001.png`
- `ui_icon_ammo_v001.png`

C# classes should use normal PascalCase with `Twb` prefix.

## 4. Required prefixes

### Materials

- `biome_`
- `terrain_`

### Masks

- `trench_mask_`
- `trench_line_`
- `trench_shadow_`

### Props

- `prop_`

### Units

- `unit_`

### Effects

- `vfx_`

### UI

- `ui_`

### Buildings

- `building_`

### Decals

- `decal_`

This makes sorting and automation easier.

## 5. Versioning

Every source file should use a version suffix.

### Example

- `_v001`
- `_v002`
- `_v003`

Do not overwrite old outputs silently unless the file is explicitly generated and documented as regeneratable.

## 6. Sprite sheet rules

When exporting sprite sheets:

- consistent frame size
- consistent anchor point
- consistent padding
- transparent background
- row/column layout clearly defined

Document slicing assumptions for each sheet.

## 7. Pivot / anchor rules

### Infantry

- pivot near feet / center contact point

### Vehicles

- center or footprint center

### Emplacements

- center of base

### Props

- logical placement center

### Effects

- center or emission origin depending on usage

These rules should be documented and consistent.

## 8. Import rules

Codex should define Unity import rules for:

- Pixels Per Unit
- compression
- sprite mode
- mesh type if relevant
- filter mode
- pivot
- packing tag / atlas group

The exact values can be project-specific, but they must be standardized.

Recommended defaults:

- terrain tile sprites: 128 PPU if 128 px = 1 tile
- small props: 128 PPU
- unit sheets: 128 PPU
- VFX: 128 PPU
- filter mode: bilinear for soft non-pixel art, point only if intentionally pixel art
- compression: none or high-quality for prototype art clarity
- mesh type: full rect for simple reliable slicing
- sprite mode: multiple for sheets, single for isolated assets

## 9. Color and alpha rules

### Alpha

Use clean alpha for extracted assets.

### Matte extraction

If a matte background is used, it must be easy to isolate and documented.

### Color consistency

Do not allow random palette drift from asset to asset.
Use reference sets from the approved style direction.

## 10. Documentation requirement

Every major asset family should have:

- purpose
- input source
- output format
- slice rules
- intended usage

If an artist pipeline step is not documented, it will not scale.

## 11. Export standard

Each deliverable should specify:

- file name
- dimensions
- transparency or opaque
- sprite sheet or isolated asset
- expected import settings
- downstream usage

This is required for Codex to automate properly.
