# TWB Unity Worker Report - 2026-05-13 - Wave Preview Scrollbar

## Task

Main game / The World Beneath. Improve the dungeon inspect monster-wave preview panel so it scrolls faster and shows a small minimalist scrollbar.

## Result

The wave preview `ScrollRect` now uses higher wheel sensitivity and reserves a narrow right-side rail for a cyan scrollbar when more than three waves are present. The wave content viewport was narrowed slightly so cards do not overlap the scrollbar lane.

## Files touched

- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs

## Checks run

- `git diff --check -- Assets/_TWB/Scripts/UnityBridge/UI/Builders/WorldMapSurfaceBuilder.cs` - passed.
- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` - passed with 2 existing warnings.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` - probably-clean, with 0 error signals and 0 warning signals.

## Cleanup performed

No temporary files were created.

## Risks

Visual verification was limited to code/layout inspection and build/status checks. The open Unity editor should be reloaded or refreshed to confirm the scrollbar sits exactly where desired in the live panel.

## Memory-worthy notes

Dungeon inspect wave preview now uses a visible scrollbar for 4+ wave dungeons and faster scroll input.

## Do not promote to memory

Do not promote this implementation detail unless Bob/orchestrator decides the UI convention should become permanent style guidance.

## Next recommended gate

Open a dungeon with 4+ waves in the live Unity view and confirm the wave list scrolls at the desired speed without card overlap.
