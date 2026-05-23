# Codex Task 03 — Build Terrain and Trench System

Read:

- `docs/art_pipeline/03_TERRAIN_AND_TRENCHES.md`
- `docs/codex_implementation/05_TERRAIN_TRENCH_GENERATOR.md`

## Task

Build the usable terrain/trench prefab and scene-placement system.

## Requirements

1. Create terrain prefabs:
   - ground tile
   - mud tile
   - trench floor tile
   - trench edge pieces
   - sandbag straight/corner/cap pieces
   - crater decals
   - mud/debris decals

2. Create prefab paths under:

```text
Assets/TWB/Prefabs/Terrain/
```

3. If the project uses Tilemap, optionally create Tile assets. If not, use SpriteRenderer prefabs.

4. Create simple helper methods in `TwbDemoSceneBuilder` for placing:
   - ground fields
   - trench paths
   - sandbag walls
   - decals

## Done when

- a trench network can be assembled in a scene
- sandbags clearly read as cover
- terrain sorting order is correct
- trench floors, walls, and decals are distinct
