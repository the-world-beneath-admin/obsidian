# Task 04 — Belts, Pipes, and Items

## Goal

Create the basic logistics network that moves goods through the factory.

---

## Required belt system

Implement:

- straight belt segment
- corner belt segment
- belt direction/orientation
- item token movement along belts
- simple handoff from belt to belt
- input/output ports for machines
- blocked output detection

---

## Pipe system

If time allows, implement a simple pipe network.

Minimum pipe scope:

- straight pipe
- corner pipe
- pipe connection rules
- simple fluid amount or binary connected/not connected

If pipe implementation is too large, create pipe art and prefabs now, but keep logic minimal.

---

## Item token rules

Use simple item tokens, not physics objects.

Each token should have:

- item id
- sprite/icon
- current segment
- progress along segment
- target direction

---

## Suggested scripts

```text
BeltSegment.cs
BeltNetworkUtility.cs
FactoryItemToken.cs
ItemDefinition.cs
MachinePort.cs
PipeSegment.cs
FluidNetwork.cs
```

---

## Acceptance criteria

This task is complete when:

- items visibly move on belts
- belts can connect several cells
- belts feed at least one machine input
- machine output can place items onto a belt
- blocked belts do not silently delete items
