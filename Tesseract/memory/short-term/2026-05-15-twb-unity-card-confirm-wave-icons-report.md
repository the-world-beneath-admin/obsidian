# TWB Unity Worker Report - 2026-05-15 - Card Confirm and Wave Icons

## Task

Fix the dungeon assignment Card Summary Confirm button still not working, and restore monster/pet sprites in the world-map dungeon wave preview.

## Result

Confirm now resolves protected starter companions to their required role slot before dispatching `SetDungeonPartySlotCommand`, so Peggy/Hazel route to the utility slot, Stanly/Merlin route to attack, and Nova/Chuck route to defense. Card Summary also shows a short routing/failure line instead of silently doing nothing when assignment is blocked.

World-map dungeon wave tiles now ask `PetCardIconResourceResolver.TryGetEnemySprite` for mirrored monster sprites and only fall back to the small affinity marker when no sprite exists.

## Files touched

- `Assets/_TWB/Scripts/UnityBridge/UI/Builders/CardSummarySurfaceBuilder.cs`
- `Assets/_TWB/Scripts/UnityBridge/UI/Builders/SharedCompanionAssignmentEligibilityBuilder.cs`
- `Assets/_TWB/Scripts/UnityBridge/UI/Builders/WorldMapSurfaceBuilder.cs`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` - passed.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` - status probably-clean, no current error/warning signals reported.

## Cleanup performed

No temporary files were created.

## Risks

Starter cards selected from a mismatched dungeon slot now route to the correct role slot automatically. This respects starter role rules, but it can feel surprising if a different slot was visibly selected; the Card Summary description now states the routing.

Boss enemies or non-mirrored enemies still use the fallback affinity marker unless dedicated sprite mappings are added later.

## Memory-worthy notes

Protected starter companion assignment should be treated as role-slot routing in UI flows, not as a free slot assignment. Silent command failures in card assignment surfaces should surface an inline explanation.

## Do not promote to memory

This was a narrow UI/assignment repair, not a new design decision about party composition.

## Next recommended gate

Open the world-map dungeon summary in the Unity editor, confirm Peggy from the card preview, and verify the utility slot fills and the archive picker collapses back to the dungeon summary. Also inspect a dungeon with mirrored monsters to confirm wave tiles show sprites.
