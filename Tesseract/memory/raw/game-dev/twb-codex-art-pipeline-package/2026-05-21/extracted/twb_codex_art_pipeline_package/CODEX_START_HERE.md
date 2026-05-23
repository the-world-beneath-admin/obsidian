# TWB Codex Art Pipeline Package
## Start Here

You are helping build a complete, usable, top-down / 2.5D tactical war game art pipeline in Unity.

The user has no art skills and is relying on Codex to make the game look complete enough to ship a prototype.  
The goal is **not perfect art**. The goal is **consistent, readable, complete-looking game art**.

## What to do first

1. Read this file.
2. Read `MANIFEST.md`.
3. Read all files in `docs/art_pipeline/`.
4. Read all files in `docs/codex_implementation/`.
5. Then use the task prompts in `codex_tasks/` in order.

## Most important rule

Do not build a pile of random images.

Build a **repeatable art system** for Unity:

- generated source assets
- generated masks
- generated 2.5D tactical sprites
- Unity import automation
- prefabs
- animation clips
- VFX
- UI icons
- one complete visual test scene

## Core visual choice

Use:

**stylized top-down 2.5D tactical miniature graphics built from procedural materials, masks, decals, modular props, small unit sprites, and particle effects.**

Avoid:

- complex realistic soldiers
- large one-off AI images
- photorealistic textures
- fragile hand-drawn tile art
- huge animation sets
- assets that require a human artist to fix them

## Minimum visual target

The game should be readable and complete-looking:

- a trench should obviously look like a trench
- sandbags should obviously look like sandbags
- a machine gun should clearly look like a machine gun
- a mortar should clearly look like a mortar
- infantry can be small helmeted bodies with guns
- effects should make combat feel alive
- factory/logistics assets should look functional and consistent

## Implementation priority

If existing game systems are present, integrate non-destructively.

If the project does not yet have enough gameplay systems, create a standalone visual vertical slice scene that proves the art pipeline works.

## Never do this

- Do not delete existing gameplay code.
- Do not replace the render pipeline without confirming the project already supports it.
- Do not ask the user to manually draw sprites.
- Do not wait for perfect external art.
- Do not make the prototype depend on unavailable assets.
- Do not stop at documentation only. Create usable Unity assets/scripts/prefabs/scenes.

## Desired result

After implementation, the Unity project should contain:

- organized art folders
- generated prototype art
- working import settings
- terrain/trench visuals
- props and emplacements
- small units with animations
- VFX sheets and particle prefabs
- UI icons/overlays
- a complete visual test scene
- a report explaining what was created and how to use it
