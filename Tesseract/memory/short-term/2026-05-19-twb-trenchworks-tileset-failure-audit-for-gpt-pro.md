# TWB Trenchworks Tileset Failure Audit For GPT Pro - 2026-05-19

## Scope

Standalone TWB-tagged Unity game: TWB Trenchworks.

This report audits the failed trench tileset/art pipeline attempts made on 2026-05-19. It is written for GPT Pro review. It does not update permanent Obsidian memory.

## Executive Summary

We have failed at the current desert tier1 `field_trench` tileset gate from multiple angles.

The core failure is not cyan cleanup, slicing, or file handling. Those parts worked. The core failure is that we never had a strict enough technical autotile contract before asking image generation to make art. The generator repeatedly produced attractive trench compositions, completed domino-like shapes, or quasi-autotile sheets, but not a reliable reusable rule-based tileset.

The latest evidence shows a clean image can be processed, but processing a clean image is not the same as having a valid autotile grammar. Connected-component slices are visual fragments, not semantic tiles.

The next useful step is not "try another prettier prompt." The next useful step is to define a deterministic autotile contract first: tile size, mask convention, exact tile IDs, neighbor masks, edge connector geometry, atlas layout, validation maps, and rejection criteria.

## What We Tried

### 1. Original one-tile / per-domino direction

The earlier gate focused on a desert tier1 `trench_straight_ns` one-tile proof and related per-domino/per-tile prompt files.

This was superseded because the workflow kept steering image generation toward completed trench pieces instead of reusable tiles.

Deleted or deprecated prompt/spec paths:

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-autotile-tile-prompts\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-autotile-tileset-prompts\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-blueprint-sprite-sheet-prompts\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-trench-autotile-tileset-spec-v1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-trench-blueprint-sprite-pack-v1-spec.md`

### 2. Tileset-first documentation reset

We created a new tileset-first direction:

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-tileset-pipeline-spec-v2.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-tileset-prompts\README.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-tileset-prompts\desert\tier1.md`
- plus biome/tier prompt files for desert, temperate forest, and tropical jungle tiers 1-3.

The new rule was:

- one biome + one tier + one trench family = one reusable tileset
- do not ask for completed dominoes, maps, contact sheets, labelled boards, or assembled trenches
- use the tileset to mechanically construct trench dominoes later

This was directionally correct, but still not enough.

### 3. Prompt attempts using "auto tile template"

The user identified that "auto tile template" was the better phrase. We tried prompts asking for a "desert trench auto tile template" and used a user-provided external example as a shape reference.

This improved the direction but still failed because the generator did not reliably follow the reference structure. It continued producing visual sheets of trench shapes rather than a strict same-size, same-grid semantic tileset.

### 4. First apparently successful cyan-backed source

The user supplied this as the first apparent success:

`C:\Users\yrred\Desktop\ChatGPT Image May 19, 2026, 05_46_27 PM.png`

It was copied into the Trenchworks project as:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\TrenchTilesets\Source\desert\tier1\desert-tier1-field_trench-autotile-template-success-cyan.png`

This image was 1448x1086 and looked much closer to a useful autotile-like template than prior attempts.

### 5. Incorrect deterministic rebuild attempt

I made a wrong turn and rebuilt a normalized proof sheet from scratch. The user correctly rejected this because it was not the supplied image.

That path was abandoned. Rebuilt proof artifacts were removed. The source of truth became only the user-provided image.

### 6. Cyan cleanup of the actual user-provided image

The actual user-provided image was cleaned without redraw, recolor, resize, or reconstruction.

Transparent output:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\TrenchTilesets\Tiles\desert\tier1\field_trench\user_template_cleanup\desert-tier1-field_trench-user-template-transparent.png`

Preview:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\TrenchTilesets\Review\desert\tier1\desert-tier1-field_trench-user-template-transparent-preview.png`

Cleanup QA:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\TrenchTilesets\Review\desert\tier1\desert-tier1-field_trench-user-template-cleanup-qa.json`

QA numbers:

- Source size: 1448x1086
- Removed cyan-family pixels: 1,204,586
- Removed adjacent near-cyan pixels: 4,291
- Remaining opaque cyan-family pixels: 0

This part worked technically.

### 7. Connected-component slicing

The cleaned transparent image was sliced into connected components.

Slice folder:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\TrenchTilesets\Tiles\desert\tier1\field_trench\user_template_slices\`

Slice manifest:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\TrenchTilesets\Tiles\desert\tier1\field_trench\user_template_slices\desert-tier1-field_trench-user-template-slices-manifest.json`

Slice QA:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\TrenchTilesets\Review\desert\tier1\desert-tier1-field_trench-user-template-slices-qa.json`

QA numbers:

- Component count: 92
- Slice-region mismatch pixels: 0
- Visible reassembly mismatch pixels: 0
- Alpha reassembly mismatch pixels: 0
- Remaining opaque cyan-family pixels: 0

This proved the source image could be losslessly cut into visual blobs. It did not prove those blobs were valid autotile cells.

### 8. Domino review sheet and pieced-together preview

We then built two review sheets from 25 of the slices:

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\TrenchTilesets\Review\desert\tier1\desert-tier1-field_trench-domino-review-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\TrenchTilesets\Review\desert\tier1\desert-tier1-field_trench-ingame-preview-sheet.png`

Manifest:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\TrenchTilesets\Review\desert\tier1\desert-tier1-field_trench-review-assembly-manifest.json`

The manifest correctly warned:

- mechanical review assembly only
- not final semantic Unity autotile mapping
- not neighbor-mask contract
- not runtime resolver data

The user rejected these sheets as horrible.

## Why It Failed

### High Finding: We confused cutout success with tileset success

The cleanup and slicing pipeline worked. That was a technical success.

But a transparent image with clean pieces is not automatically a reusable tileset. An autotile set needs semantic rule cells. Each cell must have a declared role and adjacency contract.

Transparency is not adjacency.

### High Finding: Connected-component slicing is the wrong extraction method for autotiles

Connected-component slicing cuts whatever visual blobs are connected after cyan removal. Autotile extraction should cut fixed-size grid cells with known tile IDs and masks.

The 92 slices were not "tiles." They were arbitrary visual components from an irregular generated image.

Autotiles require intentional cells such as:

- empty / isolated
- cap north
- cap east
- cap south
- cap west
- straight north-south
- straight east-west
- four corners
- four T-junctions
- four-way

Each needs fixed dimensions, atlas coordinates, and edge connector geometry.

### High Finding: The generator kept producing composition instead of grammar

The image generator repeatedly made things that looked like:

- completed trench dominoes
- finished trench pieces
- attractive trench modules
- maps or quasi-map layouts
- sprite sheets of already-assembled shapes

It did not reliably produce:

- same-size rule cells
- strict atlas layout
- known neighbor masks
- compatible edge sockets
- a deterministic assembly grammar

Prompt wording alone did not solve this.

### High Finding: We mixed art direction, technical source template, and runtime mapping

The work blurred three separate jobs:

1. Art direction: what desert tier1 field trenches should look like.
2. Technical source template: exact reusable tile cells and grid.
3. Runtime mapping: how Unity chooses tile sprites from trench occupancy.

Trying to get one generated image to solve all three produced attractive but unusable results.

### High Finding: Current docs/memory contain a contradiction

Some older memory still points toward an individual `512x512` `trench_straight_ns` tile gate. The newer Trenchworks worker prompt and v2 tileset docs say that gate is superseded and that per-domino or single completed-piece generation should not be used for final trench art.

GPT Pro should not recommend resuming the old `trench_straight_ns` per-piece path unless it explicitly reframes that tile as a semantic prototype within a broader autotile contract.

## What Is Salvageable

- The strategic pivot away from completed dominoes and toward reusable tilesets is correct.
- The cyan cleanup process is useful and should be preserved.
- The user-provided cyan image can be kept as visual reference.
- The 92 slices prove we can process images cleanly, but they should not be treated as the source tileset.
- The v2 docs are useful as a record of failure modes, but should be amended after GPT Pro resolves the technical contract.

## What To Stop Doing

- Stop generating per-domino art.
- Stop generating completed trench pieces.
- Stop generating maps, sample layouts, contact sheets, or preview assemblies as source assets.
- Stop treating connected components as tiles.
- Stop assembling review sheets from arbitrary visual slices.
- Stop asking for a full 8x8 or 4x4 production sheet before the tile contract exists.
- Stop expanding to 9 biome/tier tilesets before one desert tier1 grammar passes.
- Stop assuming a better prompt alone will fix this.

## Key Technical Questions For GPT Pro

1. What autotile standard should TWB Trenchworks use for trench occupancy?
   - 16-mask cardinal?
   - 47/48-tile blob autotile?
   - Wang tiles?
   - marching squares?
   - Unity RuleTile custom masks?

2. What is the exact minimum tile set for `desert/tier1/field_trench`?
   - tile IDs
   - NESW masks
   - atlas positions
   - required edge signatures

3. What should the canonical tile size be?
   - 256x256?
   - 512x512?
   - something else based on current Trenchworks visual scale?

4. What source-sheet format should be required?
   - transparent vs cyan
   - padding
   - margins
   - labels allowed or separate only
   - one tile per file vs sheet

5. What connector geometry should every tile obey?
   - centerline coordinate
   - channel width
   - wall lip width
   - spoil band width
   - outline behavior at edges

6. Should AI image generation be used for the technical template at all?
   - Or should the first skeleton be hand-authored/programmatic masks, with AI used only for texture/detail overlays?

7. How should Unity validate the result?
   - static preview maps
   - RuleTile asset test
   - programmatic 5x5 maps
   - seam checks
   - runtime resolver tests

8. Can the user-supplied cyan-backed image be remapped into a 16-mask or 48-tile contract?
   - If yes, how exactly?
   - If no, should it be visual reference only?

## Recommended Next Gate

Do not generate another trench image yet.

Next gate:

Create a technical autotile contract for `desert/tier1/field_trench`, including:

- chosen mask convention
- tile size
- exact tile ID table
- NESW masks or equivalent
- atlas layout
- edge connector rules
- rejection criteria
- validation preview maps
- Unity import/mapping contract

Then create a plain semantic blueprint atlas first, using simple masks or flat colors. Test that before applying desert trench art texture.

## Copy-Paste Prompt For GPT Pro

You are advising on a failed game-art pipeline for **TWB Trenchworks**, a standalone Unity 2D trench-war/factory-logistics game. The current target is a reusable `desert/tier1/field_trench` autotile/tileset for top-down trench overlays.

We have repeatedly failed because image generation keeps producing completed trench pieces, dominoes, maps, or attractive shape sheets instead of a reusable autotile grammar. We need your technical guidance before generating more images.

Context:

- The goal is **not** to create completed trench dominoes.
- The goal is **one reusable tileset/autotile contract** that can mechanically construct trench dominoes later.
- We studied Sandro Maglione's pixel tileset guidance: reusable same-size tiles, edge compatibility, basic 16-tile sets for limited shapes, larger 48-ish sets for internal corners/combinations, and variants only after the base set works.
- We created a v2 tileset-first spec and prompts, but they still did not define the technical contract strictly enough.
- We tried the phrase "auto tile template."
- We used an external example of an autotile template as shape reference.
- The generator still failed to reliably follow the reference.
- The user supplied the first seemingly successful cyan-backed desert trench template:
  `C:\Users\yrred\Desktop\ChatGPT Image May 19, 2026, 05_46_27 PM.png`
- That image was cleaned successfully:
  - source size 1448x1086
  - removed 1,204,586 cyan-family pixels
  - removed 4,291 adjacent near-cyan pixels
  - 0 remaining opaque cyan-family pixels
- It was sliced into 92 connected components with:
  - 0 slice-region mismatches
  - 0 visible reassembly mismatches
  - 0 alpha mismatches
  - 0 remaining opaque cyan-family pixels
- However, building domino review sheets from those slices looked horrible and was rejected.

Our diagnosis:

- Cyan cleanup worked.
- Pixel-preserving slicing worked.
- But connected-component slicing is the wrong model for autotiles.
- We confused clean visual fragments with semantic rule cells.
- We need a deterministic autotile contract before generating more art.

Please provide:

1. The best autotile/mapping standard for this use case:
   - 16-cardinal NESW masks?
   - 47/48-tile blob autotile?
   - Wang tiles?
   - marching squares?
   - Unity RuleTile custom masks?
   Explain the recommendation and tradeoffs for top-down trenches.

2. A complete first-pass `desert/tier1/field_trench` technical contract:
   - canonical tile size
   - exact tile IDs
   - neighbor masks
   - atlas layout
   - edge connector geometry
   - channel width
   - wall-lip/spoil-band continuity rules
   - transparent/cyan source rules
   - what is allowed and forbidden inside each tile

3. A minimal validation plan:
   - which preview maps to build
   - how to detect seams, doubled rims, bad openings, incompatible channels
   - when to reject a generated sheet

4. A recommendation on whether image generation should create:
   - one tile at a time
   - a blank labelled template first
   - a full sheet
   - only texture overlays after a programmatic/hand-authored mask skeleton exists

5. A strict next image-generation prompt or set of prompts that prevents the model from making completed dominoes, maps, sample layouts, or decorative shape sheets.

6. A recommendation on whether the existing cyan-backed image should be:
   - remapped into the contract
   - used only as visual reference
   - discarded

Please do not recommend "just prompt harder," a full production sheet, more per-domino images, or using connected components as the source tileset. We need a technical contract and next gate that can actually pass.

## Audit Result

The strongest recommendation is:

1. Stop art generation.
2. Define a 16-mask semantic blueprint atlas first.
3. Validate it mechanically.
4. Only then apply desert trench art style.
5. Expand to 48 tiles or variants only after the base grammar works.

