# TWB Unity Worker Report - 2026-05-15 - Shared Companion Projection Slice

## Task

Implement persistence slice 3 for The World Beneath main Unity game: parse and show prepared shared-platform starter selection and companion-card data as read-only Unity state.

## Result

Unity now parses `starterSelection`, companion `baseStats`, companion `gameProjection`, and companion `state` from `/api/platform/state`. The locally cached account mirror preserves the starter-selection projection, shared companion cards, exported stack rows, wallet rows, and companion locks.

The Inventory account-state panel now displays the cached starter picks, shared companion rows, lock badges, and exported stack rows without importing them into local Will/material/card inventory. Settings state summaries also now include starter-selection context through the cached mirror summary.

The main-game platform inventory adoption switch remains disabled. No remote account, inventory, Worker, migration, or Cloudflare production data was changed.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Backend\TwbPlatformAccountLinkClient.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\InventorySurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-15-twb-unity-shared-companion-projection-slice-report.md`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore`
  - Passed.
  - Existing warnings remain: `_craftCreateV2SummaryName` and `WorldMapVisualStackStats.FoldedContributorGlyphs` are never assigned.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status`
  - Passed: editor status reported `probably-clean`, with 0 error signals and 0 warning signals.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile`
  - Passed with exit code 0.
- Follow-up editor status check
  - Passed: editor status reported `probably-clean`, with 0 error signals and 0 warning signals.

## Cleanup performed

No temporary files or generated scratch artifacts were created during this slice.

## Risks

- The read-only companion projection depends on the current `/api/platform/state` JSON field names from the website Worker.
- The Inventory account-state panel shows a compact, non-scrollable subset when many companion or stack rows exist.
- This slice does not yet add a dedicated companion-detail view or companion-lock interaction model.
- The platform inventory adoption switch remains intentionally disabled, so shared companions are visible but not yet selectable for main-game activities.

## Memory-worthy notes

- Unity now has a read-only shared account companion projection.
- Starter selection is cached locally from platform state and shown alongside account inventory mirror data.
- Main-game local inventory remains protected from accidental shared-platform import.

## Do not promote to memory

- Exact panel row limits and compact text labels are UI implementation details.
- The current DTO helper names are implementation details unless they become a public client contract.

## Next recommended gate

Proceed to persistence slice 4: add a read-only shared-companion detail/selection preparation surface, still without assigning or locking companions from Unity.
