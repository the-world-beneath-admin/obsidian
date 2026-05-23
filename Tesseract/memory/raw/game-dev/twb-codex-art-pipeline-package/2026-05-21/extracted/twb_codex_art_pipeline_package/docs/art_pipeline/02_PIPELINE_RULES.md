# Pipeline Rules

## Purpose

This document defines how art is produced.

Codex must treat this as the mandatory production system.

The game art must be produced through structured layers and modular generation, not through random final-image prompting.

## 1. Core asset model

Every visual asset belongs to one of these categories:

1. material
2. mask
3. line/detail overlay
4. shadow/lighting overlay
5. decal
6. modular prop
7. unit sprite
8. particle/VFX
9. UI/icon
10. composition prefab

## 2. Asset generation strategy

### Wrong approach

“Generate a perfect finished machine gun nest sprite sheet from scratch.”

### Right approach

Generate:

- base materials
- trench masks
- emplacement props
- shadow overlays
- unit sprites
- firing particles
- impact particles

Then assemble them in-engine.

## 3. Terrain assembly model

Terrain and trenches should be assembled from:

- ground materials
- edge masks
- wall masks
- trench floor masks
- sandbag overlays
- wood reinforcement overlays
- mud smears
- debris decals
- shadow overlays

This lets one source set produce many map variations.

## 4. Layer model

### Standard layered asset stack

A typical terrain or object asset may use:

1. base shape or material
2. line/detail layer
3. shadow layer
4. weathering / decal layer
5. optional highlight or wetness accents

Not every asset requires all layers, but the model should stay consistent.

## 5. Image generation expectations

When Codex uses image generation, it must ask for:

- source sheets
- masks
- material donors
- isolated props
- clean top-down objects
- sprite sheets with controlled frame counts
- particles on clean background

Do not ask the model to solve the whole game art problem in one image.

## 6. Reusability rule

If an asset can be reused, it should be generated as a reusable source piece.

Examples:

- one sandbag material strip can support many trench configurations
- one mud decal set can be reused across all maps
- one crate sheet can serve many supply scenes
- one muzzle flash set can work for multiple weapons

## 7. Modular categories

### Terrain

- materials
- edge systems
- trench masks
- decals

### Props

- crates
- barrels
- planks
- posts
- ammo boxes
- tools
- sandbag rows

### Weapons / Emplacements

- MG nests
- mortars
- artillery pieces
- field guns
- anti-tank obstacles

### Units

- rifle infantry
- engineer
- machine gun crew
- mortar crew
- officers
- light vehicles
- trucks
- tanks

### Buildings

- bunkers
- command posts
- depots
- factories
- workshops
- conveyors
- storage yards

## 8. Size and consistency rules

All assets must share a common scale logic.

Recommended working assumption:

- 1 Unity unit = 1 gameplay tile
- terrain tiles = 1x1 units
- infantry footprint = 0.25 to 0.4 units
- small prop footprint = 0.25 to 0.75 units
- MG/mortar footprint = 0.75 to 1.25 units
- truck footprint = 1.5 to 2.5 units
- factory/building footprint = 2 to 6 units

Exact final values can vary by project, but relative scale must remain consistent.

## 9. Direction count rules

To keep production manageable:

### Infantry

- 4 directions minimum
- 8 directions only if essential

### Vehicles

- 4 directions often sufficient
- turret direction may rotate separately in code if possible

### Emplacements

- usually fixed orientation sets or rotation by code

The fewer unique directional art requirements, the better.

## 10. Animation count rules

Keep counts low.

### Suggested frame counts

- idle: 1 to 4 frames
- move: 4 to 6 frames
- fire: 2 to 4 frames
- death: 2 to 4 frames if used
- particles: 4 to 8 frames

Use effects to make low frame counts feel alive.

## 11. Small-unit simplification rules

For infantry and crew:

- helmets required
- weapon silhouette required
- facial detail optional and usually unnecessary
- hands simplified
- legs simplified
- backpack or gear optional if silhouette helps

Avoid trying to make tiny realistic humans.

The art should read as:

**small military miniatures with a gun**

That is enough.

## 12. Terrain material rules

Materials should be generated as:

- clean source sheets
- top-down orthographic
- readable at medium zoom
- not already cut into final gameplay tiles unless specifically required

The engine or tooling should do the final cutting and compositing.

## 13. Alpha and background rules

When generating assets for extraction:

- use transparent backgrounds when supported and appropriate
- if a clean matte background is required for extraction, use a clearly separable matte
- do not bury the asset in a fully illustrated environment unless it is a final composition

## 14. Completion rule

Codex should not stop at “pretty source art exists.”

The pipeline is only complete when:

- source art exists
- file structure is organized
- naming is consistent
- import settings are known
- slicing / assembly rules are defined
- the asset can be used in the game

## 15. Master rule

**Build an asset factory, not a pile of random images.**
