# One-Shot Codex Prompt

Read every markdown file in this package before editing the project.

You are implementing a complete prototype art direction and art pipeline for a Unity top-down / 2.5D tactical trench war game.

The user has no art skills and needs Codex to create a usable, complete-looking prototype.

## Hard requirements

- Do not delete existing game code.
- Do not break existing scenes.
- Do not require the user to manually draw art.
- Do not depend on unavailable external art.
- Use procedural Unity-generated placeholder art where needed.
- Make the art system consistent and replaceable later.
- Create a complete vertical slice scene that shows the visual direction.
- Prefer simple readable game art over ambitious inconsistent art.
- Commit to the art direction: stylized top-down 2.5D tactical miniature war game.

## What to implement

Implement the full Stage 0 through Stage 5 package from:

- `docs/codex_implementation/00_MASTER_CODEX_TASK.md`
- `docs/codex_implementation/04_UNITY_EDITOR_ART_GENERATOR.md`
- `docs/codex_implementation/05_TERRAIN_TRENCH_GENERATOR.md`
- `docs/codex_implementation/06_PROP_WEAPON_PREFABS.md`
- `docs/codex_implementation/07_UNIT_ANIMATION_SYSTEM.md`
- `docs/codex_implementation/08_VFX_SYSTEM.md`
- `docs/codex_implementation/09_UI_ICONS_AND_OVERLAYS.md`
- `docs/codex_implementation/10_VERTICAL_SLICE_SCENE.md`
- `docs/codex_implementation/11_VALIDATION_AND_ACCEPTANCE.md`

## Minimum files/scripts to create

Create the exact structure and script set described in the implementation docs unless the project already has better equivalents.

At minimum, create:

```text
Assets/TWB/Scripts/Editor/ArtPipeline/TwbPrototypeArtGeneratorWindow.cs
Assets/TWB/Scripts/Editor/ArtPipeline/TwbPrototypeArtGenerator.cs
Assets/TWB/Scripts/Editor/ArtPipeline/TwbSpriteImportUtility.cs
Assets/TWB/Scripts/Editor/ArtPipeline/TwbPrefabBuilder.cs
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

If names need small changes to match existing project conventions, keep the `Twb` prefix and document the change.

## Minimum generated assets

Generate prototype assets for:

- ground
- trench floor
- trench walls
- sandbag straight/corner/cap pieces
- craters
- mud/debris decals
- crates
- barrels
- planks
- ammo
- machine gun emplacement
- mortar emplacement
- rifleman
- engineer
- support gunner
- supply truck
- tank or armored support
- muzzle flashes
- smoke
- dirt impacts
- explosions
- UI icons
- selection ring
- build ghost marker

## Minimum demo scene

Create:

```text
Assets/TWB/Scenes/TWB_ArtPipeline_VerticalSlice.unity
```

The scene must show:

- a terrain base
- a trench network
- sandbag walls
- at least one MG emplacement
- at least one mortar emplacement
- crates/debris/planks
- small helmeted units
- a vehicle
- VFX examples
- UI selection/build markers
- a small factory/logistics area

## Done means

- Unity compiles.
- Menu item exists to generate/regenerate prototype art.
- Generated assets are visible in the Project window.
- Prefabs are created.
- Demo scene opens.
- The scene is readable and complete-looking.
- A final report explains what was built and how to regenerate it.
