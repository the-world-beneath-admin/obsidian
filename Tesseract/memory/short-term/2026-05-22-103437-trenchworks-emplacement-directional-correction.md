# TWB Trenchworks Emplacement Directional Correction

Date: 2026-05-22
Worker: TWB Trenchworks standing worker
Scope: Standalone TWB-tagged game: TWB Trenchworks only

## What Changed

- Investigated Bob's report that the MG nest image still showed the wrong repeated orientation.
- Confirmed the real issue was not only the source drawing: runtime had one static MG image and one static rifleman image, with no direction variants.
- Regenerated fresh procedural MG nest and rifleman emplacement active/blueprint art with north/east/south/west variants.
- Updated runtime selection so player-side emplacements use east-facing art and enemy-side emplacements use west-facing art.
- Corrected rifleman emplacements to use the same front/back rule as MG nests: weapon barrel/slit over the front lip, open rear entry behind the soldier.
- Updated the emplacement validator to expect 20 runtime textures.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\emplacement-art-generation\generate_procedural_v1_emplacements.py`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\emplacement-art-generation\emplacement-procedural-v1-manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\emplacement-art-generation\emplacement-procedural-v1-qa.json`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Emplacements\ProceduralV1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Resources\Art\War\Emplacements\ProceduralV1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Emplacements\Review\procedural-v1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`

## Review Images

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Emplacements\Review\procedural-v1\procedural-v1-emplacements-overview-contact-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Emplacements\Review\procedural-v1\procedural-v1-emplacements-directional-overview.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Emplacements\Review\procedural-v1\mg-nest-east-example-4x.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Emplacements\Review\procedural-v1\rifleman-emplacement-east-example-4x.png`

## Tests And Checks

- `python generate_procedural_v1_emplacements.py`
  - Result: wrote 40 runtime PNGs and 6 review PNGs.
- Pillow/QA JSON check:
  - Result: `emplacement-procedural-v1-qa.json` reports `pass`.
  - Runtime files exist under both `Assets\Art` and `Assets\Resources`, with mirrored hashes.
- Visual review:
  - Directional overview confirms north/east/south/west variants.
  - East variants place the weapon barrel over the right/front lip and keep the left/rear side open.
  - West variants place the weapon barrel over the left/front lip and keep the right/rear side open.
- `dotnet build "TWB-TrenchWorks.sln" --no-restore`
  - Result: passed with 0 warnings and 0 errors.
- Unity batch validator attempted:
  - Result: blocked because another Unity instance already has the project open.

## Cleanup Performed

- Closed child subagent `019e504c-0bed-75f1-bc1c-488433e25351`.
- Deleted heartbeat automation `twb-trenchworks-emplacement-correction-heartbeat`.
- No raw GPT Pro packages were modified.
- No permanent Obsidian wiki/index/hot/log files were modified.

## Risks

- Unity import validation and Play Mode/F9 placement review are still blocked until the open Unity project instance is closed or used manually.
- Runtime now selects east for player-side and west for enemy-side emplacements. If later fronts become vertical or curved, north/south variants exist but runtime direction selection will need to become anchor/vector-aware.

## Memory-Worthy Notes

- The previous "fixed" MG source was only north-facing; it was insufficient because runtime drew one static bitmap everywhere.
- Current horizontal-front logic needs player east-facing and enemy west-facing emplacement variants.
- Rifleman emplacements had the same front/back problem and are now corrected to share the MG orientation contract.
