# Folder Structure and Naming Implementation

## Goal

Create a clean project structure for all generated art and pipeline scripts.

## Required folder creation

Codex should create these folders:

```text
Assets/TWB/
Assets/TWB/Art/
Assets/TWB/Art/Source/
Assets/TWB/Art/Source/Materials/
Assets/TWB/Art/Source/Masks/
Assets/TWB/Art/Source/Props/
Assets/TWB/Art/Source/Units/
Assets/TWB/Art/Source/VFX/
Assets/TWB/Art/Source/UI/
Assets/TWB/Art/Source/Buildings/
Assets/TWB/Art/Source/Decals/

Assets/TWB/Art/Generated/
Assets/TWB/Art/Generated/Materials/
Assets/TWB/Art/Generated/Terrain/
Assets/TWB/Art/Generated/Props/
Assets/TWB/Art/Generated/Weapons/
Assets/TWB/Art/Generated/Units/
Assets/TWB/Art/Generated/VFX/
Assets/TWB/Art/Generated/UI/
Assets/TWB/Art/Generated/Buildings/
Assets/TWB/Art/Generated/Decals/

Assets/TWB/Art/Processed/
Assets/TWB/Art/Atlases/

Assets/TWB/Prefabs/
Assets/TWB/Prefabs/Terrain/
Assets/TWB/Prefabs/Props/
Assets/TWB/Prefabs/Weapons/
Assets/TWB/Prefabs/Units/
Assets/TWB/Prefabs/VFX/
Assets/TWB/Prefabs/UI/
Assets/TWB/Prefabs/Buildings/

Assets/TWB/Scenes/
Assets/TWB/Scripts/
Assets/TWB/Scripts/Editor/
Assets/TWB/Scripts/Editor/ArtPipeline/
Assets/TWB/Scripts/Runtime/
Assets/TWB/Scripts/Runtime/Art/
Assets/TWB/Scripts/Runtime/VFX/
Assets/TWB/Scripts/Runtime/Units/
Assets/TWB/Scripts/Runtime/Weapons/
Assets/TWB/Scripts/Runtime/UI/

Assets/TWB/Docs/
```

## Naming conventions

### Art files

Use lowercase snake_case:

```text
terrain_ground_temperate_v001.png
terrain_trench_floor_v001.png
terrain_sandbag_strip_h_v001.png
prop_ammo_crate_v001.png
weapon_mg_emplacement_sheet_v001.png
unit_rifleman_sheet_v001.png
vfx_muzzle_flash_mg_sheet_v001.png
ui_icon_ammo_v001.png
```

### Prefabs

Use PascalCase:

```text
TWB_Terrain_Ground.prefab
TWB_Prop_AmmoCrate.prefab
TWB_Weapon_MGEmplacement.prefab
TWB_Unit_Rifleman.prefab
TWB_VFX_MGMuzzleFlash.prefab
TWB_UI_SelectionRing.prefab
```

### Scripts

Use PascalCase and `Twb` prefix:

```text
TwbPrototypeArtGenerator.cs
TwbSpriteImportUtility.cs
TwbDemoSceneBuilder.cs
```

## Versioning rule

Generated art can be regenerated in-place if the report clearly states it is generated.

Source art should use version suffixes and should not be overwritten silently.

## Metadata file

Create a simple generated metadata file:

```text
Assets/TWB/Docs/ART_PIPELINE_GENERATED_ASSETS.md
```

It should list:

- asset path
- asset type
- whether it is generated
- intended usage
- known limitations
