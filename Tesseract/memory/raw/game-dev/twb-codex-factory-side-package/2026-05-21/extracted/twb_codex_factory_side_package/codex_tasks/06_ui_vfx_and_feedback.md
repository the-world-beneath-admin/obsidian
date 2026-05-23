# Task 06 — UI, VFX, and Feedback

## Goal

Make the factory side understandable and alive.

---

## Required UI

Implement basic UI for:

- build menu
- selected building panel
- recipe/status display
- item/resource display
- power warning
- blocked output warning
- frontline supply counter

---

## Required VFX / feedback

Add simple effects:

- belt motion effect
- machine working animation
- processor sparks/smoke
- generator smoke
- depot output pulse
- placement sound hook placeholders if applicable
- invalid placement feedback

Actual audio is optional unless the project already has an audio framework.

---

## Visual priority

Do not make fancy UI first.
Make clear UI first.

A player should know:

- what the building is
- what it needs
- what it makes
- why it is not working
- where supplies are going

---

## Acceptance criteria

This task is complete when:

- selected machines show status
- warnings are visible
- working machines visibly animate or emit effects
- belts/items are readable in motion
- the factory loop feels alive enough for prototype testing
