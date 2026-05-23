# TWB Unity Icon Asset Audit Report - 2026-05-15

## Scope

Main game / The World Beneath.

## Task

Audit live Unity content definitions against existing HoloGlyph icon assets for materials, catalysts, skills, and modifiers. Identify what still needs icon creation and break it into practical production sheets.

## Result

The live material, catalyst, shared skill, modifier, and currency icon sets are already covered by `1024x1024` PNGs under `Assets/Resources/GameArt/TWB_HoloGlyph_T1/Icons`.

Required new icon work is narrow: six special starter skill icons are missing. These should be produced as one starter-skill sheet.

There are also three legacy compatibility material item definitions without icons: `mat_low`, `mat_iron`, and `mat_high`. These are explicitly described in the item registry as compatibility-only legacy materials, not part of the live material economy. Recommendation: do not spend art time on them unless a later UI audit proves they are still intentionally player-visible.

## Coverage Summary

| Set | Live definitions | Existing icons | Missing |
| --- | ---: | ---: | ---: |
| Currency | 1 | 1 | 0 |
| Materials | 135 | 135 | 0 |
| Catalysts | 140 | 140 | 0 |
| Shared attack skills | 37 | 37 | 0 |
| Shared defense skills | 37 | 37 | 0 |
| Shared utility skills | 37 | 37 | 0 |
| Special starter skills | 6 | 0 | 6 |
| Modifiers | 20 | 20 | 0 |

Icon file QA found `0` audited PNGs with non-1024 dimensions or missing `.meta` files.

No orphan/extra icon PNGs were found in the audited folders.

## Required Creation Sheet

### Sheet 1 - Special Starter Skill Icons

Recommended sheet name: `TWB_HoloGlyph_T1_StarterSkillIcons_Sheet01`

Recommended sheet layout: 3 columns x 2 rows source sheet, with labelled slots in the production prompt and final exports as individual transparent `1024x1024` icons.

Use the existing HoloGlyph icon lane: cyan/teal sci-fi glyph form, orange accent detail, no letters, no numbers, no readable text, transparent final PNG, dark/light QA contact sheets before import.

| Slot | Output folder | Asset filename | Display name | Family |
| ---: | --- | --- | --- | --- |
| 1 | `SkillUtility` | `utilskill_special_peggy_threshold_ward_icon_1024.png` | Peggy's Threshold Ward | Faith utility |
| 2 | `SkillAttack` | `atkskill_special_stanly_prancing_bite_icon_1024.png` | Stanly's Prancing Bite | Might attack |
| 3 | `SkillDefense` | `defskill_special_nova_porchline_stand_icon_1024.png` | Nova's Porchline Stand | Faith defense |
| 4 | `SkillAttack` | `atkskill_special_merlin_chitter_pounce_icon_1024.png` | Merlin's Chitter Pounce | Cunning attack |
| 5 | `SkillUtility` | `utilskill_special_hazel_safe_cut_icon_1024.png` | Hazel's Safe Cut | Cunning utility |
| 6 | `SkillDefense` | `defskill_special_chuck_porch_sentinel_icon_1024.png` | Chuck's Porch Sentinel | Might defense |

## Optional / Not Recommended Sheet

### Sheet 2 - Legacy Material Compatibility Icons

Only produce this if the legacy material cards are intentionally retained in player-facing UI:

| Slot | Output folder | Asset filename | Display name |
| ---: | --- | --- | --- |
| 1 | `Materials` | `mat_low_icon_1024.png` | Low Potency Material |
| 2 | `Materials` | `mat_iron_icon_1024.png` | Iron |
| 3 | `Materials` | `mat_high_icon_1024.png` | High Potency Material |

Recommendation: audit UI visibility or decommission/migrate these before creating art.

## If A Full Refresh Is Desired Later

This is not required for missing coverage, but if the team chooses to regenerate all icons for style consistency, break the refresh into these sheet batches rather than one enormous sheet:

| Refresh lane | Count | 16-slot sheets |
| --- | ---: | ---: |
| Materials | 135 | 9 |
| Catalysts | 140 | 9 |
| Attack skills | 39 including special starters | 3 |
| Defense skills | 39 including special starters | 3 |
| Utility skills | 39 including special starters | 3 |
| Modifiers | 20 | 2 |
| Currency | 1 | Fold into material review or keep separate |

I would not recommend a full refresh yet. The existing files are complete by coverage and format; the proper next production move is the one special-starter skill sheet.

## Files Touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-15-twb-unity-icon-asset-audit-report.md`

## Checks Run

- Read `memory/hot.md`, `memory/index.md`, `memory/wiki/game-dev/project-hierarchy.md`, and `memory/wiki/twb-unity/ui-hologlyph-style.md`.
- Parsed `LootLibraryCatalog.cs` for live currency/material/catalyst IDs.
- Parsed attack, defense, and utility skill catalogs plus `StarterPetCatalog.cs` for shared and starter skill IDs.
- Parsed modifier definition files for live modifier IDs.
- Compared required IDs against `Assets/Resources/GameArt/TWB_HoloGlyph_T1/Icons`.
- Checked audited icon PNG dimensions and `.meta` presence.

No Unity build was run because this pass changed only the task brief and this report.

## Cleanup Performed

No temporary files were created.

## Risks

- This audit verifies file coverage, naming, dimensions, and `.meta` presence. It does not visually grade the existing icons.
- The actual UI may still need a generic icon resolver/wiring pass if any item surfaces are not loading these existing Resources assets.
- Legacy materials remain defined for compatibility; creating icons for them without a product decision could preserve old content that should instead disappear.

## Memory-Worthy Notes

- Live material, catalyst, shared skill, modifier, and currency icon coverage is complete by asset presence.
- The six special starter skill icons are the only missing live player-facing icons in the audited scope.
- Legacy materials `mat_low`, `mat_iron`, and `mat_high` are compatibility-only and should not automatically receive new art.

## Follow-Up Recommendation

Generate and import `TWB_HoloGlyph_T1_StarterSkillIcons_Sheet01`, then do a narrow UI smoke pass over Archive/Card Summary/Dungeon selection to confirm skill icon loading on special starter companion cards.
