# TWB Trenchworks War Unit Sprite Sheets Report

Date: 2026-05-16
Worker: TWB Trenchworks playtest/asset worker
Scope: TWB Trenchworks standalone Unity 2D, war-side soldier/team assets only.

## What Changed

- Created a living-unit animation contract for Trenchworks war squads.
- Formalized a role catalog with primary weapons, secondary purposes, tiers, and standard versus command frame sizes.
- Formalized team templates so the player-facing spawn unit remains a team, not individual soldier micromanagement.
- Generated first-pass sprite sheets for 24 war unit roles.
- Generated both cyan-matte source sheets and transparent Unity-facing sheets.
- Cut each role into individual transparent animation frames.
- Added review keys and action previews for quick visual inspection.
- Updated the war asset master style and output index with the new unit-sheet contract.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-squad-unit-animation-contract-v1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-asset-master-style-v1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-asset-output-index-v1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-soldier-style-reference-v1.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-sprites-v1-key.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-sprites-v1-rifleman-action-preview.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-sprites-v1-command-action-preview.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\war-unit-animation-manifest-v1.json`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\Sheets\Source\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\Sheets\Transparent\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\Frames\`

## Unit Roles Covered

- Patrol Corporal
- Scout
- Rifleman
- Sapper
- Combat Medic
- Quartermaster Runner
- Porter
- Field Engineer
- MG Gunner
- Grenadier
- Signaller
- Artillery Observer
- Trench Marksman
- Wire Cutter
- Trench Mortar Crew
- Shell Runner
- Stretcher Bearer
- Trench Lieutenant
- Pressure Projector Trooper
- Aether Lamp Scout
- Clockwork Trenchhand
- Grave-Salt Warden
- Echo Runner
- Bound Shell Cantor

## Animation Contract

- Standard soldier frame: `128 x 128`, representing `2 x 2` tiles at 64 px per tile.
- Command/officer frame: `128 x 256`, representing `2 x 4` tiles at 64 px per tile.
- Each role sheet has `4` frames per action and `5` action rows.
- Action rows: `walk`, `crouch`, `crawl`, `fire_primary`, `secondary`.
- Standard sheet size: `512 x 640`.
- Command/officer sheet size: `512 x 1280`.

## Tests And Checks Run

- Generated `24` cyan source sheets.
- Generated `24` transparent sheets.
- Generated `480` individual transparent frames.
- Checked transparent sheets for valid sizes: `512 x 640` or `512 x 1280`.
- Checked frame sizes: `128 x 128` or `128 x 256`.
- Checked transparent sheet corners are transparent.
- Checked finished transparent sheets for opaque cyan pixels.
- Validation result: `0` issues.

## Cleanup Performed

- No throwaway files were left in the project tree.
- The raw generated style-reference image was copied into the docs folder; the original under `.codex\generated_images` was preserved as raw generation evidence.

## Risks

- These are first-pass exact-dimension prototype sprites. They are readable and import-safe, but not final painterly art.
- The current sheets are role-based, not faction-duplicated. Enemy variants should be tint/palette swaps unless a later visual pass proves duplication is needed.
- The Unity runtime is not yet wired to use these sheets for actual unit animation.
- The key image uses labels for review only; game-facing sheets contain no text.
- Some expansion roles are not yet implemented in code. They were included so the squad/team art contract does not need to be redone when those squads unlock.

## Memory-Worthy Notes

- Player-facing war spawning should remain team-based. Individual soldiers exist under the hood and in animation, but the player should not manually spawn single soldiers.
- Every soldier role now has a primary weapon and a secondary purpose, matching the user's requested FPS-like role logic while preserving squad-level strategy.
- The current art contract now matches the user's scale decision: base soldier `2 x 2` tiles and command/lieutenant-style figure `2 x 4` tiles at `64 px` per tile.
- First sprite pass favors clean silhouettes, black outlines, and exact frame dimensions over final detail.

## Follow-Up Recommendations

- Review the unit key image in the docs folder and reject any role silhouette that does not read clearly enough.
- Wire only the first-slice roles into Unity first: Patrol Corporal, Scout, Rifleman, Sapper, Combat Medic, Quartermaster Runner, Porter, Field Engineer, and MG Gunner.
- Add a sprite mapping layer from unit role id plus current action/posture to the generated frame paths.
- Add faction tinting after the first runtime import, rather than duplicating the sheet set.
- Add death/wounded/casualty body sprites as a separate marker sheet if the existing casualty markers are not enough.

## Blocked

- No asset-generation blocker.
- Runtime Unity animation wiring was intentionally not part of this pass.

