# Codex Task 05 — Build VFX, UI, and Vertical Slice

Read:

- `docs/art_pipeline/06_VFX_AND_PARTICLES.md`
- `docs/art_pipeline/07_UI_AND_ICON_STYLE.md`
- `docs/codex_implementation/08_VFX_SYSTEM.md`
- `docs/codex_implementation/09_UI_ICONS_AND_OVERLAYS.md`
- `docs/codex_implementation/10_VERTICAL_SLICE_SCENE.md`

## Task

Create VFX prefabs, UI/world overlay prefabs, and the vertical slice scene.

## Requirements

Create VFX scripts:

```text
Assets/TWB/Scripts/Runtime/VFX/TwbOneShotVfx.cs
Assets/TWB/Scripts/Runtime/VFX/TwbLoopingVfx.cs
```

Create UI script:

```text
Assets/TWB/Scripts/Runtime/UI/TwbPrototypeSelectionRing.cs
```

Create scene builder:

```text
Assets/TWB/Scripts/Editor/ArtPipeline/TwbDemoSceneBuilder.cs
```

Create scene:

```text
Assets/TWB/Scenes/TWB_ArtPipeline_VerticalSlice.unity
```

Scene must include:

- battlefield terrain
- trench network
- sandbag walls
- MG
- mortar
- props
- units
- truck
- tank
- logistics/factory area
- VFX examples
- UI/world markers

## Done when

- scene opens
- scene looks like a basic complete game
- VFX animate
- units animate or move
- selection ring/markers are visible
