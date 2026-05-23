# External Game Dev Resource Index

Created: 2026-05-19

## Purpose

Curated external resources for the kinds of games currently under The World Beneath:

- top-down and 3/4-view pixel games
- isometric or pseudo-isometric factory/war maps
- tilemaps, tilesets, interiors, objects, UI, and readable game art
- sprite sheets, 2D animation, and engine import workflows
- factory/logistics simulations and trench-war supply systems

Use this page as a read-first reference for workers creating art contracts, animation pipelines, tilemap systems, factory/logistics systems, or visual QA plans.

## Source And Asset Boundary

- These links are references and learning sources, not asset banks by default.
- Do not copy, trace, recolor, rehost, or ship tutorial images unless the source license explicitly permits it.
- Treat tutorial screenshots, example sprites, and sample sheets as copyrighted unless clearly licensed otherwise.
- Prefer CC0 assets for placeholders, but still record source links and verify each pack page manually.
- CC-BY requires attribution. CC-BY-SA/GPL-style game assets can complicate commercial pipelines and need review before use.
- Pinterest, ripped sprite sheets, fan wikis, Reddit image dumps, and vague "free asset" pages are not acceptable production sources.

## Best Companion Resources To SLYNYRD

Primary existing TWB note: [[wiki/game-dev/slynyrd-pixelblog-reference]]

### Pixel Art And Visual Design

- [Lospec](https://lospec.com/) and [Lospec Palette List](https://lospec.com/palette-list)
  - Use for palette exploration, tutorials, and visual consistency study.
  - TWB use: create project-specific palette rules per biome, UI layer, and game lane rather than adopting a palette blindly.
- [Pedro Medeiros / Saint11](https://saint11.art/)
  - Use for pixel-art animation, effects, style consistency, and production thinking.
  - TWB use: excellent reference for animation readability and avoiding mismatched modern UI pasted over pixel scenes.
- [Sandro Maglione - How to Create a Pixel Art Tileset](https://www.sandromaglione.com/articles/how-to-create-a-pixel-art-tileset-complete-guide)
  - Use for detailed tileset construction: center tile, borders, outer corners, single-tile strips, internal corners, mixed border/corner cases, repetition control, and tile-count planning.
  - TWB use: Garden plots, dungeon rooms, Trenchworks terrain patches, walls, trenches, roads, cave edges, and any tile family that must compose into irregular shapes.
  - Key warning: a tile cannot be designed in isolation; every tile must fit adjacent tiles and repeated placement in the full map context.
- [Pixel Parmesan - Fundamentals of Isometric Pixel Art](https://pixelparmesan.com/blog/fundamentals-of-isometric-pixel-art)
  - Use for 2:1 isometric line rules and projection discipline.
  - TWB use: Trenchworks props/hardpoints if the project leans into iso or 2.5D.
- [Pixnote - Isometric Pixel Art Guide](https://pixnote.net/en/learn/isometric/)
  - Use for accessible isometric cubes, lighting faces, draw order, and tile-size discussion.
  - TWB use: onboarding for isometric prop or battlefield-doodad workers.

### Engine Tilemap References

- [Unity Manual - Isometric Tilemaps](https://docs.unity.cn/Manual/Tilemap-Isometric.html)
  - Use for official Unity isometric tilemap behavior, pseudo-depth, height, and sorting concepts.
  - TWB use: if Trenchworks moves toward iso, art contracts need sorting axis, pivot, tile footprint, and occlusion behavior.
- [Unity - Optimize performance of 2D games with Tilemap](https://unity.com/how-to/optimize-performance-2d-games-unity-tilemap)
  - Use for performance framing and tilemap batching/authoring expectations.
  - TWB use: main Unity and Trenchworks map rendering decisions.
- [MDN - Tiles and Tilemaps Overview](https://developer.mozilla.org/docs/Games/Techniques/Tilemaps)
  - Use for engine-agnostic tilemap structure, logic grids, layers, collision, and pathfinding graph implications.
  - TWB use: browser World Keys and shared mental model for grid-based scenes.
- [Godot TileMap Documentation](https://docs.godotengine.org/en/stable/tutorials/2d/using_tilemaps.html)
  - Use as a design reference for autotiles, scattering, collision, navigation, and Y-sort thinking even when TWB is not using Godot.
  - TWB use: controlled scatter/detail tiles in Garden-style maps without visual clutter.
- [Tiled Documentation](https://doc.mapeditor.org/) and [Tiled Automapping](https://doc.mapeditor.org/en/latest/manual/automapping/)
  - Use for external map-authoring patterns and rule-based tile placement.
  - TWB use: map editor concepts, terrain transitions, and possible future procedural/manual hybrid workflows.

### Tileset Construction Notes

Sandro Maglione's tileset guide is now the main non-SLYNYRD reference for how TWB workers should think about complete tile families.

Use these lessons when commissioning Garden tiles, dungeon/cave tiles, Trenchworks trenches, roads, walls, hardpoint pads, terrain patches, or machine floors:

- Start with the center tile. It must repeat cleanly in all directions and hide the grid where possible.
- Add one-sided border tiles for each side only after the center tile repeats correctly.
- Add outer corners so bordered areas can form complete rectangles/platforms.
- Add single-tile horizontal/vertical strip cases when paths, walls, trenches, roads, or narrow ledges can be only one tile wide.
- Add internal corners for concave shapes. Without them, irregular rooms, trenches, cave edges, and roads will show missing or wrong transition pixels.
- Add mixed border/internal-corner cases for protrusions, intersections, thin corridors, and non-rectangular blobs.
- A full square-tile transition set can reach 47 tiles plus an empty tile before variants.
- Long repeated edges usually need 2-5 variants for the most common tiles, or the pattern becomes visibly mechanical.
- Repeated sub-tile clusters can reduce production burden. Build corner/border pieces from reusable quadrants or mini-components where the style allows it.

TWB worker contract additions:

- Name the tile family: ground, wall, trench, road, water, cave, crop-bed, platform, machine-floor, hardpoint, etc.
- Define whether the first milestone needs a minimal set, a complete transition set, or a visual prototype set.
- Do not request a "complete tileset" unless the worker is allowed to handle center, borders, corners, single-tile strips, internal corners, mixed cases, and variants.
- Require a test map showing straight lines, corners, concave shapes, one-tile corridors, protrusions, islands, and long repeated edges.
- Require light/dark/background QA and in-engine placement checks, not only isolated tile-sheet review.

### Legally Safer Placeholder / Study Asset Sources

- [itch.io CC0 Game Assets](https://itch.io/game-assets/assets-cc0/free)
- [itch.io CC0 Pixel Art + Top-Down filter](https://itch.io/game-assets/assets-cc0/tag-pixel-art/tag-top-down)
- [OpenGameArt licensing FAQ](https://opengameart.org/node/5571)
- [VEXED - Bountiful Bits CC0 top-down tileset](https://v3x3d.itch.io/bountiful-bits)

Use these for placeholder/study material only after verifying the individual source page. Keep attribution records even for CC0 when practical.

## Sprite Sheet And Animation Pipeline

### Core Tools And Docs

- [Aseprite Sprite Sheet Docs](https://www.aseprite.org/docs/sprite-sheet/)
- [Aseprite CLI Docs](https://www.aseprite.org/docs/cli/)
- [Phaser Animations Docs](https://docs.phaser.io/phaser/concepts/animations)
- [Phaser Loader Docs](https://docs.phaser.io/phaser/concepts/loader)
- [Phaser Aseprite Loader](https://docs.phaser.io/api-documentation/3.90.0/class/loader-loaderplugin#aseprite)
- [Unity Learn - Sprite Editor and Sheets](https://learn.unity.com/tutorial/introduction-to-sprite-editor-and-sheets)
- [Unity Sprite Atlas Reference](https://docs.unity.cn/2023.2/Documentation/Manual/class-SpriteAtlas.html)
- [Unity TileAnimationData](https://docs.unity.cn/2021.2/Documentation/Manual/Tilemap-ScriptableTiles-TileAnimationData.html)
- [ImageMagick Command Options](https://imagemagick.org/script/command-line-options.php)

### Aseprite Export Baseline

Use this as a starting point for worker discussion, not a universal command:

```powershell
aseprite -b source.aseprite `
  --sheet output.png `
  --data output.json `
  --format json-array `
  --sheet-type rows `
  --border-padding 1 `
  --shape-padding 1 `
  --inner-padding 0 `
  --extrude
```

TWB implications:

- Use tags to preserve animation names.
- Preserve or document frame order.
- Export JSON metadata when runtime import benefits from tags/frames.
- Use padding/extrusion to reduce sampling bleed.
- Still run visual QA on light and dark backgrounds.

### Phaser Fixed-Grid Example

Useful for browser World Keys such as Glassroot Garden:

```ts
this.load.spritesheet("pet_chuck", "assets/pets/chuck.png", {
  frameWidth: 64,
  frameHeight: 64,
  spacing: 1,
});

this.anims.create({
  key: "pet_chuck:idle",
  frames: this.anims.generateFrameNumbers("pet_chuck", { start: 0, end: 3 }),
  frameRate: 6,
  repeat: -1,
});
```

### Phaser Aseprite Example

Useful when Aseprite JSON tags become the source of truth:

```ts
this.load.aseprite("pet_chuck", "assets/pets/chuck.png", "assets/pets/chuck.json");
this.anims.createFromAseprite("pet_chuck", ["idle", "walk", "work"]);
```

### Unity Pixel Import Baseline

Use for main-game companions and Trenchworks units:

```text
Texture Type: Sprite (2D and UI)
Sprite Mode: Multiple
Filter Mode: Point
Compression: None
Mesh Type: Full Rect for stable frame boxes, Tight only when explicitly wanted
Pivot: consistent per creature/unit family
Sprite Atlas Padding: nonzero, commonly 2-4px
```

### Animation QA Checklist

- Verify frame count matches manifest/tags.
- Verify every frame has the same canvas size unless atlas JSON intentionally controls bounds.
- Check dark and light preview backgrounds.
- Check no cyan/magenta matte pixels remain in visible alpha.
- Check no unintended partially transparent fringe.
- Check pivot/feet/contact point does not jitter.
- Check idle/walk/attack loops at target FPS in engine, not only in Aseprite.
- Check Phaser/Unity import settings preserve crisp pixels.
- Require workers to report export settings, import settings, preview evidence, and remaining provenance risk.

## Factory, Logistics, And Trench-War Simulation Resources

### Factorio And Automation Design

- [Factorio Friday Facts #176 - Belts optimization](https://www.factorio.com/blog/post/fff-176)
  - Use for high-scale belt simulation architecture.
  - TWB Trenchworks lesson: model long supply runs as transport lines, not thousands of independent item entities. Split only at meaningful interaction points.
- [Factorio Friday Facts #276 - Belt item spacing](https://factorio.com/blog/post/fff-276)
  - Use for how tiny spacing/math decisions affect readability and planning.
  - TWB Trenchworks lesson: choose supply rates that divide cleanly into tile/tick units.
- [Factorio Friday Facts #302 - Multiplayer megapacket](https://www.factorio.com/blog/post/fff-302)
  - Use for deterministic simulation and input/state separation ideas.
  - TWB Trenchworks lesson: keep simulation state sacred and visuals/debug layers separate.
- [Factorio Wiki - Main Bus](https://wiki.factorio.com/tutorial%3Amain_bus)
  - Use for structured production layouts and anti-spaghetti design.
  - TWB Trenchworks lesson: a central war-supply bus can teach players how resources move, but should not hide starvation behind fake fullness.
- [Factorio Wiki - Transport Network](https://wiki.factorio.com/Transport_network)
- [Factorio Wiki - Circuit Network](https://wiki.factorio.com/Circuit_network)
  - Use for readable automation verbs: read, stop, prioritize, conditional dispatch.

### Open-Source Factory / Defense References

- [shapez.io source](https://github.com/tobspr-games/shapez.io)
  - Use for simplified production-chain readability.
  - TWB lesson: clarity over realism can make automation easier to learn.
- [Mindustry source](https://github.com/Anuken/Mindustry)
- [Mindustry Logic Docs](https://mindustrygame.github.io/wiki/logic/0-introduction/)
  - Use for belts, production, defense, units, ammo logistics, and optional programmable automation.
  - TWB lesson: closest open-source reference for blending factory logistics with combat pressure.
- [Satisfactory production line tips](https://satisfactory.wiki.gg/wiki/Tutorial:Production_line_design_tips)
- [Satisfactory Balancer](https://satisfactory.wiki.gg/wiki/Balancer)
  - Use as contrast between manifolds/backpressure and exact balancing.
  - TWB lesson: manifolds may feel organic for trench supply; exact balancers can become advanced engineer tools.

### Simulation Architecture

- [Game Programming Patterns - Spatial Partition](https://www.gameprogrammingpatterns.com/spatial-partition.html)
  - Use for grid-based nearby-unit/resource/threat lookup.
  - TWB lesson: fixed grid partitions are a natural fit for trench cells, squads, supply nodes, and influence fields.
- [Unity DOTS](https://unity.com/dots)
- [Unity DOTS Best Practices](https://learn.unity.com/course/dots-best-practices)
  - Use only when scale justifies data-oriented complexity.
  - TWB lesson: a clean deterministic C# grid simulation may be better before DOTS ceremony.
- [Towards Automatic Design of Factorio Blueprints](https://arxiv.org/abs/2310.01505)
- [The Steady-States of Splitter Networks](https://arxiv.org/abs/2404.05472)
  - Use later for procedural layout, blueprint planning, or AI-assisted optimization.
  - TWB lesson: too abstract for first playable Trenchworks gates.

### War / Supply Structure

- [Britannica - Trench Warfare](https://www.britannica.com/topic/trench-warfare)
  - Use for front lines, support lines, communications trenches, dumps, aid stations, kitchens, artillery rear.
  - TWB lesson: war view should show depth: front trench, support trench, reserve/supply routes, rear nodes.
- [Britannica - Military Logistics / Staged Resupply](https://www.britannica.com/topic/logistics-military/Staged-resupply)
- [Army Sustainment Resource Portal](https://cascom.army.mil/asrp/doctrine-pubs.html)
  - Use for staged-resupply structure.
  - TWB lesson: model echelons such as base, depot, forward dump, and trench unit. Show breakdowns as node starvation, route exposure, or transport shortage.
- [RimWorld official site](https://rimworldgame.com/)
  - Use for AI storyteller/directed-pressure framing.
  - TWB lesson: a director can pace pressure from supply health, casualty tempo, and front stability rather than random attacks.

## TWB-Specific Guidance

### Glassroot Garden

- Stay top-down / 3/4 top view.
- Prioritize clean footprints, contact shadows, readable crop stages, uncluttered storage/UI cards, and consistent wall/floor depth.
- Use tile/object references to build contracts before creating more assets.
- Use Phaser/Aseprite references for pet and companion animation playback.

### TWB Trenchworks

- Decide whether each surface is true top-down, 3/4, isometric, or merely iso-inspired before commissioning art.
- Do not mix top-down units with isometric props unless anchor, pivot, sorting, and collision rules are explicit.
- Factory/logistics should start with a readable core loop:
  - resource node
  - transport
  - depot
  - trench consumption
  - front outcome
- Avoid invisible simulation. Supply starvation, route priority, trench connectivity, and enemy pressure must be drawn plainly.
- Do not clone Factorio complexity wholesale. Use the wartime logistics fantasy, not every combinator-shaped temptation.

### Main TWB Unity Game

- Use pixel-art UI and icon resources to keep HoloGlyph/icon systems crisp and consistent.
- Use Unity sprite/atlas import rules for companions, monster icons, inventory icons, and map markers.
- Use top-down animation references before expanding 8-direction combat or companion movement.

### All Lanes

Every future asset brief should state:

- projection
- tile size or grid relationship
- anchor/pivot
- collision footprint
- sorting/depth rule
- light direction
- shadow/contact rule
- palette range
- animation states and frame counts
- engine import path
- QA preview requirements
- source/provenance/license status

## Next Use

When commissioning workers for art, animation, map, or factory-simulation work, include this resource plus [[wiki/game-dev/slynyrd-pixelblog-reference]] in the read-first list.
