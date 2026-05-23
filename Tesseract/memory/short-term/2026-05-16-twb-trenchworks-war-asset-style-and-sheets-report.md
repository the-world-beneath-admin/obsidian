# TWB Trenchworks War Asset Style And Sheets Report

Date: 2026-05-16
Scope: standalone TWB Trenchworks Unity 2D project, war-side assets only.

## What changed

- Created a reusable war-side master style document for future image generation prompts.
- Generated cyan-matte war-side asset sheets.
- Removed cyan matte and cyan-to-black fringe from processed sheets and cutouts.
- Cut the canonical working sheets into individual PNG assets.
- Created labelled preview keys for human review.
- Split the overcrowded combined units/effects sheet into cleaner working sheets.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-asset-master-style-v1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-asset-output-index-v1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-trench-tiles-v1-key.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-terrain-cover-v1-key.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-units-emplacements-v1-key.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-fx-markers-v1-key.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Sheets\Source\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Sheets\Transparent\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Sheets\Normalized64\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Cutouts\`

## Sheets created

Canonical working sheets:

- `war-trench-tiles-v1`: 24 cutouts.
- `war-terrain-cover-v1`: 24 cutouts.
- `war-units-emplacements-v1`: 16 cutouts.
- `war-fx-markers-v1`: 12 cutouts.

Reference-only sheet:

- `war-units-weapons-fx-v1`: kept as reference, but not preferred because the generated layout overcrowded the lower row.

## Tests/checks run

- Viewed generated source sheets before processing.
- Ran cyan matte cleanup on all generated war sheets.
- Re-ran cleanup after validation found a small number of fringe pixels in resized cutouts.
- Scanned all non-source PNGs under `Assets\Art\War\` for remaining cyan-ish opaque pixels.
- Final result: `0` remaining cyan-ish opaque pixels.
- Counted cutout PNGs under `Assets\Art\War\Cutouts\`: `148`, including canonical and reference cutouts.

No Unity compile was run because this pass only added image/doc assets and did not change C# or scenes.

## Cleanup performed

- No temporary scripts were left behind.
- The original generated images under `.codex\generated_images` were left in place as required.
- The rejected/overcrowded combined sheet was not deleted; it is documented as reference-only so it does not masquerade as the preferred sheet.

## Risks

- These are first-pass generated assets and need visual acceptance before renderer wiring.
- The trench sheet is much closer to pathing-role tiles, but it still needs review in Unity scale before becoming the final trench grammar.
- The units are readable as concepts, but final unit sprites may need larger footprint-specific sheets for 2x2 soldiers and 2x4 command units.
- The FX sheet includes some bright effects; tone may need darkening once seen in the live battlefield.

## Memory-worthy notes

- War-side assets now have a master style prompt and a cyan-matte cleanup process.
- The chosen direction is dark, gritty, hand-painted tactical war art.
- The production/mining side should get its own lighter style document later rather than being mixed into war sheets.
- Trench art must be authored as separate pathing-role tiles, not as one wide-looking trench sprite.

## Follow-up recommendations

- Review the four key PNGs first.
- If accepted, wire only the terrain and trench sheets into a non-destructive preview layer in Unity.
- Keep production-side assets for a later separate style pass with a lighter mining/factory tone.
- Consider a second trench sheet dedicated only to cleaner wall/floor/corner topology after the current visual direction is approved.

## Anything blocked

- Final wiring into the live war renderer is blocked on user visual approval of the sheets.
