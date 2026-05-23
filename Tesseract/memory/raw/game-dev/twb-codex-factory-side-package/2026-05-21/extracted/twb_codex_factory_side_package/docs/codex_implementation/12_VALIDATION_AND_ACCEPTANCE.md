# Validation and Acceptance

## Purpose

Define how to verify the factory implementation.

---

## Compile validation

Check:

- no C# compiler errors
- no missing references that break scene load
- no missing scripts on created prefabs

---

## Art validation

Check:

- generated assets exist
- sprites are readable
- machine scale is consistent
- item icons are distinguishable
- status icons are understandable

---

## Placement validation

Check:

- grid snap works
- footprint validation works
- rotation works for belts/machines where relevant
- invalid placement feedback appears

---

## Belt validation

Check:

- items move
- corners work if used
- blocked belts stop items
- items are not silently deleted

---

## Machine validation

Check:

- extractor produces raw item
- processor consumes raw item and outputs processed item
- workshop consumes processed item and outputs wartime supply
- depot consumes wartime supply and increments counter

---

## UI validation

Check:

- build menu appears
- selected machine panel updates
- status warnings appear
- supply counter changes

---

## Final acceptance

The factory side is accepted when the vertical slice produces a supply output end-to-end and the scene looks complete enough for prototype testing.
