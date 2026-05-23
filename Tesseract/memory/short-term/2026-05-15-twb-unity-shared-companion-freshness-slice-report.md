# TWB Unity Worker Report - 2026-05-15 - Shared Companion Freshness Slice

## Task

Implement the sixth conservative Unity persistence slice for The World Beneath: account-state freshness and refresh affordance around shared companion assignment prep.

## Result

Completed slice 6 of 8. Pet assignment prep now exposes cached shared-account state freshness while remaining read-only.

When Archive is opened as a pet assignment picker, it now shows a compact account-cache readout beside the context bar:

- `NO ACCOUNT` when no TWB account is linked.
- `NOT PULLED` when no cached platform mirror exists yet.
- `PULLING` while the existing Settings platform-state pull is running.
- `SYNC <age>` for fresh cached state.
- `STALE <age>` when the cached mirror is older than 15 minutes.

The assignment picker also has a small `Pull` button that reuses the existing Unity Settings shared-account-state pull path. This calls the existing `/api/platform/state` read flow and refreshes Archive/Card Summary labels when the mirror updates. It does not add platform inventory events, assignment locks, unlocks, or remote writes.

Card Summary assignment mode now also includes the account-cache age beneath the shared companion eligibility line, so a player can see whether lock/projection labels were based on fresh or stale cached state.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\SharedCompanionAssignmentEligibilityBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\SettingsSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\UIShellBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-15-twb-unity-shared-companion-freshness-slice-report.md`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore`
  - Passed.
  - 0 errors.
  - 2 existing warnings remained:
    - `WorldMapSurfaceBuilder.cs(649,24): UIShellBootstrap.WorldMapVisualStackStats.FoldedContributorGlyphs is never assigned`
    - `UIShellBootstrap.cs(370,22): _craftCreateV2SummaryName is never assigned`
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile`
  - Passed.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status`
  - `Status: probably-clean`
  - `ErrorSignals: 0`
  - `WarningSignals: 0`

## Cleanup performed

No temporary files or scratch artifacts were created.

## Risks

- The `Pull` affordance depends on the existing linked-account bearer token and `/api/platform/state` read path. If the token is expired, the user must relink from Settings.
- The 15-minute stale threshold is conservative and UI-only. It warns about potentially old lock/projection data but does not force a refresh.
- The refresh button is only shown in assignment-picker context; the broader Archive browsing surface remains uncluttered.
- No remote lock write protocol exists yet. Shared companion locks are still advisory/read-only in Unity.
- No automated UI test exists yet for the new freshness readout or assignment-picker pull button.

## Memory-worthy notes

- Unity assignment prep now displays cached account-state freshness and can manually refresh the read-only platform mirror from the assignment picker.
- This slice continues to preserve the boundary that Unity may read account state but must not adopt platform inventory or write shared companion assignment locks yet.

## Do not promote to memory

- Exact freshness wording and the 15-minute stale threshold can remain implementation detail unless they become formal UI/UX policy.

## Next recommended gate

Slice 7 should define and test a non-mutating companion lock conflict model end to end: local assignment planner, cached remote locks, local dungeon/home-defense locks, and the exact user-facing conflict states before any real platform lock write protocol is attempted.
