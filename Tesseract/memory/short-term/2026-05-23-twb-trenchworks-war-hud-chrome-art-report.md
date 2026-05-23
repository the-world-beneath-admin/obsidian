# TWB Trenchworks War HUD Chrome V1 Art Report

Date: 2026-05-23

## Scope

Standalone TWB-tagged Unity 2D game: TWB Trenchworks.

This pass created player-facing war-mode HUD/UI chrome candidates only. It did not edit the raw GPT Pro package, permanent Obsidian wiki, main TWB Unity project, Garden, Alchemy, website/shared platform, or factory-side art.

## What Changed

- Created `WarHUDChrome/V1` as the next war-side art batch.
- Generated 440 transparent runtime PNGs:
  - 12 HUD panel/shell sprites.
  - 288 button sprites across 12 roles, 6 states, and 4 sizes.
  - 90 gauge sprites across 6 gauge roles, 3 widths, and 5 fill levels.
  - 32 weapon/unit-role silhouettes across 16 roles and 2 sizes.
  - 10 tier-tree control sprites.
  - 8 status-chip sprites.
- Generated 4 review/contact sheets:
  - panels
  - button state samples
  - weapon and role silhouettes
  - gauges, tier-tree controls, and status chips
- Packaged the batch as:
  - `C:\Users\yrred\Downloads\twb-trenchworks-war-hud-chrome-v1.zip`
- Updated the Trenchworks asset catalog and current brief to record the pack and runtime caveats.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-art-generation\generate_war_hud_chrome_v1.py`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\art-pipeline\10_asset_catalog_twb_trenchworks.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\UI\WarHUDChrome\V1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\war-hud-chrome-v1\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-23-twb-trenchworks-war-hud-chrome-art-report.md`

## Child Subagent Review

Child subagent Epicurus completed read-only QA/spec support.

Key recommendations incorporated:

- Keep this pack scoped as final player-facing HUD/UI chrome.
- Do not duplicate `CommandAndMapMarkers/V1`, which owns world overlays, war-map markers, minimap pips, route masks, and debug plan markers.
- Do not duplicate `CombatFeedback/V1`, which owns muzzle flashes, impacts, suppression/casualty/bombardment feedback, and burst VFX.
- Include button states, HUD panels, tier controls, status strips/chips, and weapon/unit silhouettes.
- Record that Unity/F9 still needs to prove UI scale, readability, canvas layer, state switching, and packaged-build-safe loading.

## Checks Run

- `python -m py_compile C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-art-generation\generate_war_hud_chrome_v1.py`
- `python C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-art-generation\generate_war_hud_chrome_v1.py`
- Mechanical PNG/zip QA:
  - manifest count: 440
  - asset PNG count: 440
  - review PNG count: 4
  - zip asset PNG count: 440
  - zip review PNG count: 4
  - empty-alpha PNGs: 0
  - cyan matte residue pixels: 0
  - magenta matte residue pixels: 0
  - zip includes manifest, README, and generator
- Manual visual review of the panel, button, silhouette, and control contact sheets.

Unity Play Mode/F9 was not run. This is art-package complete, not runtime-accepted.

## Cleanup Performed

- Regenerated the output directory cleanly from the script.
- Regenerated the review directory cleanly from the script.
- Corrected the contact-sheet preview scaling so oversized panels do not overlap review cells.
- The temporary heartbeat used during the child-agent review should be deleted after this report is reviewed.

## Risks

- HUD sprites still need Unity UI anchoring and scaling validation.
- Panel shells may need nine-slice import settings before they are suitable for stretched runtime panels.
- Weapon silhouettes should be compared against accepted soldier/emplacement art before final UI acceptance.
- This pack does not solve factory-side UI icons.
- This pack does not solve runtime integration or packaged-build-safe icon loading.

## Memory-Worthy Notes

- `WarHUDChrome/V1` is now the first-pass final non-IMGUI war HUD chrome candidate pack.
- `WarHUDChrome/V1` should remain separate from `CommandAndMapMarkers/V1`, `CombatFeedback/V1`, and `PersistentMoraleVFX/V1`.
- Treat this as player-facing UI art, not solid assets, world-space markers, combat VFX, soldier sprites, or factory-side UI.

## Follow-Up Recommendations

- Next war-side art gap should be chosen from the updated catalog, not assumed from memory.
- Runtime UI follow-up should prove the HUD over the map at the current accepted max zoom, with bottom buttons and tracker/minimap toggles using these sprites.
- Keep debug/F9/hidden-plan iconography separate from normal HUD chrome.
