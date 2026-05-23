# TWB Trenchworks Procedural V2 Full Soldier Unity Validation Report - 2026-05-22

## Scope

Standalone TWB-tagged Unity game: TWB Trenchworks.

This pass validated that the generated `ProceduralV2Full` soldier/unit art matrix is loadable by Unity through the current runtime Resources path shape. It did not modify old V2 unit art, other TWB projects, permanent Obsidian memory, or the raw GPT Pro package.

## Summary

Added and ran a Unity Editor batchmode validation for the new soldier art matrix.

The validator confirms:

- The frame-export summary reports `all_valid: true`.
- The runtime role mapping contains 33 complete `*-procedural-v2` slugs.
- No exact old quoted `war-unit-*-v2` runtime slugs remain in `PrototypeBootstrap.cs`.
- Unity `Resources.Load<Texture2D>` can load all expected ProceduralV2Full soldier frame textures.
- All loaded textures are `64 x 64`.

## Files Changed

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unity-procedural-v2-full-soldier-art-validation.log`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-twb-trenchworks-procedural-v2-full-soldier-unity-validation-report.md`

Unity batchmode also generated Unity import metadata side effects for the new assets. These were left in place because they are expected import artifacts for the generated art and broad cleanup/reset is forbidden.

## Validation Method

Added menu/batch method:

```text
TWB.Trenchworks.Editor.TrenchworksProjectSetup.ValidateProceduralV2FullSoldierUnitArt
```

Menu item:

```text
TWB Trenchworks > Assets > Validate ProceduralV2Full Soldier Unit Art
```

The method validates the full matrix:

- 33 roles.
- 5 actions: `Move`, `Crouch`, `Crawl`, `Primary`, `Secondary`.
- 4 directions: `down`, `left`, `right`, `up`.
- 4 frames per direction.
- 2,640 expected Resources textures.

Representative paths include:

- rifleman `Move`
- stretcher bearer `Secondary`
- MG gunner `Primary`
- field engineer `Crouch`, `Crawl`, and `Primary`

## Checks Run

From:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

Build:

```powershell
dotnet build TWB-TrenchWorks.sln --no-restore
```

Result:

```text
Build succeeded.
0 Warning(s)
0 Error(s)
```

Unity batchmode:

```powershell
& 'C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Unity.exe' -batchmode -quit -projectPath 'C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks' -executeMethod TWB.Trenchworks.Editor.TrenchworksProjectSetup.ValidateProceduralV2FullSoldierUnitArt -logFile 'C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unity-procedural-v2-full-soldier-art-validation.log'
```

Result:

```text
Unity exited with return code 0.
TWB Trenchworks ProceduralV2Full soldier/unit art validation passed.
Loaded 2640/2640 Resources frame textures.
roles/actions/directions/frames: 33/5/4/4.
texture size: 64x64.
```

Additional parent verification:

- Confirmed `procedural-v2-full-frame-export-summary.json` reports:
  - `all_valid: true`
  - `role_count: 33`
  - `action_count: 5`
  - `art_frame_png_count: 2640`
  - `resources_frame_png_count: 2640`
  - `qa_json_count: 165`
- Confirmed no Unity process remained running after validation.

## Current State

The full current-system soldier/unit art requirement is now satisfied at the asset and runtime-load level:

- All current roles have new-system procedural art.
- All current runtime actions/postures have frames.
- Individual frame PNGs exist under Art and Resources.
- Runtime mapping points to the new `ProceduralV2Full` cutout paths.
- Unity batchmode successfully imports and loads all expected Resources textures.

## Source Policy

- No old V2 soldier/unit visual assets were used as inputs.
- No old ProceduralV1 outputs were used as visual inputs.
- No image generation was used.
- The raw Obsidian/GPT Pro package was not modified.

## Remaining Caution

This pass proves Unity import/load readiness and matrix coverage. It does not replace a future subjective art-direction polish pass. If Bob wants the sprites prettier or more bespoke per role, that is a separate polish gate, not a missing current-system coverage gate.

## Cleanup Performed

- Deleted the soldier Unity validation heartbeat automation after child completion.
- Closed the child subagent after reviewing its result.
- No broad cleanup was performed.

## Memory-Worthy Notes

- Fact: ProceduralV2Full soldier art is now Unity batchmode validated.
- Fact: Unity loaded all 2,640 expected soldier Resources frame textures.
- Fact: Runtime mapping points to `Art/War/Units/ProceduralV2Full/Cutouts`.
- Fact: `dotnet build TWB-TrenchWorks.sln --no-restore` passed after adding the validator.
