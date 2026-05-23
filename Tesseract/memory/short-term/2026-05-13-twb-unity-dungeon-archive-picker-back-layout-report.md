# TWB Unity Worker Report - 2026-05-13 - Dungeon Archive Picker Back And Layout

## Task

Main game / The World Beneath. Fix the dungeon party pet picker so its Back button returns cleanly to the dungeon context and reduce visual overlap/bleed-through from the world-map frame assets behind it.

## Result

The picker Back button now closes only the floating picker and returns to the underlying dungeon summary/inspect context without forcing an Activities surface rebuild. The picker also has a solid inner backplate and archive-content backing so map/navigation frame art no longer shows through the archive tiles and controls.

## Files touched

- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs

## Checks run

- `git diff --check -- Assets/_TWB/Scripts/UnityBridge/UI/Builders/WorldMapSurfaceBuilder.cs` - passed.
- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` - passed with 2 existing warnings.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` - probably-clean, with 0 error signals and 0 warning signals.

## Cleanup performed

No temporary files were created.

## Risks

This was verified by code/build/status checks, not by a fresh screenshot from the open editor. The live picker should be reopened to confirm the darker backplate is visually strong enough at the current Unity Game view scale.

## Memory-worthy notes

Dungeon party picker Back should behave as a local close back to the dungeon summary/inspect context, not as an Activities app rebuild.

## Do not promote to memory

Do not promote unless Bob/orchestrator wants this Back-button convention recorded as permanent UI guidance.

## Next recommended gate

Reopen the pet picker from a dungeon party slot and confirm Back returns to the dungeon summary/inspect window while the picker content no longer overlaps visually with background frame assets.
