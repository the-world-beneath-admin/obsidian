# Factory Animation and VFX

## Purpose

Simple animation and effects make the factory feel alive.

This is important because the art style is intentionally simple.

---

## 1. Animation philosophy

Use cheap, clear loops:

- belts scroll
- item tokens move
- machines pulse/bob/press
- fans rotate
- smoke puffs
- sparks flicker
- status lights blink

Do not make complex frame-heavy animations first.

---

## 2. Required animation/VFX categories

### Logistics
- moving item tokens
- belt motion
- output pulse

### Machines
- extractor dust/sparks
- processor smoke/sparks
- workshop tool movement
- generator smoke/fan

### Feedback
- missing input icon
- blocked output icon
- no power icon
- production complete pulse
- invalid placement flash

---

## 3. Belt animation

Can be implemented as:

- scrolling texture
- cycling sprite frames
- small repeated chevron movement
- item movement only

Item movement alone may be enough for the first prototype.

---

## 4. Machine activity

Each machine type should have a simple activity cue:

### Extractor
- drill/scoop bob
- dust puff

### Processor
- smoke puff
- spark burst
- glow or press movement

### Workshop
- tool arm bob
- crate output pulse

### Depot
- crate stack update
- output dispatch pulse

### Generator
- smoke loop
- fan/engine wobble

---

## 5. Status icon animation

Status icons should be small and readable.

Examples:

- missing input: crate/question symbol
- blocked: stop/box jam symbol
- no power: lightning warning
- working: small rotating gear or green lamp equivalent

Use shape-first icons, not text.

---

## 6. VFX scale

VFX should not overpower the map.

Small loops are enough:

- smoke puff sheet
- spark sheet
- dust puff sheet
- output pulse ring
- placement footprint highlight

---

## 7. Minimum deliverables

Create:

- belt/item movement visual
- extractor dust
- processor smoke/sparks
- generator smoke
- depot output pulse
- no-power icon
- blocked-output icon
- missing-input icon
