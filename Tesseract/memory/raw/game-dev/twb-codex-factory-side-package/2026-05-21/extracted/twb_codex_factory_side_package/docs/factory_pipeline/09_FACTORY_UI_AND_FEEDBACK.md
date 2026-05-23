# Factory UI and Feedback

## Purpose

The factory side depends on clarity.

The UI must explain machines, recipes, items, and blocked states without becoming complicated.

---

## 1. UI style

Use the same military-practical UI style as the trench side:

- clean panels
- muted dark backgrounds
- simple borders
- small utilitarian icons
- no glossy sci-fi chrome
- no decorative clutter behind text

---

## 2. Required UI panels

### Build menu
Shows placeable factory buildings.

### Selection panel
Shows selected building:

- name
- state
- recipe
- inputs
- outputs
- stored items
- power status

### Resource/supply panel
Shows important counters:

- ammo supply
- sandbag/fortification supply
- fuel supply
- repair supply
- shell/artillery supply

### Warning area
Shows major factory problems:

- no power
- blocked output
- missing input
- storage full

---

## 3. Build menu categories

Recommended categories:

- Logistics
- Production
- Storage
- Power
- Resources
- Defense/Frontline support if applicable

---

## 4. Placement feedback

During placement show:

- ghost sprite
- footprint
- valid placement highlight
- invalid placement highlight
- rotation preview
- port/output arrows if possible

---

## 5. Recipe display

A recipe display should show:

```text
inputs -> machine -> outputs
```

Use icons, not paragraphs.

Example:

```text
ore_chunk -> processor -> metal_parts
metal_parts -> workshop -> ammo_crate
```

---

## 6. Machine state feedback

State should appear both in-world and in selected panel.

In-world feedback:

- small warning icon
- lamp/status marker
- animation stopped if not working

Panel feedback:

- exact reason text
- current stored input/output count

---

## 7. Frontline supply feedback

Since this factory feeds the war side, the UI must show:

- which supplies are being produced
- how much reached the frontline
- whether the front is under-supplied if that system exists

---

## 8. Minimum UI deliverables

For first prototype:

- build menu
- selected building panel
- production counter
- frontline supply counter
- placement ghost
- machine status icons
