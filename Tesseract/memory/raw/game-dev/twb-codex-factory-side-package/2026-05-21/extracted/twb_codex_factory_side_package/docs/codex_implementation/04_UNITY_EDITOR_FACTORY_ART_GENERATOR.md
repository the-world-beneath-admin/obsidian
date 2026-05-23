# Unity Editor Factory Art Generator

## Purpose

Codex should build an editor utility that creates basic readable factory art.

This gives the project a usable visual foundation even without external image generation.

---

## Suggested script

```text
Assets/TWB/Factory/Scripts/Editor/FactoryPrototypeArtGenerator.cs
```

---

## Menu item

Add an editor menu command similar to:

```text
TWB/Factory/Generate Prototype Factory Art
```

---

## Generator responsibilities

The generator should:

1. create output folders
2. generate Texture2D images
3. save PNGs into `Assets/TWB/Factory/Art/Generated/`
4. refresh the AssetDatabase
5. set sprites/import settings if feasible
6. optionally create simple materials or sprite assets

---

## Drawing approach

Use simple primitive drawing helpers:

- fill rectangle
- rounded rectangle if easy
- circle/ellipse
- line
- polygon/triangle
- noise speckle
- shadow layer
- highlight edge

Do not overcomplicate art generation.

---

## Visual recipes

### Belt
- dark central strip
- side rails
- direction chevrons
- slight top-left highlight
- lower-right shadow

### Pipe
- rounded metal tube
- flanges
- darker lower side
- corner elbows

### Extractor
- base plate
- drill/scoop head
- output chute
- resource dust
- status lamp

### Processor
- metal body
- vent/smokestack
- press/furnace mark
- input/output ports

### Workshop
- broad body
- tool arm/press head
- output crate platform

### Depot
- platform
- crate stacks
- loading marker
- output arrow toward front

### Generator
- engine body
- fan/vent
- smoke stack
- power marker

---

## Import handling

If possible, set generated PNGs to Sprite import mode.

If not practical, document manual import expectations in implementation notes.

---

## Acceptance criteria

The generator is acceptable when one menu command can produce all base factory placeholder assets in organized folders.
