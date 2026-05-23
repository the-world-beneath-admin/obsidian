# Definition of Done

The art pipeline first pass is done when the following are true.

## Project safety

- existing code is not deleted
- existing scenes are not overwritten
- generated files live under `Assets/TWB/`
- changes are documented

## Tooling

- menu command exists to generate prototype art
- folders are created automatically
- generated assets can be regenerated
- report file is generated

## Art

- terrain is generated
- trench visuals are generated
- sandbag visuals are generated
- props are generated
- MG and mortar are generated
- infantry are generated
- vehicle is generated
- VFX are generated
- UI icons/markers are generated

## Prefabs

- terrain/prop/weapon/unit/VFX/UI prefabs exist
- prefabs use valid sprites
- prefabs have reasonable sorting orders
- weapon prefabs have VFX anchors
- unit prefabs can animate in demo scene

## Scene

- vertical slice scene exists
- scene opens
- scene has organized hierarchy
- scene has camera
- scene visibly shows the art direction
- scene includes battlefield and logistics pieces

## Visual quality

The scene does not need final art.

It must look:

- intentional
- consistent
- readable
- complete enough for a game prototype

It must not look like:

- random debug blocks
- unrelated AI images
- inconsistent asset-store pieces
- empty placeholder prototype

## Final status

Report should say:

```text
Prototype art pipeline status: usable first pass.
```

Only say this if the pipeline actually works.
