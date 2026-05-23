# TWB Trenchworks First Trench Hiccup Report

Date: 2026-05-22 11:28

## Scope

Standalone TWB-tagged game: TWB Trenchworks only.

## What Changed

- Added a trench-render warm-up pass during scenario reset/startup.
- The warm-up preloads and slices common trench render assets before the first visible trench construction frame:
  - legacy 16-mask trench blueprint atlas
  - Tier 1 wide-bottom trench art style
  - wide-bottom floor, berm, spill, edge, outer-corner, and inner-corner masks for the 16 common connection masks
  - floor, edge-shadow, edge-cut, and edge-rim material textures
- Added a profiler marker named `TWB.Trenchworks.WarTrenchRenderWarmup`.

## Why

The highest-confidence cause of the first-trench hiccup was synchronous first-use work in the trench renderer. When the first dug trench appeared, the renderer could parse style data, read PNG files, create atlas tile textures, run `GetPixels`, call `SetPixels`, and `Apply` during that gameplay frame.

Moving that work to reset/startup should prevent the visible hitch when the first trench cell starts getting dug.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-112841-trenchworks-first-trench-hiccup-report.md`

## Child Subagent

- Child explorer `019e5082-9c96-7c62-ab31-966a9e2a9530` was spawned for bounded inspection.
- The implementation finished before the child returned useful notes; the child was closed and the heartbeat was deleted.

## Checks Run

From `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`:

```powershell
dotnet build "TWB-TrenchWorks.sln" --no-restore
```

Result: passed, 0 warnings, 0 errors.

## Cleanup Performed

- Deleted the temporary heartbeat automation after work completed.
- No scratch files were created.
- No raw GPT Pro package files were modified.
- No staging, commit, reset, or broad cleanup was performed.

## Risks

- Unity Play Mode profiling is still needed to confirm the hitch is fully removed.
- Reset/startup may now pay a small extra warm-up cost. That is preferable to a visible hiccup during first trench construction.
- If a second hiccup appears at Tier 2 or Tier 3 upgrade time, those tier atlases should be warmed separately or progressively.

## Memory-Worthy Notes

- First trench construction is sensitive to synchronous trench atlas/style first-use work in `PrototypeBootstrap.cs`.
- Warm-up currently covers Tier 1/common masks, which is the likely first-dig path.

## Follow-Up Recommendations

- Play Mode profile the first trench dig again.
- If any hitch remains, inspect terrain chunk loads and first soldier-frame loads around the same tick.
