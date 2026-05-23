# Factory Pipeline Rules

## Purpose

This document defines how factory-side art and implementation should be produced.

---

## 1. Core production rule

Use a modular asset factory, not random finished images.

Factory visuals should be built from:

1. floor materials
2. grid overlays
3. machine body sprites
4. port overlays
5. belt/pipe modules
6. item icons/tokens
7. status overlays
8. VFX loops
9. decals and shadows

---

## 2. Code-generated placeholder art is acceptable

Codex should generate usable prototype sprites in code if image assets are not available.

This is preferred over waiting for perfect art.

A complete simple generated machine is better than a missing high-quality machine.

---

## 3. Machine composition model

Most machines can be made from layered components:

```text
footprint shadow
+ base body
+ top panel
+ functional attachment
+ input port marker
+ output port marker
+ status light
+ optional animation element
```

Example extractor:

```text
resource patch
+ extractor base
+ drill/scoop head
+ output chute
+ dust/spark VFX
+ item output port
```

Example workshop:

```text
base body
+ workbench top
+ mechanical tool arm
+ crate output pad
+ status lamp
+ output belt port
```

---

## 4. Logistics clarity rule

The player must always understand:

- where an item enters
- where an item exits
- what direction a belt moves
- whether a machine is working
- why a machine is stopped

Use visual cues liberally.

---

## 5. Grid clarity rule

The factory side is grid-based.
The grid should be understandable but not ugly.

Use:

- subtle floor seams
- placement ghost footprint
- highlights while building
- clear snap behavior

Do not render a loud always-on grid unless the game needs it.

---

## 6. Belts and pipes

### Belt rules
- one tile/cell per belt segment
- direction must be readable
- corners must be clear
- item tokens should sit on top
- moving item tokens are more important than fancy belt texture

### Pipe rules
- use simple pipe modules
- elbows/flanges help readability
- fluid simulation can be simple at first
- pipe color should not overpower the scene

---

## 7. Machine art count rule

Start with a small machine set:

- extractor
- processor
- workshop
- depot
- power source

Do not create 25 machine types before the first chain works.

---

## 8. Item icon rule

Items should be simplified tokens/icons.

They must be readable on belts and in UI.

Examples:

- ore chunk
- metal plate/part
- ammo crate
- shell crate
- sandbag kit
- fuel can
- repair parts

Do not create tiny realistic objects that vanish at zoom.

---

## 9. Status overlay rule

Every machine should have readable state feedback:

- working
- missing input
- output blocked
- no power
- idle

Status feedback may be a small icon, lamp color, animation state, or UI panel.

---

## 10. Expansion rule

Once one chain works, expand by duplication:

- new recipes
- new item icons
- new machine variants
- new resource patches
- new depot outputs

Never expand by rewriting the entire system.

---

## 11. Final pipeline rule

The factory side should be implemented as a repeatable system that can support many recipes and machines later, while starting with a tiny complete chain now.
