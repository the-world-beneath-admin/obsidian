# TWB Unity Worker Report - 2026-05-13 - Hazel Validation Fix

## Task

Main game / The World Beneath. Clear the cascading SystemConsole/UI bootstrap failure caused by `creature_special_ephemrial_spirit_hazel` violating Tier 1 stat envelope bounds.

## Result

Fixed Hazel without weakening validators.

Hazel was authored with Hst `9..10` and Mgk `6..7`, but the Tier 1 creature template allows Hst `1..8` and Mgk `1..6`. Hazel is now high-end Tier 1 within bounds:

- Creature envelope: HP `40..42`, Hst `7..8`, Str `4..5`, Mgk `5..6`
- Starter floor stats: HP `42`, Hst `8`, Str `5`, Mgk `6`

The Hazel starter package SystemConsole assertion was updated to match the corrected Tier 1 stats.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\Definitions\C_Special_EphemrialSpirit_Hazel.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\StarterPets\StarterPetCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\EphemrialSpiritStarterPetTests.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-unity-hazel-validation-fix-report.md`

## Checks run

From `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`:

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore`
  - Passed.
  - Existing warnings only:
    - `InMemoryGameCOnfigProvider.cs(138,17): warning CS0162: Unreachable code detected`
    - `WorldMapSurfaceBuilder.cs(645,24): warning CS0649: FoldedContributorGlyphs is never assigned`
    - `UIShellBootstrap.cs(370,22): warning CS0649: _craftCreateV2SummaryName is never assigned`
- Direct fresh-assembly catalog validation:
  - Passed.
  - `CatalogCount=359`
  - `Hazel=Hazel Hst=7..8 Mgk=5..6`
- Direct fresh-assembly Hazel starter package validation:
  - Passed.
  - `HazelStats=HP:42 Hst:8 Str:5 Mgk:6`
- `rg` fixed-string stale checks for Hazel `hst: 10`, `mgk: 7`, `minHst: 9`, and `maxHst: 10`
  - No stale matches in the touched creature/test surfaces.
- `git diff --check` on touched source/test paths
  - Passed.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile`
  - Blocked because another Unity instance has this project open.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-editmode -TestFilter SystemConsole`
  - Blocked because another Unity instance has this project open.

## Cleanup performed

No scratch files or screenshots were created. Unity automation logs were retained under `artifacts\unity-automation\` as check evidence.

## Risks

The open Unity editor still had stale Hazel exceptions in `Editor.log` after the fix. The fresh C# assemblies validate correctly, so the remaining editor red should be rechecked after Unity completes a clean script/domain reload or after closing the open editor and running batch tests.

Because the full SystemConsole run is blocked by the open Unity instance, additional non-Hazel failures may still be present behind this initial catalog initialization blocker.

## Memory-worthy notes

Hazel should remain a Cunning utility Ephemrial Spirit starter, but her Tier 1 stats must stay within Hst max `8` and Mgk max `6` unless the Tier 1 template itself is intentionally redesigned.

## Do not promote to memory

Do not promote as full SystemConsole-clean. This only clears the known Hazel catalog bootstrap blocker in source and fresh assemblies.

## Next recommended gate

Trigger a clean Unity script/domain reload, then rerun the SystemConsole list. If failures cascade again, take the next topmost non-stale exception and fix that blocker next.
