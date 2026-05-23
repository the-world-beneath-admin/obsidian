# Power, Fluids, and Status Overlays

## Purpose

Implement machine status clarity.

---

## Power minimum

Implement a simple power system.

Recommended first version:

- generator provides power radius
- machines check whether they are within powered area
- unpowered machines enter NoPower state
- selected generator shows coverage overlay

---

## Alternative

If a power system already exists, integrate with it instead of duplicating.

---

## Status overlays

Each machine should show small in-world feedback for important states:

- no power
- missing input
- output blocked
- working

Working can be shown by animation instead of an icon.

---

## Status UI

The selected building panel should show exact status text.

Examples:

- `Working: producing ammo crate`
- `Missing input: metal parts`
- `Output blocked`
- `No power`

---

## Fluids

Fluid logic is optional for first vertical slice.

If implemented, use simple connected network logic only.

---

## Acceptance criteria

A player should never have to guess why a machine is stopped.
