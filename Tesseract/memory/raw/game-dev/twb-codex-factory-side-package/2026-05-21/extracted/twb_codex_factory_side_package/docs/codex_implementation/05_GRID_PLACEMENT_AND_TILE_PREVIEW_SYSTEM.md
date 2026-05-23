# Grid Placement and Tile Preview System

## Purpose

This document defines the build placement system.

---

## Required components

### FactoryGrid
Responsible for:

- grid dimensions
- world-to-cell conversion
- cell-to-world conversion
- occupancy lookup
- placement validation

### FactoryGridCell
Stores:

- coordinates
- occupant reference
- floor type if needed
- resource node if present

### FactoryPlacementController
Responsible for:

- selected building definition
- ghost movement
- rotation
- placement command
- cancel placement
- remove/deconstruct command if implemented

### FactoryPlacementGhost
Responsible for:

- preview sprite
- footprint highlight
- valid/invalid material or overlay
- rotation display
- port arrows if possible

### FactoryBuildingDefinition
Defines:

- id
- display name
- category
- footprint
- prefab
- cost
- ports
- power need
- recipe/machine role

---

## Placement behavior

- snap to grid
- validate footprint
- prevent overlap
- allow rotation where relevant
- place prefab at footprint center
- mark cells occupied
- show invalid feedback if blocked

---

## Floor display

Use tiles/sprites to create a readable yard:

- compacted dirt base
- concrete pads under machines if useful
- resource patches
- loading pad for depots

---

## Controls

Use existing project input style if known.

Minimum editor/dev controls are acceptable:

- click to place
- key to rotate
- key or button to select building

---

## Acceptance criteria

The player/developer can place an extractor, belt, processor, workshop, depot, and generator on the grid with clear visual feedback.
