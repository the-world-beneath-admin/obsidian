# TWB Trenchworks Squad-Leader AI Implementation Report

Date: 2026-05-16
Worker: Bob / Codex
Scope: TWB Trenchworks standalone Unity prototype.

## What Changed

- Implemented the first shared squad-leader decision model in `WarTeamSlice`.
- Added a squad decision blackboard for anchor, entry lane, heard contact, contact heat, and supply-needy friendly teams.
- Replaced the narrow local influence sample with broader candidate generation:
  - forward cone candidates
  - lateral offsets
  - heard/known contact candidates
  - nearby cover candidates
  - nearby trench candidates
  - resupply and fallback candidates
- Added utility-style scoring for:
  - scout value
  - cover
  - contact state
  - friendly trench value
  - friendly support
  - supply reach
  - route risk
  - straight-line advance penalty
  - combat edge
- Added role/profile weighting by current team kind:
  - scouts prefer recon and suspected-contact investigation
  - assault teams prefer confirmed contact but can hold/dig before attacking
  - engineers prefer held contact, trenches, construction, and connection work
  - supply teams prefer needy squads and safer routes
- Added combat-edge behavior so positive fights can produce `DigIn` or `Hold` instead of automatic attack.
- Added "holding trench" decision reasons using existing `Hold` decisions.
- Changed leader stepping so movement can alternate between forward and lateral movement instead of always walking x-first.
- Added formation collision avoidance so members search nearby open cells instead of overlapping.
- Extended `InfluenceSample` with diagnostic fields for combat edge, support, route risk, straight-line penalty, and final score.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamTypes.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-squad-leader-ai-implementation-report.md`

## How To Run It In Unity Hub

1. Open `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks` in Unity Hub.
2. If the Editor is already in Play Mode, stop Play once so Unity can import/recompile scripts.
3. Wait for script compilation to finish.
4. Open `Assets\Scenes\TrenchworksPrototype.unity` if needed.
5. Press Play.

The immediately visible wave-drill layer still has legacy per-unit behavior, but the integrated team overlay and diagnostics now use the improved squad-leader model. This is the intended first step before retiring or wiring the old unit loop more deeply into the team brain.

## Tests And Checks Run

- Source-level C# compile against Unity 6000.3.8f1 UnityEngine modules and non-editor scripts.
  - Passed.
- Temporary .NET smoke runner for `WarTeamSmoke.RunAllPrototypeSmokes()`.
  - Passed all 5 prototype smoke scenarios:
    - `scout_probe`
    - `assault_no_mans_land`
    - `fortify_after_contact`
    - `supply_under_pressure`
    - `trench_connect_back_to_base`
- `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln`
  - Passed, with the known warning that the Unity-generated solution currently has no projects to restore/build.

## Unity Editor Compile Status

- The Unity Editor is open on this project.
- `Editor.log` has not yet shown a fresh `Assembly-CSharp` rebuild after the latest script save.
- This usually means the open Editor is waiting for a refresh or is still in Play Mode.
- The code has passed source-level compile and smoke checks; stop Play/re-focus Unity and let it compile before testing.

## Cleanup Performed

- Removed temporary smoke-runner project files from `%TEMP%`.
- Removed temporary source-check response/output files from `%TEMP%`.
- No source, asset, or user files were deleted.

## Risks

- The prototype still has two war-behavior paths: legacy `WarWorld` per-unit logic and newer `WarTeamSlice` team logic.
- This pass improves the team-layer squad brain first; it does not fully retire the old visible unit loop.
- Contact/trench ownership is still coarse in `WarTeamSlice`; "friendly trench" currently comes from trench value rather than a fully-owned trench map.
- Hearing/contact behavior is represented through known contact heat, not yet a fully separate sound-event blackboard.

## Memory-Worthy Notes

- The right Trenchworks AI shape is shared leader tree plus specialization overlays, not bespoke trees per leader.
- Combat-edge logic should favor dig/hold before pushing, preserving the trench-war fantasy.
- Candidate generation must include lateral and cover targets; x-first movement made squads look like they were marching straight into trouble.
- Smoke diagnostics caught a real one-square occupancy issue after movement changes.

## Follow-Up Recommendations

- Wire the visible wave-drill units closer to `WarTeamSlice` decisions so the main playtest view shows the smarter squad brain more directly.
- Add explicit faction-owned trench data to the team layer.
- Add a separate sound-event/contact-report blackboard with cooldowns and response caps.
- Add debug UI rows for combat edge, route risk, straight-line penalty, and selected candidate score.
- Promote `HoldTrench` to a separate decision enum only if the diagnostics/UI need it.

## Anything Blocked

- Nothing is blocked for source-level testing.
- Live Unity playtesting depends on Unity importing the changed scripts after Play Mode is stopped/refreshed.
