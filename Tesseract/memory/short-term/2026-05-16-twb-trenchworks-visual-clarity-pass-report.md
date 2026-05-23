# TWB Trenchworks Visual Clarity Pass Report

Date: 2026-05-16

## Scope

Standalone TWB-tagged game: TWB Trenchworks Unity 2D prototype at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

## What Changed

- Added persistent casualty markers: dead units now remain visible as muted faction-tinted X markers at their last position instead of simply disappearing.
- Added live-unit status cues: living unit markers now have a health strip, state outline, command tab for leaders, orange combat halo while fighting, amber hatching while digging/building, and red warning strip when retreating/seeking/recycling.
- Changed command unit map label from `C2` to `LT` for a clearer lieutenant/leader read.
- Made active contacts more readable with orange contact pulses and an outline, alongside the existing bullet tracers.
- Restyled integrated trench plans as amber blueprint/construction hatching with progress labels instead of green solid trench-like slabs.
- Reworked the war map key to explain living units, casualty X markers, firefights, construction hatching, trenches, and dug-in units.
- Simplified the right-side Unit Summary stats so it shows player/enemy alive and dead counts, engaged/digging/trouble counts, build-plan count, and map-key reminders instead of field-map debug metrics.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-visual-clarity-pass-report.md`

## How To Run It In Unity Hub

1. Open Unity Hub.
2. Open `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
3. Open or confirm scene `Assets\Scenes\TrenchworksPrototype.unity`.
4. Press Play.
5. Watch the wave drill after first contact: living units should have faction colours and health strips, casualties should remain as X marks, active fights should read orange, and construction should read amber/hatched.

## Whether `prototype\My project` Was Involved

No. This pass only touched the current live project home: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

## Tests And Checks Run

- Read project memory context: `memory/hot.md`, `memory/index.md`, and `memory/wiki/game-dev/project-hierarchy.md`.
- `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln`
  - Result: passed with the existing warning that there is no project to restore.
- Unity response-file compiler:
  - `dotnet exec ... csc.dll ... Assembly-CSharp.rsp ... Assembly-CSharp.rsp2`
  - Result: passed with exit code 0.
- Unity editor log check:
  - The open editor imported `PrototypeBootstrap.cs`, booted `TrenchworksPrototype`, and logged `PrototypeBootstrap.Awake` plus first `OnGUI` frame.
  - No relevant C# compile failure was found.

## Cleanup Performed

- No temporary files, screenshots, or batchmode logs were created.

## Risks

- This is still immediate-mode prototype rendering, so it improves legibility but does not replace the eventual tile/sprite visual pass.
- Casualty markers are capped at far zoom to avoid clutter; a very large battle may still need grouped casualty piles later.
- The right panel now hides some field-map debug numbers in favour of playtest clarity. Those diagnostics still exist in code and can be surfaced later behind a debug toggle.
- Batchmode smoke was skipped because Unity is already open on the project.

## Memory-Worthy Notes

- Normal play needs a plain battlefield vocabulary before deeper AI tuning: alive, dead, engaged, building, in cover, and retreating must be visually obvious.
- Construction plans should not look like completed trenches. Amber blueprint hatching reads better than solid green/owner-tinted slabs.
- Casualties should remain visible during playtests so the user can understand where engagements happened and which side paid for the ground.

## Follow-Up Recommendations

- Live Play review should specifically check whether the X casualty markers and orange firefight cues remain readable at the usual zoom level.
- If construction hatching is still too busy, the next pass should make build plans visible only near selected teams or active engineer squads.
- Consider adding a simple “debug visuals” toggle later so field-map/influence information can be separated from normal playtest readability.

## Anything Blocked

- No source-level blockers. Full Unity batchmode smoke was not run because an active Unity editor instance is already open on this project.
