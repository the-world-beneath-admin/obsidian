# TWB Trenchworks Soldier Runtime Mapping Report - 2026-05-22

## Scope

Standalone TWB-tagged Unity game: TWB Trenchworks.

This pass connected the current soldier runtime path mapping to the newly generated `ProceduralV2Full` soldier/unit frame art. It did not modify old V2 unit art, other TWB projects, permanent Obsidian memory, or the raw GPT Pro package.

## Summary

The full `ProceduralV2Full` soldier art matrix already existed from the prior pass:

- 33 roles.
- 5 actions: `Move`, `Crouch`, `Crawl`, `Primary`, `Secondary`.
- 2,640 individual frame PNGs under `Assets\Art`.
- 2,640 matching frame PNGs under `Assets\Resources`.

This pass updated `PrototypeBootstrap.cs` so the current runtime role/path builders target the new procedural frame set instead of the old V2 cutout path.

## Files Changed

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-twb-trenchworks-soldier-runtime-mapping-report.md`

## Runtime Mapping Changes

- Added/used the new unit cutout base path:
  - `Art/War/Units/ProceduralV2Full/Cutouts/`
- Kept the old V2 cutout base path only as a recognition path for unit-frame trimming/fallback classification:
  - `Art/War/Units/V2/Cutouts/`
- Changed the 33 `WarMemberRoleSpriteSlugs` entries from `*-v2` to `*-procedural-v2`.
- Changed `WarUnitSpritePath` to build paths under `ProceduralV2Full\Cutouts`.
- Changed `IntegratedWarMemberSpritePath` to build paths under `ProceduralV2Full\Cutouts`.
- Changed `WarUnitSpriteRole` variant/fallback slugs to `*-procedural-v2`.
- Updated `IsWarUnitFrameTexture` to recognise both new ProceduralV2Full frames and old V2 cutouts, preserving trim behaviour.

## Checks Run

- Searched `PrototypeBootstrap.cs` for exact old quoted `war-unit-*-v2` slugs:
  - Result: `0` exact old runtime slug matches.
- Searched `PrototypeBootstrap.cs` for `Art/War/Units/V2/Cutouts/`:
  - Result: one intentional constant remains for `IsWarUnitFrameTexture` compatibility.
- Verified every expected new Resources frame path exists:
  - 33 roles x 5 actions x 4 directions x 4 frames = 2,640 expected.
  - Actual Resources frames found: 2,640.
  - Missing Resources frames: 0.
- Verified `procedural-v2-full-frame-export-summary.json` reports `all_valid: true`.
- Verified raw GPT Pro catalog hash remained unchanged:
  - `EB3701497C8B7E1A0F82BA50D09F795A198B52AC9C4FED65E8C5B824D0DDBF55`
- Ran from `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`:

```powershell
dotnet build TWB-TrenchWorks.sln --no-restore
```

Result:

```text
Build succeeded.
0 Warning(s)
0 Error(s)
```

## Cleanup Performed

- Deleted the soldier runtime mapping heartbeat automation after child completion.
- Closed the child subagent after reviewing its result.
- Deleted the `__pycache__` artifact created by the parent compile checks.
- No broad cleanup was performed.

## Current State

The generated soldier/unit art is now both asset-complete for the current role/action matrix and targeted by the current runtime path builders in `PrototypeBootstrap.cs`.

The old V2 art folders remain untouched and available as archive/fallback material, but the active runtime role slugs and path builder now point to `ProceduralV2Full`.

## Risks / Remaining Gate

- Unity Play Mode and F9 visual review were not run.
- Unity import settings and visual framing should still be checked live.
- This mapping assumes Unity will import the new Resources PNGs normally; dotnet build cannot prove import settings or in-scene readability.
- Art remains first-pass procedural coverage, not final bespoke polish.

## Memory-Worthy Notes

- Fact: `PrototypeBootstrap.cs` now maps current soldier/unit runtime paths to `Art/War/Units/ProceduralV2Full/Cutouts`.
- Fact: All 2,640 expected new Resources frame paths exist.
- Fact: `dotnet build TWB-TrenchWorks.sln --no-restore` passed after the mapping change.
- Warning: Unity/F9 live validation remains the final acceptance gate before calling the soldier art fully runtime-accepted.

## Next Recommended Gate

Run a narrow Unity Play Mode/F9 visual check with representative roles:

- `rifleman`
- `field_engineer`
- `stretcher_bearer`
- `mg_gunner`

Check movement, crouch, crawl, primary, and secondary poses in scene scale before broad art polish or migration cleanup.
