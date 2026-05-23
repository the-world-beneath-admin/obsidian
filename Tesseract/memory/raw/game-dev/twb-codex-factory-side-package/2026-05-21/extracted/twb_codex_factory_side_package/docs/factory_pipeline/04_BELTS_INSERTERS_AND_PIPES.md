# Belts, Inserters, and Pipes

## Purpose

This document defines the logistics visuals and behavior.

The factory side needs moving goods. Belts and pipes are the clearest way to show that.

---

## 1. Conveyor belt visual standard

Belts should be readable at a glance.

### Required visual parts
- dark belt surface
- side rails
- direction cue
- item travel lane
- optional roller marks

### Belt segment types
- straight horizontal
- straight vertical
- corner NE/SE/SW/NW
- input/output cap if needed
- splitter optional
- underground/bridge belt optional later

---

## 2. Belt direction clarity

Use at least one of:

- animated belt texture
- small direction chevrons
- item movement
- side rail shape

Item movement is the most important cue.

---

## 3. Belt behavior scope

For first implementation:

- one item lane per belt
- fixed item speed
- item-to-item spacing
- handoff to next belt
- machine output can insert item on belt
- machine input can consume item from belt

Do not build a complex multi-lane logistics solver first.

---

## 4. Inserters / loaders

The game may use inserters, loaders, or direct ports.

### Recommended first prototype
Use direct machine ports instead of complex inserter arms.

A machine can:

- consume from adjacent input belt/port
- output to adjacent belt/port

### Optional later
Add small loader/inserter props:

- short mechanical arm
- pickup claw
- rotate/pivot animation
- input/output arrows

---

## 5. Pipe visual standard

Pipes should be simple and modular.

### Required pipe pieces
- straight horizontal
- straight vertical
- corner elbow
- T junction optional
- valve piece optional
- pump piece optional

### Visual cues
- dull metal pipe
- flanges/bolts simplified
- darker lower-right edge
- small fluid marker only when selected or needed

---

## 6. Pipe behavior scope

First implementation can be simple:

- connected/not connected network
- fluid source provides amount
- machine requires fluid presence
- no pressure simulation required

This is enough for early gameplay.

---

## 7. Item tokens on belts

Item tokens should be drawn on top of belts.

They should be:

- larger than realistic scale
- icon-like
- readable
- centered on belt lane
- not hidden by belt texture

---

## 8. Blocked state visual

When a belt or output is blocked:

- machine status changes
- output port can flash or show warning
- item token stops visibly

Blocked feedback is critical.

---

## 9. Minimum deliverables

For first vertical slice:

- straight belt H/V
- belt corner pieces
- moving item token system
- machine input/output port behavior
- simple pipe art
- simple pipe prefab or module
- blocked output detection
