# TWB Creature Sprite Sheet Asset Contract

## Status

Active asset contract - created 2026-05-12.

## Source And Output Location

Source creature portraits and final walk sheets live in:

```text
C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\<affinity>\<biome>\
```

Special creatures use:

```text
C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\<group>\
```

## Naming Contract

- Start with the source card-art stem.
- Strip only a terminal version suffix such as `-v2`.
- Append `-walk-4dof-1024`.

Each completed creature should have sibling files:

- `.png`
- `.png.meta`
- `.manifest.json`

## Sheet Contract

- Canvas: `1024x1024`
- Grid: `4x4`
- Cell size: `256x256`
- Frames per direction: `4`
- Row order: `down`, `left`, `right`, `up`
- Background: true transparent `RGBA`
- Temporary matte/chroma background, if needed during generation or cleanup: flat magenta `#FF00FF`
- Forbidden temporary matte/background: lime or green

## Finishing Pass Contract

Before final repack or acceptance, each creature needs an edge cleanup pass:

- remove matte/chroma spill
- remove cutout halos and outline artifacts
- clean 1-2 px edge fringe without damaging the silhouette
- reject or redo output with visible green, lime, magenta, white, dark, or colored fringe around the sprite
- final output remains true transparent `RGBA`

## Unity Import Contract

- Texture Type: `Sprite (2D and UI)`
- Sprite Mode: `Multiple`
- Pixels Per Unit: `100`
- Pivot: `{x: 0.5, y: 0.08}`
- Mipmaps: disabled
- Compression: none
- Alpha Is Transparency: enabled
- Slice count: `16`

## QA Contract

Before a creature is marked done:

- Final PNG exists beside source card art.
- PNG is `1024x1024`.
- PNG mode is `RGBA`.
- Alpha extrema include `0` and `255`.
- All four corner alpha values are `0`.
- Every `256x256` cell has non-empty alpha content.
- `.png.meta` exists.
- `.png.meta` contains `spriteMode: 2`.
- `.png.meta` contains `alphaIsTransparency: 1`.
- `.png.meta` has `16` slice names.
- `.manifest.json` exists.
- Visual inspection confirms no cropping and usable row order.
- Visual inspection confirms no matte spill, chroma fringe, or cutout outline artifacts.

## Source Documents

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\CREATURE_WALK_SPRITESHEET_USAGE.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\T1_CREATURE_WALK_SPRITESHEET_HOWTO.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\README.md`
