# TWB Trenchworks Runtime War Art Loading Report

Date: 2026-05-23

Scope: standalone TWB Trenchworks war-side runtime art readiness. Permanent Obsidian memory was not edited.

## What Changed

Updated `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`:

- War battlefield textures now load from editor `Assets`, then packaged `StreamingAssets`, then `Resources`.
- War UI icons now use the same safer fallback path instead of failing immediately when loose editor files are absent.
- Added shared helpers:
  - `LoadWarTextureFromProjectOrStreaming`
  - `LoadWarTextureFromFile`
- Preserved point filtering and wrap-mode behaviour for unit frames, UI icons, and repeatable battlefield textures.

Updated `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`:

- Command-plan smoke now validates that the runtime war-art mirror exists under `Assets\StreamingAssets\Art\War`.
- The smoke compares source and StreamingAssets runtime file counts for:
  - `Cutouts`
  - `Emplacements`
  - `MultiTile`
  - `SolidAssets`
  - `TrenchExtras`
  - `UI`
  - `VFX`
- The smoke also checks that `PrototypeBootstrap` still contains the StreamingAssets fallback.

Created runtime StreamingAssets mirrors under:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\StreamingAssets\Art\War
```

Mirrored runtime categories:

- `Cutouts`: 366 files, 11.42 MB
- `Emplacements`: 31 files, 0.44 MB
- `MultiTile`: 45 files, 2.88 MB
- `SolidAssets`: 5,396 files, 56.88 MB
- `TrenchExtras`: 1,223 files, 17.49 MB
- `UI`: 4,725 files, 12.34 MB
- `VFX`: 792 files, 5.42 MB

Total mirrored runtime files: 12,578.

Excluded intentionally:

- `Review` and `Sheets`, because they are evidence/source review material rather than runtime assets.
- `Units`, because a `Resources` runtime unit mirror already exists and the full source unit folder is roughly 500 MB.
- `TrenchTilesets`, because a large `Resources` mirror already exists.

## Checks Run

- `dotnet build TWB-TrenchWorks.sln --no-restore`
  - Passed: 0 warnings, 0 errors.

- Unity command-plan smoke:
  - Log: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Logs\codex-war-runtime-assets-command-smoke.log`
  - Passed with return code 0.
  - Key proof: `war runtime StreamingAssets mirror passed=True, folders=7, files=12578`.

## Remaining Risks

- This improves packaged-build safety, but it is not a substitute for an actual Windows player build smoke.
- Candidate-only solid packs are now available to runtime loading, but many still need gameplay/render integration before they should be considered accepted in-scene assets.
- Mission system gaps remain from the prior audit: 14 placeholder mission families and several partial families need richer decision-hint behaviour.

## Recommended Next Gate

Next implementation slice should target the mission/controller gap:

- Add an all-planned-template command smoke that requires non-placeholder profiles to produce either a real `SquadMissionController` hint or an explicit failure.
- Harden the first failures for `ClaimBuildMgPoint`, `OccupyRifleBay`, `CasualtyResponse`, `MortarSupport`, and `CommandRelay`.
- Then run a live editor/F9 visual test and, after that, a Windows player build smoke to prove the StreamingAssets path.
