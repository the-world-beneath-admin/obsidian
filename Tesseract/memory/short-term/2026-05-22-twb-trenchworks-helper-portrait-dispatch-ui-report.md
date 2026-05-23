# TWB Trenchworks Helper Portrait Dispatch UI Report - 2026-05-22

## Scope

Standalone TWB-tagged game: TWB Trenchworks only.

## What Changed

- Added a cleaner anime-style general portrait aligned with the provided factory helper character art direction.
- Added a factory helper portrait cropped from Bob's provided worker character sheet.
- Added a shared top-left portrait/text panel that appears over the map in both factory and war modes.
- War mode now shows the general portrait and a dispatch message.
- When the player requests a squad, the dispatch message is built from the actual spawned team snapshot, including sector coordinates and the assigned mission.
- Factory mode now shows the factory helper portrait with a placeholder operations blurb based on current factory lane, workers, lane stores, and the latest factory log line.
- Moved the war minimap down below the new general panel to avoid top-left overlap.
- Added pointer-overlay blocking for the helper panel so map drag/zoom input does not pass through it.
- Added a focused smoke check for the general dispatch message.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\UI\general-portrait-v2.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\UI\factory-helper-portrait-v1.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\GeneralDispatchMessageSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`

## Child Subagents

- Hooke inspected the war-mode UI and spawn/mission-assignment hook points.
- Nietzsche inspected the factory-mode UI hook point and texture-loading pitfalls.
- Both child agents were closed after results were reviewed.
- A 2-minute heartbeat was active during child work and was deleted after completion.

## Checks Run

- `dotnet build TWB-TrenchWorks.sln --no-restore`
  - Passed, but the solution currently contains no project entries, so this is only a light check.
- Focused temporary .NET harness for `GeneralDispatchMessageSmoke.RunPrototypeSmoke()`
  - Passed.
  - Verified dispatch contains welcome text, sector coordinates, mission label, and the actual assigned mission.
  - Example verified message: `OK MAGGOTS, WELCOME TO THE FRONT! Assault Section to sector (320,299) via Middle. Mission: Assault Line. assault team can press the line; team=Assault order=Assault lane=Middle intent=Balanced mission=AssaultLine`
- Unity editor log scan for `error CS`, `Compilation failed`, and `Scripts have compiler errors`
  - No matching entries found in the scanned log.

## Cleanup Performed

- Removed the first over-detailed generated general portrait from the Unity project.
- Removed the temporary dispatch smoke harness folder after the focused check passed.
- Left the original generated image outputs under `C:\Users\yrred\.codex\generated_images\...` intact as required by image generation handling.

## Risks

- Unity Play Mode was not run, so final in-editor visual layout/import behaviour still needs a live check.
- The factory helper panel is currently a placeholder blurb, not a full factory-side tutorial/dialogue system.
- The general's dispatch message currently updates on player-requested squad spawns; future enemy/general dialogue can use the same panel pattern but is not wired yet.
- The minimap has been moved downward under the general panel; verify Bob likes that top-left stack during live play.

## Memory-Worthy Notes

- Helper portraits should use the cleaner anime production-sheet style of the factory worker, not high-detail painterly portrait rendering.
- War dispatch blurbs should be generated from actual assigned mission snapshots rather than hardcoded flavour text.
- The current UI texture loader expects paths relative to `Application.dataPath`, such as `Art/War/UI/general-portrait-v2.png`, not `Assets/...` or absolute paths.

## Follow-Up Recommendations

- Run Unity Play Mode and visually confirm both helper panels at 1920x1080 and at the common working Game view scale.
- If the helper panel becomes interactive later, keep its rect in `IsPointerOverMapOverlay()`.
- Consider a small rotating dialogue queue for factory helper tips and general combat updates once the command system produces more user-facing events.
