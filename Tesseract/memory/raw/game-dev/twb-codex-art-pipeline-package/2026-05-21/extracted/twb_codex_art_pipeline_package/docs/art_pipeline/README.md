# TWB Tactical Miniature Art Pipeline
## Codex Package

This package defines the full art direction and production pipeline for the game.

The goal is not to chase perfect art.
The goal is to make a game that looks complete, readable, consistent, and scalable using Codex plus procedural generation.

This package assumes:

- engine: Unity
- camera: top-down / slight 2.5D readable game camera
- target look: stylized tactical miniature battlefield
- production method: mask-driven modular art pipeline
- team: Codex only
- priority: finished playable prototype over art perfection

## Core decision

The game will not rely on one-off finished illustrations for every asset.

Instead, the game art will be built from repeatable source pieces:

1. materials
2. masks
3. line/detail overlays
4. shadow overlays
5. decals
6. modular props
7. small unit sprites
8. particle effects
9. simple UI icons

This is the realistic way to make the full game at scale with Codex.

## Visual target

The intended look is:

- readable top-down tactical battlefield
- slight 2.5D depth
- chunky silhouettes
- muted military palette
- simple but believable materials
- visible trenches, sandbags, guns, bunkers, and equipment
- small helmeted soldiers with gun silhouettes
- simple particles and effects to sell combat
- clear functional factory/logistics visuals
- no random-AI look
- no need for perfect realism

Think:

- tactical board-game readability
- handheld-era war game clarity
- simplified painted battlefield materials
- small toy-soldier / diorama feel
- practical military visuals instead of cinematic realism

## Production order

Codex should follow this order exactly.

1. Read `01_ART_DIRECTION_BIBLE.md`
2. Read `02_PIPELINE_RULES.md`
3. Build terrain source system from `03_TERRAIN_AND_TRENCHES.md`
4. Build prop system from `04_PROPS_AND_WEAPONS.md`
5. Build unit system from `05_UNITS_AND_ANIMATION.md`
6. Build particles and effects from `06_VFX_AND_PARTICLES.md`
7. Build UI and icons from `07_UI_AND_ICON_STYLE.md`
8. Follow naming/export rules from `08_FILE_STRUCTURE_AND_EXPORT.md`
9. Use `09_CODEX_WORK_ORDER.md` as the production sequence
10. Use `10_ASSET_CATALOG.md` as the minimum prototype checklist
11. Use `11_IMAGE_GENERATION_BRIEF_TEMPLATES.md` only if image generation is available

## Absolute rules

- Prefer reusable source sheets over finished one-off sprites.
- Prefer modular parts over bespoke illustrations.
- Prefer clarity over detail.
- Prefer scale consistency over extra decoration.
- Prefer game-readability over realism.
- Do not create giant complex soldier art.
- Do not rely on fully unique AI-generated final tiles.
- Do not create perspective scenes.
- Do not create photorealism.
- Do not create huge animation counts.
- Do not create a style that requires a human artist to maintain.

## What “finished enough” means

An asset is good enough if:

- the player instantly knows what it is
- it matches the rest of the game
- it tiles or animates correctly
- it does not visually break the scene
- it supports gameplay clarity
- it can be reproduced by the same pipeline later

If it is a clear sandbag trench, machine gun nest, mortar pit, supply crate, or infantry unit and it fits the style, it is acceptable.

## Art style summary in one sentence

**Stylized top-down 2.5D tactical miniature graphics built from materials, masks, decals, modular parts, simple unit sprites, and lightweight effects.**
