# Terrain and Trench System

## Purpose

This document defines how terrain and trench visuals are created.

Terrain is the backbone of the game.
If terrain looks solid, the whole game will already feel much better.

## 1. Terrain production model

Terrain is built from five main categories:

1. base materials
2. trench masks
3. edge / wall overlays
4. decals and scatter
5. shadow / depth overlays

## 2. Base biome material sets

Each biome should eventually have its own source set.

Initial production should start with **one biome only**.

Recommended first biome:

- temperate battlefield / damp earth

Later biomes:

- desert
- tropical jungle
- snow / frozen mud
- industrial / ruined urban

### Each biome should include

- flat ground material
- trench floor material
- outer berm / wall material
- sandbag material
- timber / reinforcement material
- mud smear / wear decals
- rock / debris scatter

## 3. Base material sheet requirements

### Material sheet goals

- top-down orthographic
- no finished map
- no labels
- no UI
- no perspective scene
- clean reusable surface zones

### Typical material zones

- compacted trench floor
- outer ground soil
- wetter mud variant
- sandbag texture region
- timber planks
- reinforcement wood
- exposed soil bank
- rubble / debris patch
- dark shadowy dirt patch
- optional puddle patch

## 4. Trench shape system

The trench itself should be created from masks and runtime/editor assembly.

### Required trench mask families

- straight horizontal
- straight vertical
- outer corner
- inner corner / notch
- T-junction
- cross junction
- end cap
- widened bunker pit / node
- emplacement pocket
- road crossing / trench interruption if needed

### Mask layers per trench element

At minimum:

1. silhouette / fill mask
2. line/detail mask
3. shadow/depth mask

## 5. Sandbag trench wall specification

Sandbag trench walls are a primary identity asset.

### Visual goals

- clearly reads as sandbags
- top-down readable
- slightly organic silhouette
- field-built, imperfect
- still tile-safe
- not hyper-detailed
- not noisy

### Construction style

- rows of connected lumpy bags
- visible seams and tied ends in simplified way
- occasional slight deformation
- mild dirt/wear
- slight top-left light, bottom-right shade

### Trench wall use cases

- straight wall strip
- corner strip
- bunker lip
- emplacement ring
- end cap

## 6. Trench tiers

The art system should support trench upgrade tiers.

### Tier 1: fresh dug earth

- dirt edge
- loose soil lip
- no or minimal reinforcement
- rough shape

### Tier 2: basic sandbag trench

- clear sandbag edge
- compact trench floor
- some wood bracing
- clearer cover geometry

### Tier 3: reinforced trench

- mature sandbag walls
- timber support
- more stable corners
- crates, boards, posts, ammo clutter
- visually developed defensive network

Codex should structure terrain assets so these tiers can be swapped or upgraded.

## 7. Terrain decals

Decals make the world feel used without requiring bespoke tiles.

### Required decal families

- mud smears
- boot wear
- wagon / wheel marks if useful
- loose boards
- shell scuffs
- dirt clumps
- debris patches
- small rock patches
- grass tufts
- spent casings near gun positions
- sandbag stains
- scorched impact marks

### Rules

- keep decals subtle
- avoid over-cluttering
- use many small reusable decals instead of baked-in unique scenes

## 8. Craters and damage

### Crater types

- small shell crater
- medium shell crater
- heavy crater
- crater with wet mud
- crater with broken boards or sandbags

### Layering

Crater visuals may include:

- base depression shading
- rim lip
- exposed soil
- internal dark mud
- optional debris overlay

## 9. Bunker pits and nodes

Some trench nodes should widen into special-purpose spaces.

### Examples

- machine gun nest pocket
- mortar pit
- command pocket
- storage alcove
- dugout entrance area

These should be generated as modular trench expansions rather than full one-off scenes whenever possible.

## 10. Road and path crossings

If trenches intersect supply routes or roads, define:

- compacted crossing dirt
- planked crossing
- damaged crossing
- narrow bridge / duckboard crossing

These should be readable and modular.

## 11. Shadow strategy

Terrain shadows should not be full scene shadows.

Use:

- subtle wall-contact shadow
- trench depth darkening
- sandbag underside darkening
- prop contact shadows

Do not create huge dramatic cast shadows across the map.

## 12. What the terrain should look like

A finished scene should communicate:

- where the trench is
- where the cover is
- where the floor is
- where the battlefield ground is
- where the reinforced points are
- where artillery and logistics have worn the environment

Even if simple, it should feel intentional.

## 13. Required deliverables for one biome

Codex should create these before moving on:

### Materials

- 1 biome source material sheet

### Trench masks

- straight H/V
- corners
- T-junction
- cross
- end cap
- node / widened pocket

### Sandbag overlays

- straight H/V strips
- corner strips
- end caps
- ring or arc segment for pits

### Decals

- mud
- boards
- debris
- damage
- crater set

### Props integrated with terrain

- duckboards
- support posts
- loose sandbags
- ammo pile
- broken timber

Only after this is stable should Codex move to the next biome.
