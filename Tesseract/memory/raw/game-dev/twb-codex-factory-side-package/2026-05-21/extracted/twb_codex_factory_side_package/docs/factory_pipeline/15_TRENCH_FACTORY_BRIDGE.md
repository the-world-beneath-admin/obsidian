# Trench / Factory Bridge

## Purpose

This document defines how the factory side supports the trench battlefield side.

The two halves should feel like one game, not two separate prototypes.

---

## 1. Shared visual language

Both sides should share:

- muted military palette
- upper-left lighting
- top-down 2.5D readability
- modular masks and sprites
- simple readable icons
- muddy field-worn surfaces
- practical wartime equipment

Factory assets can be more industrial, but they must not feel like a different game.

---

## 2. Shared supply logic

Factory output should support battlefield systems.

Recommended supply categories:

| Factory Output | Battlefield Use |
|---|---|
| ammo crates | infantry/MG resupply |
| shell crates | mortar/artillery firing |
| sandbag kits | trench upgrades/fortifications |
| fuel cans | vehicles/generators |
| repair parts | repairing machines, vehicles, bunkers |
| generic supplies | flexible mission resource |

---

## 3. Shared UI language

Resource counters should use the same icons across factory and battlefield.

Example:

- ammo crate icon appears on belt token
- same icon appears in depot UI
- same icon appears in battlefield resupply UI

This makes the game easier to understand.

---

## 4. Shared prop language

Some assets can be reused:

- crates
- barrels
- fuel drums
- pallets
- sandbag piles
- repair tools
- ammo boxes
- smoke/spark VFX

Reuse them where possible.

---

## 5. Scene transition options

The game can connect factory and battle in several ways.

### Option A: Same map edge
Factory exists behind the trench line.
Supply depot sends output along a road to the front.

### Option B: Separate management layer
Factory scene produces counters consumed by battlefield scene.

### Option C: Abstract supply route
Depot output increments supply manager. Battlefield reads from supply manager.

### Recommendation
Start with Option C because it is easiest and reliable.
Then visually represent the route with a depot/truck/road cue.

---

## 6. First integration target

Create a shared manager or simple data object:

```text
FrontlineSupplyManager
  ammo_supply
  fortification_supply
  fuel_supply
  repair_supply
  artillery_supply
```

The factory supply depot increments these values.
The battlefield side can later consume them.

---

## 7. Integration acceptance criteria

The bridge is working when:

- factory produces a recognizable supply item
- item reaches supply depot
- depot increments a frontline supply value
- UI shows the value
- battlefield/trench systems can later consume it without rewriting factory code
