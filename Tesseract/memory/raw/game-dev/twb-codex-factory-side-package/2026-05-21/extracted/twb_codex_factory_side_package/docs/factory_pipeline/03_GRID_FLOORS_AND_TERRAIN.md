# Grid, Floors, and Factory Terrain

## Purpose

This document defines the ground/floor system for the factory side.

The factory floor should support placement readability and still match the war/trench world.

---

## 1. Floor identity

The factory area should feel like a field production yard, not a sterile modern building.

Use a mix of:

- compacted dirt
- muddy tire-worn ground
- worn concrete pads
- metal floor plates where useful
- oil stains
- crate drag marks
- worker path wear

---

## 2. Tile/floor categories

### Required floor tiles
- compacted dirt yard
- worn concrete pad
- muddy industrial edge
- metal plate floor
- resource ground patch edge
- depot/loading pad

### Optional
- rail/track tile
- road tile
- puddle/oil tile
- damaged floor tile

---

## 3. Grid readability

The grid should be visible during placement and subtle otherwise.

### During normal play
- use floor seams and object alignment
- avoid loud grid lines

### During build mode
- show cell highlights
- show footprint preview
- show valid/invalid overlays
- show rotation preview

---

## 4. Factory terrain decals

Use decals to make floors feel used.

### Required decals
- oil stain
- tire mark
- belt dirt streak
- scattered screws/scrap
- mud track
- crate scuff
- coal/ore dust patch
- small puddle
- spark burn mark

---

## 5. Resource patch visuals

Resource nodes must be obvious.

### Ore patch
- clustered dark/metallic stones
- dirt depression
- high contrast enough to see
- not too noisy

### Fuel/coal patch
- dark chunks
- dusty black-brown patch

### Water/fluid source if used
- pumpable pool/tank/well marker
- not huge unless mechanically important

### Wood/scrap source if used
- pile of lumber/scrap pieces
- clear harvesting source

---

## 6. Footprint language

Each building should occupy a clear footprint.

Use:

- base shadow
- floor plate
- foundation outline
- small corner anchors

This helps players understand placement and scale.

---

## 7. Terrain-to-battlefield transition

Factory terrain should be able to blend into battlefield terrain.

Transition examples:

- muddy road from factory to front
- loading yard connected to supply route
- damaged factory outskirts
- supply depot near trench map edge

---

## 8. Minimum deliverables

For the first vertical slice, create:

- one factory yard floor tile
- one concrete pad tile
- one loading pad tile
- one ore patch
- one oil stain decal
- one tire mark decal
- one scrap/debris decal
- build-mode grid overlay
- placement ghost overlay

If these exist, the factory side can look grounded immediately.
