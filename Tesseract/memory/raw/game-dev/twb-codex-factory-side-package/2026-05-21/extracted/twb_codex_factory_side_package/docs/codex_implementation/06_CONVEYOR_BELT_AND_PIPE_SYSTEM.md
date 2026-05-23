# Conveyor Belt and Pipe System

## Purpose

Implement logistics movement in a simple deterministic way.

---

## Belt segment model

Each belt segment should know:

- grid position
- input direction(s) if needed
- output direction
- speed
- next segment reference or lookup
- current item slots/tokens

---

## Item token model

Each item token should know:

- ItemDefinition
- current segment
- progress 0..1
- visual GameObject/SpriteRenderer
- blocked state if necessary

---

## Movement behavior

Each tick/update:

1. item advances along segment
2. if progress reaches end, find next target
3. if next target accepts item, transfer
4. if not, item waits/blocks

---

## Machine port behavior

Machines should expose ports:

- input ports consume acceptable items
- output ports attempt to push items onto adjacent belt

Port orientation should respect building rotation.

---

## Visual handling

- item token position lerps along segment path
- belt sprites show direction
- corners move item along curved or two-point path if possible
- simple centerline movement is acceptable first

---

## Pipe system minimum

For first build, pipe logic can be minimal:

- pipe segment has connections
- source marks connected network as hasFluid
- machine requiring fluid checks adjacent/network state

If not needed by first recipes, implement only art/prefabs and defer logic.

---

## Avoid

- Rigidbody item movement
- collision-based handoff
- uncontrolled object spawning
- complex belt intersections before basic chain works

---

## Acceptance criteria

A visible item token can move from extractor output to processor input, then from processor output to workshop input, then to depot.
