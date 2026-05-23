# Power, Fluids, and Overlays

## Purpose

This document defines support systems that make the factory readable and expandable.

---

## 1. Power philosophy

Power should be simple at first.

The first goal is not a perfect electrical simulation.
The first goal is that players understand why machines are working or stopped.

---

## 2. Power model options

### Option A: Radius power
A generator powers machines within a radius.

Pros:
- easiest to implement
- easy to read
- good for prototype

### Option B: Pole network
Power poles connect machines through a network.

Pros:
- more expandable
- more factory-like

### Recommendation
Start with radius power or a very simple pole network.

---

## 3. Power visuals

Power state should be visible through:

- small status lamp
- selected-machine UI
- optional power overlay mode
- generator animation
- no-power warning icon

Do not make power wires visually dominate the scene.

---

## 4. Fluid philosophy

Fluids are optional for the first vertical slice.

If included, keep fluid logic very simple.

---

## 5. Fluid model options

### Option A: Binary fluid connected
Machine works if connected to source through pipe network.

### Option B: Simple amount flow
Pipe network holds an amount value and machines consume it.

### Recommendation
Start with binary connected or simple amount.

---

## 6. Pipe/fluid visuals

Use:

- pipe modules
- valves
- pump source
- selected overlay showing fluid type
- small leak/drip VFX only if useful

---

## 7. Overlay modes

Useful overlays:

- power coverage
- logistics direction
- blocked machine warning
- recipe/status overlay
- resource patch overlay
- supply route overlay to front

Keep overlays off by default unless needed.

---

## 8. Minimum implementation

For first prototype:

- generator prefab
- machines require power bool
- no-power status icon
- power coverage visualization when selected/building
- optional pipe art only

Fluids can be implemented later unless a recipe needs them.
