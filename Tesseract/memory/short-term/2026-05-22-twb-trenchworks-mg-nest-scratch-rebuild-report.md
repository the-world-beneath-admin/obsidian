# TWB Trenchworks MG Nest Scratch Rebuild Report

Date: 2026-05-22
Worker: TWB Trenchworks standing worker
Scope: Standalone TWB-tagged game: TWB Trenchworks only

## Summary

Recreated the ProceduralV1 MG nest built and blueprint images from scratch after Bob clarified that the previous issue was not a compass flip. The correct contract is: no-man's-land is north/top, sandbags form only the front firing lip, the rear/south side remains open for soldier entry, and the machine-gun barrel projects north over the sandbag lip from an internal receiver/tripod.

## Child Subagent

- Child agent: `019e503f-d46f-7ef3-abd3-f0bc083d8787`
- Heartbeat: `twb-trenchworks-mg-nest-scratch-rebuild-heartbeat`, created during child work and deleted after review.
- Child scope: recreate MG nest art and generator contract only; no raw package edits, permanent memory edits, staging, commits, or broad cleanup.

## What Changed

- Updated `generate_procedural_v1_emplacements.py` so the MG nest is produced from a new north-facing/no-man's-land composition.
- Regenerated:
  - `mg-nest/mg-nest-procedural-v1.png`
  - `mg-nest/mg-nest-blueprint-procedural-v1.png`
- Regenerated review images:
  - `mg-nest-example-4x.png`
  - `mg-nest-blueprint-example-4x.png`
  - `procedural-v1-emplacements-overview-contact-sheet.png`
- Updated manifest/QA wording to state:
  - top/north is no-man's-land
  - rear/south is open
  - sandbags are only the front lip/notch cheeks
  - barrel runs north over the firing lip
  - no closed sandbag ring and no side-facing gun

## Checks

- Independent Pillow check confirmed updated MG runtime PNGs are `128x128 RGBA`, transparent, and nonblank.
- `dotnet build TWB-TrenchWorks.sln --no-restore` passed with 0 warnings and 0 errors.
- Unity batchmode validator passed:
  - method: `TWB.Trenchworks.Editor.TrenchworksProjectSetup.ValidateProceduralV1EmplacementArt`
  - loaded `4/4` Resources textures
  - texture size: `128x128`

## Review Images

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Emplacements\Review\procedural-v1\mg-nest-example-4x.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Emplacements\Review\procedural-v1\mg-nest-blueprint-example-4x.png`

## Risks

- Live Play Mode/F9 review is still needed for final scale and in-scene readability.
- Faction-specific mirroring/orientation is still a future runtime question; this pass corrects the static art anatomy.

## Memory-Worthy Note

MG nest art should be specified as a top/north no-man's-land firing position: front lip sandbags only, open rear, barrel over the lip. Do not describe this as merely left/right facing.
