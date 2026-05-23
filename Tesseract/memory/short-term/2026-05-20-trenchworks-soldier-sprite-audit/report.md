# TWB Trenchworks Soldier Sprite Audit - 2026-05-20

## Scope

Standalone TWB-tagged game: TWB Trenchworks only.

## What Changed

- Audited all `2,640` V2 soldier/unit cutout PNG frames under `Assets/Art/War/Units/V2/Cutouts`.
- Removed detached alpha components from `412` existing cutout frames. These were separated neighbor-frame contaminants, commonly partial helmets/heads or body fragments below the active frame.
- Rebuilt `107` existing V2 transparent sheet PNGs from the cleaned cutout frames so the sheets and runtime cutouts now match.
- Patched the runtime unit loader to preserve the fixed sprite-frame canvas instead of trimming every frame at load time. This prevents per-frame scale/framing jitter during walking and other animations.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- Existing PNG cutout frames under:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Cutouts`
- Existing transparent sheet PNGs under:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Transparent`

## Checks

- Component audit after repair: `0` remaining detached-bleed frames.
- Transparent sheet rebuild verification: `0` sheet/cutout mismatches.
- `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln --no-restore` passed with `0` warnings and `0` errors.

## Evidence

- `war-unit-v2-sprite-component-audit.json`
- `war-unit-v2-sprite-component-audit.csv`
- `war-unit-v2-sprite-component-audit-preview.png`
- `war-unit-v2-sprite-component-repair.json`
- `war-unit-v2-sprite-component-postrepair-audit.json`
- `war-unit-v2-sprite-component-repair-after-preview.png`
- `war-unit-v2-transparent-sheet-rebuild-report.json`

## Risks

- This was a broad image repair pass. It removed only detached alpha islands that were separated from the main soldier silhouette; deliberately attached props and weapons were preserved.
- Unity Play Mode should be visually checked after editor reimport/domain reload to confirm the unit animation framing now reads correctly at gameplay scale.

## Memory-Worthy Notes

- V2 unit runtime rendering should not trim unit-frame PNGs per frame. The unit cutouts already use normalized canvases, and trimming causes animation jitter.
- Future unit-sheet generation/cleanup should include a detached-alpha-component QA pass before runtime integration.
