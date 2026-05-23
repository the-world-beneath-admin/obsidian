# Task 02 — Factory Art Generator

## Goal

Create generated prototype art so the factory side can look complete without waiting on final image assets.

---

## Instructions for Codex

Build a Unity editor utility that generates simple but readable factory sprites.

The generator should create placeholder/prototype art for:

- floor tiles
- resource nodes
- belts
- belt corners
- splitters if included
- pipes
- pipe elbows
- extractor
- processor
- workshop / assembler
- depot
- power pole
- generator
- item tokens/icons
- machine status icons
- VFX sprites

---

## Required script

Create something like:

```text
Assets/TWB/Factory/Scripts/Editor/FactoryPrototypeArtGenerator.cs
```

The exact class name can vary, but it must be easy to find.

---

## Required behavior

The generator should:

1. create Texture2D assets or PNG files
2. save them into `Assets/TWB/Factory/Art/Generated/`
3. make sprites readable from gameplay zoom
4. use consistent scale and visual language
5. create import-ready assets

---

## Visual rules

Generated art should be simple:

- top-down 2.5D shapes
- muted industrial/military colors
- clear silhouettes
- fake upper-left lighting
- darker contact shadows
- simple outlines only where needed
- no noisy random art

---

## Acceptance criteria

This task is complete when:

- generated factory sprites exist
- sprites are organized by category
- at least one machine, belt, item, and floor tile is visible in Unity
- generated art is usable even if final art never arrives
