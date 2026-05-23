# Terrain and Trench Generator Implementation

## Purpose

Create readable battlefield terrain and trench visuals.

This is the most important visual foundation.

## Approach

Do not depend on Tilemap unless it already exists.

A simple prototype scene can use:

- SpriteRenderer ground tiles
- SpriteRenderer trench overlays
- SpriteRenderer sandbag overlays
- SpriteRenderer decals

If project already uses Tilemap, Codex may create Tile assets and a Tilemap version as an optional improvement.

## Terrain asset generation

### Ground tile

File:

```text
terrain_ground_temperate_v001.png
```

Size:

```text
128x128
```

Visual:

- muddy green/brown battlefield ground
- low contrast noise
- subtle grass/soil flecks
- top-down flat
- no strong directional features

### Mud tile

File:

```text
terrain_mud_temperate_v001.png
```

Visual:

- darker muddy patch
- damp but not shiny
- used around trenches/roads

### Trench floor

File:

```text
terrain_trench_floor_v001.png
```

Visual:

- compacted darker dirt
- scuffed center
- a few footprints/marks
- lower contrast than sandbags

### Trench edge

Files:

```text
terrain_trench_edge_h_v001.png
terrain_trench_edge_v_v001.png
terrain_trench_edge_corner_ne_v001.png
terrain_trench_edge_corner_nw_v001.png
terrain_trench_edge_corner_se_v001.png
terrain_trench_edge_corner_sw_v001.png
```

Visual:

- raised dirt lip
- darker inner edge shadow
- slightly lighter outer earth
- modular piece

### Sandbag pieces

Files:

```text
terrain_sandbag_strip_h_v001.png
terrain_sandbag_strip_v_v001.png
terrain_sandbag_corner_ne_v001.png
terrain_sandbag_corner_nw_v001.png
terrain_sandbag_corner_se_v001.png
terrain_sandbag_corner_sw_v001.png
terrain_sandbag_cap_n_v001.png
terrain_sandbag_cap_s_v001.png
terrain_sandbag_cap_e_v001.png
terrain_sandbag_cap_w_v001.png
```

Visual:

- lumpy connected bags
- khaki/canvas color
- dark creases
- clear small shadows
- top-left highlight

### Craters

Files:

```text
terrain_crater_small_v001.png
terrain_crater_medium_v001.png
terrain_crater_large_v001.png
```

Visual:

- dark depression
- raised rim
- broken mud
- optional scorch
- transparent background

### Decals

Files:

```text
decal_mud_smear_a_v001.png
decal_mud_smear_b_v001.png
decal_boards_a_v001.png
decal_debris_a_v001.png
decal_rocks_a_v001.png
decal_boot_wear_a_v001.png
```

Visual:

- transparent background
- subtle
- reusable scatter

## Trench layout for demo scene

The generated vertical slice should create a trench network:

```text
        [MG]
         |
  ---====+====---
      [Mortar]
         |
      supply path
```

Use a mix of:

- horizontal trench
- vertical trench
- junction
- node/pocket
- sandbag wall overlays
- props

## Demo scene placement method

Use a simple grid.

Recommended:

- tile size: 1 Unity unit
- each terrain tile: 1x1
- trench floor sprites: placed on top of ground at tile positions
- sandbags: placed along trench edges
- props: placed slightly offset for organic feel

## Sorting

Recommended sorting orders:

```text
ground: 0
mud patches: 5
trench floor: 10
trench edge shadows: 15
sandbags: 20
decals: 25
props: 40
units: 50
weapons: 55
vfx: 80
world UI: 100
```

## Trench quality test

The scene passes if:

- trench path is obvious
- sandbag cover is obvious
- the floor and walls are distinct
- weapons feel embedded in the position
- decals add life without clutter
