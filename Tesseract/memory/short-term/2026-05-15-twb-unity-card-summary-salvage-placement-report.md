# TWB Unity Worker Report - 2026-05-15 - Card Summary Salvage Placement

## Task

Confirm whether the Card Summary Salvage button is inert because the selected card is a protected starter pet, and if so move Salvage to the right-hand side.

## Result

Confirmed Peggy is protected by existing starter-pet dismantle rules. The UI snapshot sets `CanDismantle` false for protected starter cards, and `ArchiveService` also rejects protected starter companion dismantles. I did not weaken that protection.

Moved the Card Summary Salvage button to the lower-right action position during initial build and refresh, matching the user's requested placement.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\CardSummarySurfaceBuilder.cs`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed with 0 errors and 2 existing warnings.

## Cleanup performed

No cleanup was needed.

## Risks

The right-side placement needs a quick Unity editor reload/visual pass because this was verified by build, not by a live click/visual test.

## Memory-worthy notes

Protected starter companion cards are blocked from dismantle in both UI projection and archive service command validation.

## Do not promote to memory

Do not promote this as a new design decision; it confirms existing starter-pet protection.

## Next recommended gate

After scripts reload, open Peggy's Card Summary and confirm Salvage is on the right and disabled by protection. Then test a non-starter archive card to confirm the salvage modal still opens.
