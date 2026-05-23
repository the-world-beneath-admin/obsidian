# Factory Codex Work Order

## Purpose

This is the recommended build sequence.

Codex should not jump to advanced systems before the first production chain works.

---

## Stage 0: Foundation

Create folders, audit project, set naming rules.

Done when:

- factory folders exist
- no existing systems are broken
- implementation notes exist

---

## Stage 1: Generated placeholder art

Create code-generated prototype sprites for:

- floors
- resource nodes
- belts
- machines
- items
- UI status icons
- simple VFX

Done when:

- assets exist in Unity
- they are usable in scene

---

## Stage 2: Grid and placement

Implement:

- factory grid
- placeable definitions
- placement controller
- placement ghost
- rotation support
- footprint validation

Done when:

- machines and belts can be placed on grid

---

## Stage 3: Belts and item movement

Implement:

- belt segments
- item tokens
- movement along belts
- handoff between belts
- input/output ports

Done when:

- item tokens visibly move through a belt line

---

## Stage 4: Machines and recipes

Implement:

- item definitions
- recipe definitions
- extractor
- processor
- workshop
- depot

Done when:

- one full production chain works

---

## Stage 5: Power and state feedback

Implement:

- generator/power source
- machine power requirement
- no-power state
- missing input state
- blocked output state
- working state

Done when:

- stopped machines tell the player why they stopped

---

## Stage 6: UI and feedback

Implement:

- build menu
- selected building panel
- resource/supply counters
- warnings
- status overlays

Done when:

- player can understand the factory without inspecting debug logs

---

## Stage 7: Vertical slice

Create a scene that proves:

```text
resource -> extraction -> belt -> processing -> belt -> assembly -> depot -> frontline supply
```

Done when:

- the output depot increments frontline supply

---

## Stage 8: Polish and report

Improve readability and document next steps.

Done when:

- validation report exists
- known limitations are listed
- next tasks are clear

---

## Final rule

Do not expand to multiple complex chains until the first chain is complete and visually readable.
