# TWB Unity Worker Report - 2026-05-15 - Shared Companion Eligibility Slice

## Task

Implement the fifth conservative Unity persistence slice for The World Beneath: local activity assignment eligibility using cached shared companion lock/projection data.

## Result

Completed slice 5 of 8. Unity assignment prep now checks the cached platform inventory mirror before allowing shared companion cards into dungeon and Home Defense slot assignment flows.

Cards with an active cached shared-companion lock are locally blocked from assignment and labelled `ACCOUNT LOCKED`. Cards with matching cached shared-companion data but incomplete Unity projection data are labelled `NO ACCOUNT PROJECTION` as a warning, but are not blocked. Cards with clean cached shared-companion data are labelled `ACCOUNT READY`. Local-only or unmatched cards continue to behave as before.

No platform assignment, lock, unlock, inventory-event, or account writes were added.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\SharedCompanionAssignmentEligibilityBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\SharedCompanionAssignmentEligibilityBuilder.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\CardSummarySurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\UIShellBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\TWB.UnityBridge.csproj`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-15-twb-unity-shared-companion-eligibility-slice-report.md`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore`
  - First run failed because the new partial builder file was not included in `TWB.UnityBridge.csproj`.
  - Fixed by adding the compile include.
- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore`
  - Passed after the project-file include.
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

No temporary files or scratch artifacts were created. Unity generated the `.meta` file for the new builder and it was preserved.

## Risks

- Shared companion matching is conservative and based on cached mirror identifiers plus starter-pet bridge identifiers. If backend identifier contracts change, eligibility labels may stop matching until the bridge is updated.
- Cached locks can block local assignment until the next mirror refresh if the remote state changed. Expired `locked_until` values are ignored when parseable.
- Missing projection data is surfaced as a warning only, not a hard block.
- This is UI-level local assignment gating only. Lower-level local services still do not write or enforce platform account locks.
- No narrow automated UI regression test exists yet for the new archive/card-summary account eligibility labels.

## Memory-worthy notes

- Unity now has a read-only local assignment eligibility bridge using cached shared companion lock/projection data.
- The slice intentionally keeps platform inventory/account state read-only and does not implement remote assignment locks.

## Do not promote to memory

- Exact temporary UI label wording can still change.
- The current identifier matching logic should remain implementation detail unless it hardens into a formal contract.

## Next recommended gate

Slice 6 should add a small account-state freshness/refresh affordance around assignment prep, or define the remote lock write protocol on paper before implementing any real platform assignment mutation.
