# Unity Editor Art Generator

## Purpose

Create an editor tool that generates the first complete art pass.

## Required menu

Create an editor window or direct menu action:

```text
TWB/Art Pipeline/Generate Prototype Art
```

Optional supporting menu actions:

```text
TWB/Art Pipeline/Generate Art Only
TWB/Art Pipeline/Rebuild Prefabs Only
TWB/Art Pipeline/Rebuild Demo Scene
TWB/Art Pipeline/Open Implementation Report
```

## Core scripts

Create:

```text
Assets/TWB/Scripts/Editor/ArtPipeline/TwbPrototypeArtGeneratorWindow.cs
Assets/TWB/Scripts/Editor/ArtPipeline/TwbPrototypeArtGenerator.cs
Assets/TWB/Scripts/Editor/ArtPipeline/TwbTextureDrawUtility.cs
Assets/TWB/Scripts/Editor/ArtPipeline/TwbSpriteImportUtility.cs
```

## Responsibilities

### TwbPrototypeArtGeneratorWindow

- display buttons
- call generator methods
- show simple status
- explain that generated art is prototype art
- include regenerate warning for generated files only

### TwbPrototypeArtGenerator

- create folders
- generate texture assets
- call import utility
- call prefab builder
- call demo scene builder
- write reports

### TwbTextureDrawUtility

Provide drawing helpers:

- create transparent texture
- create opaque texture
- fill rect
- fill circle/ellipse
- fill rounded rect
- draw line with thickness
- draw capsule
- draw polygon
- draw soft shadow ellipse
- add noise/speckle
- add scratch marks
- save PNG
- optional downsample

### TwbSpriteImportUtility

Configure import settings:

- texture type: Sprite
- sprite mode: Single or Multiple
- pixels per unit: consistent
- compression: none or high quality
- filter mode: bilinear
- wrap mode: clamp for sprites, repeat only for material-like textures
- alpha is transparency: true for transparent assets
- set sprite pivots
- slice sheets where needed

## Important Unity note

For sprite sheet slicing, use Unity APIs compatible with the installed Unity version.

If direct `TextureImporter.spritesheet` is obsolete in the project version, use `UnityEditor.U2D.Sprites.SpriteDataProviderFactories` and related sprite editor data providers if available.

If slicing is risky, create sheets but also create individual frame PNGs as fallback.

## Recommended fallback

Generate individual frame files for animated assets first.

Example:

```text
Assets/TWB/Art/Generated/Units/Rifleman/
  unit_rifleman_down_idle_00_v001.png
  unit_rifleman_down_idle_01_v001.png
  unit_rifleman_down_move_00_v001.png
  ...
```

Then optionally generate sheets.

This avoids Unity-version sprite slicing issues.

## Output files

The generator should create these art files at minimum:

### Terrain

```text
Assets/TWB/Art/Generated/Terrain/terrain_ground_temperate_v001.png
Assets/TWB/Art/Generated/Terrain/terrain_mud_temperate_v001.png
Assets/TWB/Art/Generated/Terrain/terrain_trench_floor_v001.png
Assets/TWB/Art/Generated/Terrain/terrain_trench_edge_h_v001.png
Assets/TWB/Art/Generated/Terrain/terrain_trench_edge_v_v001.png
Assets/TWB/Art/Generated/Terrain/terrain_sandbag_strip_h_v001.png
Assets/TWB/Art/Generated/Terrain/terrain_sandbag_strip_v_v001.png
Assets/TWB/Art/Generated/Terrain/terrain_sandbag_corner_ne_v001.png
Assets/TWB/Art/Generated/Terrain/terrain_crater_small_v001.png
Assets/TWB/Art/Generated/Terrain/terrain_crater_medium_v001.png
```

### Props

```text
Assets/TWB/Art/Generated/Props/prop_ammo_crate_v001.png
Assets/TWB/Art/Generated/Props/prop_supply_crate_v001.png
Assets/TWB/Art/Generated/Props/prop_fuel_drum_v001.png
Assets/TWB/Art/Generated/Props/prop_barrel_v001.png
Assets/TWB/Art/Generated/Props/prop_plank_bundle_v001.png
Assets/TWB/Art/Generated/Props/prop_sandbag_pile_v001.png
Assets/TWB/Art/Generated/Props/prop_wire_spool_v001.png
Assets/TWB/Art/Generated/Props/prop_shell_box_v001.png
```

### Weapons

```text
Assets/TWB/Art/Generated/Weapons/weapon_mg_idle_v001.png
Assets/TWB/Art/Generated/Weapons/weapon_mg_fire_00_v001.png
Assets/TWB/Art/Generated/Weapons/weapon_mg_fire_01_v001.png
Assets/TWB/Art/Generated/Weapons/weapon_mortar_idle_v001.png
Assets/TWB/Art/Generated/Weapons/weapon_mortar_fire_00_v001.png
Assets/TWB/Art/Generated/Weapons/weapon_mortar_fire_01_v001.png
```

### Units

Generate separate frames for:

- rifleman
- engineer
- support gunner
- truck
- tank

At minimum:

```text
unit_[type]_[direction]_[state]_[frame]_v001.png
```

Directions:

```text
down
up
left
right
```

States:

```text
idle
move
fire
```

### VFX

```text
vfx_muzzle_flash_rifle_00_v001.png
vfx_muzzle_flash_mg_00_v001.png
vfx_mortar_puff_00_v001.png
vfx_dirt_impact_00_v001.png
vfx_explosion_small_00_v001.png
vfx_smoke_loop_00_v001.png
vfx_fire_loop_00_v001.png
vfx_dust_puff_00_v001.png
```

### UI

```text
ui_selection_ring_v001.png
ui_move_marker_v001.png
ui_attack_marker_v001.png
ui_build_ghost_v001.png
ui_icon_rifleman_v001.png
ui_icon_engineer_v001.png
ui_icon_mg_v001.png
ui_icon_mortar_v001.png
ui_icon_ammo_v001.png
ui_icon_fuel_v001.png
ui_icon_supplies_v001.png
ui_icon_trench_v001.png
ui_icon_factory_v001.png
```

## Generation quality

The procedural art must include:

- soft contact shadows
- simple top-left highlight
- muted palette
- clear silhouette
- subtle noise or scuffs
- consistent scale

Do not produce flat single-color rectangles unless used only as a temporary debug fallback.

## Report requirement

After generation, write:

```text
Assets/TWB/Docs/ART_PIPELINE_GENERATED_ASSETS.md
```

Include:

- generated date/time
- generator script version
- all output paths
- known limitations
- how to regenerate
