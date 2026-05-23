# TWB Trenchworks MG Dugout Orientation V1 Art Report

Date: 2026-05-23

## Scope

Standalone TWB-tagged Unity 2D game: TWB Trenchworks.

This pass created directional MG dugout side-bulge overlay art only. It did not edit the raw GPT Pro package, permanent Obsidian wiki, main TWB Unity project, Garden, Alchemy, website/shared platform, or factory-side art.

## What Changed

- Created `MGDugoutOrientation/V1` as a dedicated MG front/rear orientation proof pack.
- Generated 288 transparent 192x192 PNGs:
  - 3 biomes: desert, temperate forest, tropical jungle.
  - 3 tiers: Tier 1 field dugout, Tier 2 timber-reveted dugout, Tier 3 reinforced redoubt.
  - 4 orientations: north, east, south, west.
  - 8 states: blueprint, foundation, under-construction, active-empty, active-claimed, debug-front-arc, damaged, destroyed.
- The pack uses a strict orientation contract:
  - `front_vector` is no man's land and the machine-gun barrel direction.
  - `rear_entry_vector` is the open crew-entry side.
  - The barrel points over the closed parapet.
  - The rear entry remains open with no sandbag cross-wall.
  - The art is a compact side-bulge overlay, not a duplicate long field-trench segment.
- Generated 6 review/contact sheets:
  - active overview
  - desert orientation check
  - east-facing tier 2 state check
  - one per-tier orientation sheet for temperate forest
- Packaged the batch as:
  - `C:\Users\yrred\Downloads\twb-trenchworks-mg-dugout-orientation-v1.zip`
- Updated the Trenchworks asset catalog and current brief.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-art-generation\generate_mg_dugout_orientation_v1.py`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\art-pipeline\10_asset_catalog_twb_trenchworks.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\SolidAssets\MGDugoutOrientation\V1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\mg-dugout-orientation-v1\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-23-twb-trenchworks-mg-dugout-orientation-art-report.md`

## Child Subagent Review

Child subagent Copernicus completed read-only scope QA.

Key recommendations incorporated:

- Proceed with `MGDugoutOrientation/V1`; it is aligned with remaining war-side art gaps.
- Keep it as side-bulge MG dugout modules, not full trench replacements.
- Include north/east/south/west orientations, Tier 1-3 upgrades, and build/damage states.
- Record front-fire direction, operator/rear side, socket points, state, tier, and not-base-trench classification.
- Do not flip front/rear: the barrel faces outward toward enemy/front; operator/access connects back into the trench.
- Do not treat empty MG socket overlays as completed MG nests.

## Checks Run

- `python -m py_compile C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-art-generation\generate_mg_dugout_orientation_v1.py`
- `python C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-art-generation\generate_mg_dugout_orientation_v1.py`
- Mechanical PNG/zip QA:
  - manifest count: 288
  - asset PNG count: 288
  - review PNG count: 6
  - zip asset PNG count: 288
  - zip review PNG count: 6
  - expected runtime canvas: 192x192 only
  - empty-alpha PNGs: 0
  - cyan matte residue pixels: 0
  - magenta matte residue pixels: 0
  - bad classification entries: 0
  - `contains_operator=true` entries: 0
  - barrel/front and crew/rear orientation metadata failures: 0
  - zip includes manifest, README, and generator
- Manual visual review of active overview, orientation check, and state check contact sheets.

Unity Play Mode/F9 was not run. This is art-package complete, not runtime-accepted.

## Cleanup Performed

- Regenerated the output directory cleanly from the script.
- Regenerated the review directory cleanly from the script.
- Corrected the transform convention after QA caught the first generated pass had front/rear metadata inverted. The final generated pack passes the barrel-front/crew-rear check.
- The temporary heartbeat used during child-agent review should be deleted after this report is reviewed.

## Risks

- The pack is not wired to `FrontlineMGSockets/V1`, `HardpointStructures/V1`, or runtime `MachineGunNest` behaviour yet.
- Unity/F9 must still prove anchor, scale, pivot, sorting, trench attachment, socket preservation, muzzle point, crew socket, ammunition state, manning state, and firing arc.
- `active-claimed` includes only a small crew-position indicator, not a rendered soldier; soldiers should still come from the unit renderer.
- Debug-front-arc variants must stay out of normal play.

## Memory-Worthy Notes

- `MGDugoutOrientation/V1` is the first-pass all-orientation completed MG dugout overlay art pack.
- It explicitly fixes the front/rear rule: barrel out over sandbags toward the front, crew entry open to the rear.
- It remains separate from `FrontlineMGSockets/V1`, which is socket-only and contains no barrel/operator.

## Follow-Up Recommendations

- Runtime integration should pair one `MGDugoutOrientation/V1` active-empty asset with one `FrontlineMGSockets/V1` socket at the same zoom and validate all four orientations before exposing functional MG build flow.
- Compare the Tier 1-3 dugout visuals against the existing Tier 1-3 trench overlays and hardpoint structures so upgrade readability remains coherent.
- Keep normal-play art free of `debug-front-arc` variants.
