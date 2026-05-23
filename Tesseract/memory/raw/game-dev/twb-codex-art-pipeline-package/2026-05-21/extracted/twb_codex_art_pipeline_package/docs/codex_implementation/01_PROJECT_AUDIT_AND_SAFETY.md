# Project Audit and Safety Rules

## Purpose

Before changing the project, Codex must understand what exists and avoid breaking it.

## Audit checklist

Codex must inspect:

- Unity version
- render pipeline
- folder structure
- existing scenes
- existing art folders
- existing gameplay scripts
- existing unit/terrain systems
- existing tilemap systems
- existing sorting layers
- existing input/UI systems
- existing package dependencies

## Do not assume

Do not assume the project uses:

- URP
- 2D Renderer
- Tilemap
- Addressables
- Sprite Atlas package
- Cinemachine
- Input System
- TextMeshPro
- any specific architecture

Use what exists when possible.

## Non-destructive rules

- Do not delete existing files.
- Do not rename existing files unless absolutely necessary.
- Do not move existing project code.
- Do not overwrite existing scenes.
- Do not change render pipeline assets unless the project already uses them and the change is safe.
- Do not change Project Settings broadly unless documented and necessary.

## Safe namespace

Put new scripts under a clear namespace if the project uses namespaces.

Recommended:

```csharp
namespace TWB.ArtPipeline
```

Runtime scripts may use:

```csharp
namespace TWB.Runtime.Art
namespace TWB.Runtime.VFX
namespace TWB.Runtime.Units
namespace TWB.Runtime.Weapons
namespace TWB.Runtime.UI
```

If project namespaces already exist, align with them.

## Conflict handling

If a file already exists:

1. inspect it
2. determine whether it is part of this pipeline
3. update it only if safe
4. otherwise create a new file with a clear name
5. document the decision in the report

## Scene safety

Do not modify existing gameplay scenes unless requested.

Create a new test scene:

```text
Assets/TWB/Scenes/TWB_ArtPipeline_VerticalSlice.unity
```

If there is already a scene with this name, create a backup or versioned scene first.

## Package safety

Do not add paid packages.
Do not assume external assets are installed.
Do not rely on asset store content.

If extra packages are useful, write them as optional notes in the report, but keep the core system working without them.

## Compile safety

Make incremental changes and ensure each major script compiles before adding more.

If Unity APIs differ by version, use stable APIs:

- `AssetDatabase`
- `TextureImporter`
- `SpriteRenderer`
- `GameObject`
- `PrefabUtility`
- `AnimationClip`
- `SceneManager`
- `EditorSceneManager`

Avoid fragile reflection-heavy systems unless needed.
