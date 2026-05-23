# SLYNYRD Pixelblog Reference

## Purpose

Reference source for top-down, 3/4 top-view, isometric, tile, animation, object, terrain, and pixel-art production decisions across The World Beneath, Glassroot Garden, TWB Trenchworks, and future World Keys.

Primary source: [SLYNYRD Pixelblog Catalogue](https://www.slynyrd.com/pixelblog-catalogue), by Raymond Schlitter.

## Copyright Boundary

Use this page as a learning and production reference, not as an asset mirror.

- Do not copy SLYNYRD article text into TWB docs beyond brief citation snippets.
- Do not download, rehost, trace, recolor, or ship SLYNYRD images/assets without permission or a valid purchased/download license.
- Use source links to inspect the tutorial images in context.
- Store TWB-specific derivative rules, checklists, and conclusions here.
- If an artist needs a visual, send them to the linked source post and require original TWB art output.

## Highest-Value TWB Lessons

### Perspective And Grid

- Decide projection before asset production. Top-down, 3/4 top-view, and isometric assets do not share the same collision, readability, or animation assumptions.
- Isometric art benefits from consistent 2:1 diagonal rules, fixed scale, fixed light direction, and repeated reusable clusters.
- Isometric is excellent for readable buildings, machines, and dimensional factory pieces, but it is harder for direct/twitch control and precise player movement.
- Top-down 3/4 view is the better default for Garden-style interaction, RPG movement, pets, plants, interiors, and object-heavy rooms.
- Asset dimensions should respect the game grid even when sprites are not literally tile-sized. A sprite that visually matches the grid is easier to place, animate, and collide.

### Top-Down Characters

- Four-facing characters can still move diagonally; this is cheaper and can work if attack arcs, tools, and enemy design respect the limitation.
- Eight-direction characters demand more animation, more consistency checking, and more combat/level design to justify the extra directionality.
- Build rough orientations first, compare them together, then test them as a rotation before polishing.
- Symmetric designs can reduce workload through flipping; asymmetric gear, hair, shields, or weapons may require all eight views.
- Small sprites need simplified costumes. A design that looks good in one still frame can become unreadable noise once animated.

### Animation

- Compare all directions side by side while animating; do not polish one direction in isolation.
- Idle/run/attack clarity comes from anatomy consistency, silhouette, head/body bob, readable extremities, and timing variation.
- Six-frame cycles are a useful economy target for compact top-down run animations.
- Variable frame timing usually feels better than a perfectly even mechanical loop.
- Weapon attacks should separate anticipation, strike/smear, follow-through, and recovery.
- Smears should emphasize the committed strike path, not every fast movement.
- Weapon weight can be communicated through frame timing, longer holds, impact frames, and optional shake/rebound cues.

### Tiles, Objects, And Rooms

- Build tiles as systems: base texture, edge cases, transitions, variants, detail overlays, and repeating-cluster control.
- Top-down environments need object-shadow and contact-shadow rules early so props feel grounded.
- Interior rooms need a clear wall/floor/depth convention before furniture and UI overlays multiply.
- Trees, plants, rocks, walls, doors, water, food, and item icons should each have modular style rules, not one-off isolated art.
- Variant density is production-critical: too few variants look tiled; too many ungoverned variants become noisy.

### TWB Project Applications

- Glassroot Garden: prioritize posts on top-down tiles, objects, plants, farm scenes, interiors, UI, items, water, wind, and top-down character/pet animation.
- TWB Trenchworks: prioritize isometric basics, isometric mecha tactics, city builder, bricks/walls/doors, tiny sci-fi pixels, military shmup, and top-down tiles.
- Main TWB Unity game: prioritize top-down characters, attacks, items, UI, dungeon tiles, sci-fi RPG, 8-bit adventure, light/shadow, palettes, and texture.
- Future World Keys: use the full catalogue as a style reference library, but always create original TWB art contracts and source assets.

## Priority Reading Sets

### Garden / World Key Farming

- [20 - Top Down Tiles](https://www.slynyrd.com/blog/2019/8/27/pixelblog-20-top-down-tiles)
- [21 - Top Down Objects](https://www.slynyrd.com/blog/2019/9/18/pixelblog-21-top-down-objects)
- [22 - Top Down Character Sprites](https://www.slynyrd.com/blog/2019/10/21/pixelblog-22-top-down-character-sprites)
- [34 - On The Farm](https://www.slynyrd.com/blog/2021/10/24/pixelblog-34-on-the-farm)
- [35 - Top Down Interiors](https://www.slynyrd.com/blog/2021/11/30/pixelblog-35-top-down-interiors)
- [44 - Top Down Trees](https://www.slynyrd.com/blog/2023/5/22/pixelblog-44-top-down-trees)
- [55 - Top Down Character Animation](https://www.slynyrd.com/blog/2025/3/24/pixelblog-55-top-down-character-animation)
- [56 - Top Down Character Attack Animation](https://www.slynyrd.com/blog/2025/5/23/pixelblog-56-top-down-character-attack-animation)
- [58 - Top Down Character Animation Part 3](https://www.slynyrd.com/blog/2025/10/2/pixelblog-58-top-down-character-animation-part-3)

### Trenchworks / Factory War Game

- [4 - Graphical Projection Part 2](https://www.slynyrd.com/blog/2018/4/12/pixelblog-4-graphical-projection-part-2)
- [41 - Isometric Pixel Art](https://www.slynyrd.com/blog/2022/11/28/pixelblog-41-isometric-pixel-art)
- [54 - More Isometric Pixels](https://www.slynyrd.com/blog/2025/1/23/pixelblog-54-isometric-pixel-art)
- [61 - Isometric Mecha Tactics](https://www.slynyrd.com/blog/2026/4/1/pixelblog-61-isometric-mecha-tactics)
- [51 - City Builder](https://www.slynyrd.com/blog/2024/7/25/pixelblog-51-city-builder)
- [45 - Bricks, Walls, Doors, and More](https://www.slynyrd.com/blog/2023/7/21/pixelblog-45-bricks-walls-doors-and-more)
- [59 - Tiny Sci-Fi Pixels](https://www.slynyrd.com/blog/2025/11/28/pixelblog-59-tiny-sci-fi-pixels)
- [48 - Military Shmup](https://www.slynyrd.com/blog/2024/1/23/pixelblog-48-military-shmup)

### General Pixel Art Foundation

- [1 - Color Palettes](https://www.slynyrd.com/blog/2018/1/10/pixelblog-1-color-palettes)
- [2 - Texture](https://www.slynyrd.com/blog/2018/2/15/pixelblog-2-texture)
- [3 - Graphical Projection Part 1](https://www.slynyrd.com/blog/2018/3/14/pixelblog-3-graphical-projections-1)
- [5 - Back to the Basics](https://www.slynyrd.com/blog/2018/5/16/pixelblog-5-back-to-basics)
- [6 - Light and Shadow](https://www.slynyrd.com/blog/2018/6/15/pixelblog-6-light-and-shadow)
- [7 - Developing Style](https://www.slynyrd.com/blog/2018/7/14/pixelblog-7-developing-style)
- [8 - Intro to Animation](https://www.slynyrd.com/blog/2018/8/19/pixelblog-8-intro-to-animation)
- [26 - UX/UI Design Basics](https://www.slynyrd.com/blog/2020/2/23/pixelblog-26-uxui-design-basics)

## Production Checklists

### Top-Down Sprite Contract

- State facing count: 4-way, 5-source-with-flips, or full 8-way.
- State grid relationship: tile size, footprint, anchor, shadow/contact point, and collision footprint.
- Require a rotation/side-by-side consistency check before polish.
- Require silhouette testing on light and dark backgrounds.
- Require motion timing notes for idle, walk/run, attack, tool-use, and hit/react states.
- Keep costume complexity below the readability limit for the final sprite size.

### Tile And Object Contract

- Define projection, tile size, and light direction first.
- Require base, edge, corner, transition, and variant tiles where applicable.
- Require contact shadows or grounding pixels for loose props.
- Keep object scale consistent with characters and doors.
- Add visual-noise QA: repeated clusters, outline clutter, accidental tangents, and unclear walkable boundaries.

### Isometric Contract

- Confirm whether the project is truly isometric or only uses isometric-looking props inside a top-down game.
- Define 2:1 diagonal line rules and pixel grid before production.
- Define height steps, ramps, occlusion, selectable bounds, and click/collision footprint.
- Avoid committing to real-time precision control in iso until input feel is proven.
- Reuse clusters deliberately for efficiency, but break repetition with controlled variants.

## Full Catalogue Index

Use category as a TWB reading priority, not as a judgment of article quality.

| # | Post | TWB Use |
|---|---|---|
| 61 | [ISOMETRIC MECHA TACTICS](https://www.slynyrd.com/blog/2026/4/1/pixelblog-61-isometric-mecha-tactics) | Trenchworks: iso units, machines, battlefield props |
| 60 | [Side View Run N Gun](https://www.slynyrd.com/blog/2026/1/26/side-view-run-n-gun) | Animation reference; side-view only |
| 59 | [Tiny Sci-Fi Pixels](https://www.slynyrd.com/blog/2025/11/28/pixelblog-59-tiny-sci-fi-pixels) | Trenchworks/UI: tiny tile readability |
| 58 | [Top Down Character Animation Part 3](https://www.slynyrd.com/blog/2025/10/2/pixelblog-58-top-down-character-animation-part-3) | Garden/main-game: top-down run/attack continuation |
| 57 | [Knights, Monsters, & Castles](https://www.slynyrd.com/blog/2025/7/28/pixelblog-57-knights-monsters-amp-castles) | Fantasy creature/building reference |
| 56 | [Top Down Character Attack Animation](https://www.slynyrd.com/blog/2025/5/23/pixelblog-56-top-down-character-attack-animation) | Main-game: 8-way melee/tool-use timing |
| 55 | [Top Down Character Animation](https://www.slynyrd.com/blog/2025/3/24/pixelblog-55-top-down-character-animation) | Main-game/Garden: 8-way character animation process |
| 54 | [More Isometric Pixels](https://www.slynyrd.com/blog/2025/1/23/pixelblog-54-isometric-pixel-art) | Trenchworks: iso buildings, props, trees |
| 53 | [Punches and Kicks](https://www.slynyrd.com/blog/2024/11/25/pixelblog-53-punches-and-kicks) | Combat animation reference |
| 52 | [Idle Fighting Stance](https://www.slynyrd.com/blog/2024/9/26/pixelblog-52-idle-fighting-stance) | Combat idle timing |
| 51 | [City Builder](https://www.slynyrd.com/blog/2024/7/25/pixelblog-51-city-builder) | Trenchworks: grid-based build readability |
| 50 | [Human Walk Cycle](https://www.slynyrd.com/blog/2024/5/24/pixelblog-50-human-walk-cycle) | Human movement anatomy reference |
| 49 | [Realistic Human Anatomy](https://www.slynyrd.com/blog/2024/3/25/pixelblog-49-realistic-human-anatomy) | Proportion reference before stylization |
| 48 | [Military Shmup](https://www.slynyrd.com/blog/2024/1/23/pixelblog-48-military-shmup) | Trenchworks: military silhouettes, vehicles, effects |
| 47 | [Tiny Pixels](https://www.slynyrd.com/blog/2023/11/26/pixelblog-47-tiny-pixels) | Low-resolution readability reference |
| 46 | [Anti-Gravity Racers](https://www.slynyrd.com/blog/2023/9/25/pixelblog-46-anti-gravity-racing-scene) | Parallax and scene-motion reference |
| 45 | [Bricks, Walls, Doors, and More](https://www.slynyrd.com/blog/2023/7/21/pixelblog-45-bricks-walls-doors-and-more) | Main-game/Trenchworks: walls, doors, dungeons |
| 44 | [Top Down Trees](https://www.slynyrd.com/blog/2023/5/22/pixelblog-44-top-down-trees) | Garden: modular tree and foliage process |
| 43 | [Top Down Tiles Part 2](https://www.slynyrd.com/blog/2023/3/26/pixelblog-43-top-down-tiles-part-2) | Garden/main-game: richer tile layers and variants |
| 42 | [Cyberpunk Pixel Art](https://www.slynyrd.com/blog/2023/1/30/pixelblog-42-cyberpunk-pixel-art) | Neon/sci-fi atmosphere reference |
| 41 | [Isometric Pixel Art](https://www.slynyrd.com/blog/2022/11/28/pixelblog-41-isometric-pixel-art) | Trenchworks: iso basics through mech/building forms |
| 40 | [3D Pixel Art Animation](https://www.slynyrd.com/blog/2022/9/25/pixelblog-40-3d-animation) | Special animation reference |
| 39 | [Sci-fi RPG](https://www.slynyrd.com/blog/2022/7/24/pixelblog-39-sci-fi-rpg) | Main-game: RPG sprites, portraits, sci-fi dungeon tiles |
| 38 | [Metroid Study](https://www.slynyrd.com/blog/2022/5/24/pixelblog-38-metroid-study) | Enemy/environment readability reference |
| 37 | [Castlevania Study](https://www.slynyrd.com/blog/2022/3/19/pixelblog-37-classic-castlevania-study) | Gothic/dungeon mood reference |
| 36 | [8-Bit Adventure](https://www.slynyrd.com/blog/2022/1/25/pixelblog-36-8-bit-adventure) | Adventure characters and environments |
| 35 | [Top Down Interiors](https://www.slynyrd.com/blog/2021/11/30/pixelblog-35-top-down-interiors) | Garden/main-game: rooms, furniture, cozy interiors |
| 34 | [On The Farm](https://www.slynyrd.com/blog/2021/10/24/pixelblog-34-on-the-farm) | Garden: farm subject matter and props |
| 33 | [Wind Effects](https://www.slynyrd.com/blog/2021/7/16/pixelblog-33-wind-effects) | Garden: subtle environment motion |
| 32 | [Shmup Design Part 2](https://www.slynyrd.com/blog/2021/2/15/pixelblog-32-shmup-design-part-2) | Projectile, pickup, and effect reference |
| 31 | [Shmup Design Part 1](https://www.slynyrd.com/blog/2020/12/14/pixelblog-31-shmup-sprite-design) | Sprite/effect design reference |
| 30 | [Food](https://www.slynyrd.com/blog/2020/9/30/pixelblog-30-food) | Garden/Alchemy item icon reference |
| 29 | [Anime Faces and Hair](https://www.slynyrd.com/blog/2020/7/28/pixelblog-29-anime-faces-and-hair) | Portrait/hair reference |
| 28 | [Side View Tiles](https://www.slynyrd.com/blog/2020/5/21/pixelblog-28-side-view-tiles) | Side-view tile reference; not primary TWB projection |
| 27 | [Under the Sea](https://www.slynyrd.com/blog/2020/3/24/pixelblog-27-under-the-sea) | Biome/plant-like form reference |
| 26 | [UX/UI Design Basics](https://www.slynyrd.com/blog/2020/2/23/pixelblog-26-uxui-design-basics) | HUD bars, gauges, item UI readability |
| 25 | [Motion Cycles](https://www.slynyrd.com/blog/2020/1/23/pixelblog-25-motion-cycles) | Creature/human motion study |
| 24 | [ITEMS](https://www.slynyrd.com/blog/2019/12/21/pixelblog-24-items) | Inventory, loot, and item animation |
| 23 | [Parallax Scrolling](https://www.slynyrd.com/blog/2019/11/12/pixelblog-23-parallax-scrolling) | Background depth and loop reference |
| 22 | [Top Down Character Sprites](https://www.slynyrd.com/blog/2019/10/21/pixelblog-22-top-down-character-sprites) | Early top-down character/pet sprite reference |
| 21 | [Top Down Objects](https://www.slynyrd.com/blog/2019/9/18/pixelblog-21-top-down-objects) | Garden/main-game props and object grounding |
| 20 | [Top Down Tiles](https://www.slynyrd.com/blog/2019/8/27/pixelblog-20-top-down-tiles) | Core Garden/main-game tile reference |
| 19 | [Mecha Mania](https://www.slynyrd.com/blog/2019/7/23/pixelblog-19-mecha-mania) | Trenchworks unit silhouette reference |
| 18 | [Age of Flight](https://www.slynyrd.com/blog/2019/6/18/pixelblog-18-age-of-flight) | Vehicles/clouds/sky reference |
| 17 | [Human Anatomy](https://www.slynyrd.com/blog/2019/5/21/pixelblog-17-human-anatomy) | Anatomy foundation |
| 16 | [Medieval Fantasy](https://www.slynyrd.com/blog/2019/4/23/pixelblog-16-medieval-fantasy) | Fantasy props/creatures/buildings |
| 15 | [Plant Life](https://www.slynyrd.com/blog/2019/3/7/pixelblog-15-plant-life) | Garden plants, crop silhouettes, leaves |
| 14 | [Cityscapes](https://www.slynyrd.com/blog/2019/2/23/pixelblog-14-cityscapes) | Architecture silhouette reference |
| 13 | [Rocks](https://www.slynyrd.com/blog/2019/1/22/pixelblog-13-rocks) | Terrain, cave, and node art |
| 12 | [to the Stars](https://www.slynyrd.com/blog/2018/12/12/pixelblog-12-to-the-stars) | Space/celestial UI reference |
| 11 | [Landscape Pixeling](https://www.slynyrd.com/blog/2018/11/16/pixelblog-11-landscape-pixeling) | Natural depth and horizon reference |
| 10 | [Water in Motion](https://www.slynyrd.com/blog/2018/10/12/pixelblog-10-water-in-motion) | Garden wells, water, liquids, Alchemy fluids |
| 9 | [Melee Attacks](https://www.slynyrd.com/blog/2018/9/8/pixelblog-9-melee-attacks) | Basic melee timing |
| 8 | [Intro to Animation](https://www.slynyrd.com/blog/2018/8/19/pixelblog-8-intro-to-animation) | Animation fundamentals |
| 7 | [Developing Style](https://www.slynyrd.com/blog/2018/7/14/pixelblog-7-developing-style) | Style consistency reference |
| 6 | [Light and Shadow](https://www.slynyrd.com/blog/2018/6/15/pixelblog-6-light-and-shadow) | Shared lighting rules |
| 5 | [Back to the Basics](https://www.slynyrd.com/blog/2018/5/16/pixelblog-5-back-to-basics) | Pixel-art fundamentals |
| 4 | [Graphical Projection Part 2](https://www.slynyrd.com/blog/2018/4/12/pixelblog-4-graphical-projection-part-2) | Isometric projection primer |
| 3 | [Graphical Projection Part 1](https://www.slynyrd.com/blog/2018/3/14/pixelblog-3-graphical-projections-1) | Projection choice primer |
| 2 | [Texture](https://www.slynyrd.com/blog/2018/2/15/pixelblog-2-texture) | Texture and material rules |
| 1 | [Color Palettes](https://www.slynyrd.com/blog/2018/1/10/pixelblog-1-color-palettes) | Palette construction reference |

## Next Use

When commissioning new pixel-art or sprite workers, include this note as a read-first reference only. Workers should extract principles and create original TWB art, not copy SLYNYRD assets.
