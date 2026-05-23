# TWB Trenchworks MG Nest Barrel Correction Report

Date: 2026-05-22
Worker: TWB Trenchworks standing worker
Scope: Standalone TWB-tagged game: TWB Trenchworks only

## Summary

Corrected the ProceduralV1 MG nest art after Bob flagged that the machine gun was staged incorrectly inside the nest. The issue was not simply compass direction; the receiver/tripod needed to sit inside the dugout while the barrel/muzzle protrudes through and beyond the front sandbag firing lip.

## Child Subagent

- Child agent: `019e5037-a1b9-7423-afd0-a50e82168224`
- Heartbeat: `twb-trenchworks-mg-direction-correction-heartbeat`, created during child work and deleted after review.
- Child scope: revise generator and regenerate emplacement art only; no permanent memory edits, raw package edits, staging, commits, or broad cleanup.

## What Changed

- Updated `generate_procedural_v1_emplacements.py` so the MG nest is corrected by construction.
- Regenerated MG nest runtime art and blueprint art.
- Regenerated the full required four-file emplacement set because the generator writes the complete contract.
- Updated manifest and QA wording to describe the anatomical contract: receiver/tripod inside, barrel beyond the front sandbag firing aperture.
- Rifleman drawing logic was not intentionally changed.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\emplacement-art-generation\generate_procedural_v1_emplacements.py`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\emplacement-art-generation\emplacement-procedural-v1-manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\emplacement-art-generation\emplacement-procedural-v1-qa.json`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unity-procedural-v1-emplacement-validation.log`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Emplacements\ProceduralV1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Resources\Art\War\Emplacements\ProceduralV1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Emplacements\Review\procedural-v1\`

## Checks

- Independent Pillow check confirmed the updated MG runtime PNGs are `128x128 RGBA`, transparent, and nonblank.
- `dotnet build TWB-TrenchWorks.sln --no-restore` passed with 0 warnings and 0 errors.
- Unity batchmode validator passed:
  - method: `TWB.Trenchworks.Editor.TrenchworksProjectSetup.ValidateProceduralV1EmplacementArt`
  - loaded `4/4` Resources textures
  - texture size: `128x128`

## Review Images

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Emplacements\Review\procedural-v1\mg-nest-example-4x.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Emplacements\Review\procedural-v1\mg-nest-blueprint-example-4x.png`

## Risks

- Live Play Mode/F9 visual review is still needed to judge scale and readability in the actual trench scene.
- The corrected art still uses one side-facing presentation; faction-specific mirroring can be added later if live placement proves the same bitmap is insufficient for both fronts.

## Memory-Worthy Note

For MG nest art, the important contract is anatomical: the gun must visibly fire out over/through the front sandbag lip. Do not reduce this requirement to a generic left/right flip.
