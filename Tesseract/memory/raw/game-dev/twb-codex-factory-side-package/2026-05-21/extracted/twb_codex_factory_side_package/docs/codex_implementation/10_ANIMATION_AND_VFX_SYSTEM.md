# Animation and VFX System

## Purpose

Make the factory feel alive using simple reusable effects.

---

## Required visual loops

### Belts
- item tokens move
- optional belt direction animation

### Extractor
- dust/spark emission while working
- optional drill bob

### Processor
- smoke/spark emission while working
- optional press/furnace pulse

### Workshop
- tool/press pulse while working
- output crate pulse on completion

### Generator
- smoke loop or fan animation while active

### Depot
- output pulse when item delivered to frontline supply

---

## Implementation options

Use whichever is simplest for the project:

- Animator components with simple sprites
- scripted scale/position pulses
- ParticleSystem using generated sprites
- sprite sheet flipbooks

---

## State-driven animation

Animations should depend on machine state.

- Working: active animation/VFX
- NoPower: animation off, warning visible
- MissingInput: animation off, missing input icon
- OutputBlocked: animation off or jam pulse, blocked icon

---

## Acceptance criteria

When machines work, the scene feels active.
When machines stop, the scene clearly communicates why.
