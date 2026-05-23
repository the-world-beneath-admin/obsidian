# Machines and Buildings

## Purpose

This document defines the factory machines and industrial buildings.

The first version should include only enough machines to create a working supply chain.

---

## 1. Machine categories

### Resource machines
- extractor / drill / pump

### Processing machines
- processor / smelter / crusher / refinery-style machine

### Assembly machines
- workshop / assembler / fabrication bench

### Logistics buildings
- storage depot
- supply depot
- loading platform

### Power machines
- generator
- power pole / connection post

---

## 2. Extractor

### Purpose
Pulls raw resources from a resource patch.

### Visual recipe
- anchored base
- drill/scoop/pump head
- dust or spark point
- output chute
- small status lamp
- footprint/foundation

### Gameplay role
- requires resource node under/near it
- periodically outputs raw item
- outputs to belt or internal storage

### Must look like
A machine taking something from the ground.

---

## 3. Processor

### Purpose
Turns raw resources into usable parts.

### Visual recipe
- squat metal body
- vent or smoke stack
- press/furnace/crusher symbol
- input side
- output side
- working animation area

### Gameplay role
- consumes raw item
- produces processed item
- may require power/fuel

### Must look like
A heavy machine that transforms material.

---

## 4. Workshop / Assembler

### Purpose
Combines processed goods into military supplies.

### Visual recipe
- wide workbench/machine body
- tool arm/press/head
- crate output platform
- small conveyor connection
- status lamp

### Gameplay role
- consumes one or more processed items
- produces wartime output item

### Must look like
A machine making finished supply crates or components.

---

## 5. Storage depot

### Purpose
Stores items and buffers factory flow.

### Visual recipe
- crate stacks
- pallet base
- loading pad
- open top or visible goods
- input/output areas

### Gameplay role
- accepts items
- stores counts
- outputs on demand or through belts

### Must look like
A place where supplies accumulate.

---

## 6. Frontline supply depot

### Purpose
Converts factory output into battlefield supply.

### Visual recipe
- larger depot or loading dock
- crates and military marking
- truck/loading cue
- arrow/route toward front
- output pulse effect

### Gameplay role
- consumes finished supply item
- increments frontline supply counters
- optionally spawns trucks or sends logistics events

### Must look like
The link between factory and war front.

---

## 7. Power source

### Purpose
Makes machine operation visually and mechanically clear.

### Visual recipe
- generator body
- smoke stack or fan
- fuel tank/can
- cable/pole connection
- animated smoke/fan

### Gameplay role
- provides power radius or network
- machines outside power show warning

---

## 8. Machine size guidance

Start with simple sizes:

- small props: 1x1
- belts/pipes: 1x1
- extractor: 2x2
- processor: 2x2 or 3x2
- workshop: 3x2
- depot: 3x3
- supply depot: 4x3
- generator: 2x2

Exact values may change, but scale must remain consistent.

---

## 9. Minimum deliverables

Create these first:

- extractor
- processor
- workshop
- storage depot
- frontline supply depot
- generator
- power pole or power overlay

Each machine must have:

- prefab
- sprite/art
- footprint
- input/output ports if applicable
- status display
