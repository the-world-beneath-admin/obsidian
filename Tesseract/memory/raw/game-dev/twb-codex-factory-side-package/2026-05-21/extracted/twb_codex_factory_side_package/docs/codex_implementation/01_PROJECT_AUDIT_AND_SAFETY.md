# Project Audit and Safety

## Purpose

Before implementing the factory side, inspect the project and avoid damaging existing systems.

---

## Audit steps

1. Identify Unity version if visible.
2. Inspect `Assets/` folder organization.
3. Look for existing TWB/trench/battlefield folders.
4. Look for existing art pipeline scripts.
5. Look for existing UI framework.
6. Look for existing scene naming conventions.
7. Look for existing ScriptableObject patterns.
8. Look for current input system use.

---

## Safety rules

- Do not delete unrelated files.
- Do not overwrite existing scenes unless specifically required.
- Do not rename existing public classes unless absolutely necessary.
- Do not break battlefield code.
- Do not introduce package dependencies unless necessary.
- Put new work under `Assets/TWB/Factory/` unless project conventions clearly require another folder.

---

## Integration caution

If a battlefield supply manager already exists, integrate carefully.

If no supply manager exists, create a simple one that can later be connected.

---

## Required note file

Create/update:

```text
Assets/TWB/Factory/Docs/factory_implementation_notes.md
```

Include:

- what was found
- where files will be created
- assumptions made
- existing systems to preserve

---

## Completion criteria

This step is complete when the project is understood enough to safely add the factory side.
