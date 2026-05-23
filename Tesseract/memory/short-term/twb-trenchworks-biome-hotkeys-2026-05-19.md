# TWB Trenchworks Biome Regeneration Hotkeys

Scope: TWB Trenchworks only.

## What Changed

- Added keyboard shortcuts for full war map regeneration by biome:
  - `F5`: Temperate Forest
  - `F6`: Tropical Jungle
  - `F7`: Desert
- Each shortcut uses the biome regeneration path that pins the biome and calls `ResetScenario()`.
- This creates a fresh full war simulation/map seed/front plan instead of only changing background art.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`

## Tests And Checks

- `dotnet build TWB-TrenchWorks.sln --no-restore` passed with 0 warnings and 0 errors.

## Cleanup

- Child subagent was closed after completion.
- No permanent Obsidian memory was updated.

## Risks

- Unity Play Mode keypress verification has not yet been run.
- `F5` may also trigger editor/browser-style refresh behavior in some contexts, so live Play Mode should confirm Unity receives it cleanly.

## Follow-Up Recommendation

In Play Mode, press `F5`, `F6`, and `F7` while F9 trench debug is available, confirming the biome, terrain chunks, generated front/trench plan, hardpoints, and routes all reroll.
