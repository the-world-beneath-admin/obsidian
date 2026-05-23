# Task 03 — Grid, Floor, and Placement

## Goal

Build the placement foundation for the factory side.

---

## Required systems

Implement:

- grid manager
- grid cell data
- factory floor tile display
- building footprint definitions
- placement ghost
- valid/invalid placement feedback
- rotation support
- remove/deconstruct support if practical

---

## Suggested scripts

```text
FactoryGrid.cs
FactoryGridCell.cs
FactoryPlaceable.cs
FactoryPlacementController.cs
FactoryPlacementGhost.cs
FactoryBuildingDefinition.cs
```

Names may vary, but responsibilities should stay clear.

---

## Placement rules

A placeable should define:

- building id
- display name
- footprint width/height
- sprite/prefab
- rotation behavior
- category
- cost if costs exist
- blocks movement/logistics yes/no

---

## Visual feedback

Placement must show:

- ghost preview
- valid placement color/overlay
- invalid placement color/overlay
- footprint highlight
- grid snap

---

## Acceptance criteria

This task is complete when:

- the player or developer can place factory buildings on a grid
- the placement ghost is readable
- invalid placement is prevented or clearly indicated
- building rotation works where relevant
- the factory floor looks intentional, not empty
