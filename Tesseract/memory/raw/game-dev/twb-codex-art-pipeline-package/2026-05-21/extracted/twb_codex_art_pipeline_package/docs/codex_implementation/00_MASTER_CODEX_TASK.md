# Master Codex Task

## Task summary

Implement a Unity art pipeline and complete prototype art pass for a top-down / 2.5D tactical trench war game.

The game should no longer look like a raw prototype.
It should look like a complete, basic, readable tactical war game.

## Do not wait for external art

Codex must generate the first usable art pass using code.

Use Unity Editor scripts to procedurally generate PNG textures and sprite sheets.

If the environment supports image generation or existing art sources, Codex may use them, but the project must not depend on them.

## Required Unity features

Create a menu item:

```text
TWB/Art Pipeline/Generate Prototype Art
```

When clicked, it should:

1. create folders
2. generate art PNGs
3. import sprites
4. slice sprite sheets
5. create prefabs
6. create animation clips where needed
7. create the demo scene
8. write the implementation report

Also create:

```text
TWB/Art Pipeline/Rebuild Demo Scene
TWB/Art Pipeline/Open Implementation Report
```

The exact menu names can vary slightly, but the functions must be discoverable.

## Required created files

At minimum, create these files unless existing project conventions require small adjustments:

```text
Assets/TWB/Scripts/Editor/ArtPipeline/TwbPrototypeArtGeneratorWindow.cs
Assets/TWB/Scripts/Editor/ArtPipeline/TwbPrototypeArtGenerator.cs
Assets/TWB/Scripts/Editor/ArtPipeline/TwbSpriteImportUtility.cs
Assets/TWB/Scripts/Editor/ArtPipeline/TwbTextureDrawUtility.cs
Assets/TWB/Scripts/Editor/ArtPipeline/TwbPrefabBuilder.cs
Assets/TWB/Scripts/Editor/ArtPipeline/TwbAnimationBuilder.cs
Assets/TWB/Scripts/Editor/ArtPipeline/TwbDemoSceneBuilder.cs

Assets/TWB/Scripts/Runtime/Art/TwbSimpleSpriteAnimator.cs
Assets/TWB/Scripts/Runtime/Art/TwbBillboardFreeTopDownSorter.cs
Assets/TWB/Scripts/Runtime/VFX/TwbOneShotVfx.cs
Assets/TWB/Scripts/Runtime/VFX/TwbLoopingVfx.cs
Assets/TWB/Scripts/Runtime/Units/TwbPrototypeUnitMotor.cs
Assets/TWB/Scripts/Runtime/Weapons/TwbPrototypeWeaponAnimator.cs
Assets/TWB/Scripts/Runtime/UI/TwbPrototypeSelectionRing.cs

Assets/TWB/Docs/ART_PIPELINE_IMPLEMENTATION_REPORT.md
```

If the existing project already has a stronger equivalent, use it but document the reason.

## Required generated art families

Create PNGs or sprite sheets for:

### Terrain

- ground base tile
- mud tile
- trench floor tile
- trench edge pieces
- sandbag strips
- sandbag corners
- craters
- mud decals
- planks/duckboards
- debris

### Props

- ammo crate
- supply crate
- fuel drum
- barrel
- sandbag pile
- wire spool
- plank bundle
- shell box
- industrial storage bin
- pallet stack

### Weapons

- machine gun emplacement
- mortar emplacement
- simple bunker/firing slit

### Units

- rifleman
- engineer
- support gunner
- supply truck
- tank or armored support

### VFX

- rifle muzzle flash
- MG muzzle flash
- mortar launch puff
- dirt impact
- small explosion
- smoke loop
- fire loop
- vehicle dust puff

### UI

- selection ring
- move marker
- attack marker
- build ghost marker
- icons for rifleman, engineer, MG, mortar, truck, tank, ammo, fuel, supplies, trench, factory, repair

## Required demo scene

Create:

```text
Assets/TWB/Scenes/TWB_ArtPipeline_VerticalSlice.unity
```

Scene must contain:

- camera
- light if the project uses 2D/3D lights
- terrain base
- trench path
- sandbag walls
- MG position
- mortar position
- scattered props
- at least three infantry units
- one truck
- one tank or armored support
- one small factory/logistics area
- VFX showcase objects
- UI/marker showcase objects

## Sorting and readability

Use sorting layers or explicit `sortingOrder` values.

Recommended order:

```text
TerrainBase: 0
TerrainOverlay: 10
Decals: 20
TrenchFloor: 30
TrenchWall: 40
Props: 50
Units: 60
Weapons: 65
VFX: 80
UIWorld: 100
```

Create sorting layers if safe.
If not safe, use `SpriteRenderer.sortingOrder`.

## Done criteria

The task is done when:

- Unity compiles
- generated assets appear in the project
- prefabs are created
- demo scene opens
- scene is visibly readable
- no manual art drawing is required
- final report exists
- report lists all generated files and known limitations
