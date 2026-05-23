# TWB Unity Starter Pets Worker Report - 2026-05-12 - Peggy Stanly Verification

## Task

Run the next bounded starter-pet milestone for the main Unity game, The World Beneath: verify Peggy and Stanly as valid special starter pets without touching starter selection UI, world-map work, broad catalog refactors, monster mirrors, or permanent Obsidian memory.

## Result

Peggy and Stanly now satisfy the intended starter-pet runtime contract in the checked code path after narrow fixes.

- Peggy remains `AffinityId.Faith`, utility role, Threshold Ward.
- Stanly remains `AffinityId.Might`, attack role, Prancing Bite.
- Creature catalog entries are registered for exact ids:
  - `creature_special_ephemrial_spirit_peggy`
  - `creature_special_ephemrial_spirit_stanly`
- Companion cards are registered as `ItemRarity.Legendary` and reference the exact creature ids.
- Skill definitions are registered with real A-Series primary affinities.
- Starter skill-card item metadata now uses real A-Series affinity strings: `faith` for Peggy and `might` for Stanly.
- Runtime starter package stats now use the documented Tier 1 envelopes:
  - Peggy: MaxHp 45, Hst 8, Str 8, Mgk 6.
  - Stanly: MaxHp 45, Hst 8, Str 10, Mgk 5.
- Protected starter role resolution now uses the starter-pet definition role instead of forcing base-stat dominance that would break the Tier 1 stat envelope.
- No Peggy, Stanly, or Ephemrial starter mirror appeared in the enemy/mirrored-monster search.
- No `AffinityId.Unknown` or `StarterPetCatalog.EphemrialSpiritStableId` usage remains in the inspected starter creature, skill-card, and skill-definition contract files.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\StarterPets\StarterPetCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Services\StarterPets\EphemrialSpiritStarterPackageService.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\Services\CreatureRoleResolver.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\Definitions\CARD_Skill_Peggy_Threshold_Ward_v1.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\Definitions\CARD_Skill_Stanly_Prancing_Bite_v1.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\EphemrialSpiritStarterPetTests.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-12-twb-unity-starter-pets-worker-report.md`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore`
  - Passed.
  - 0 errors.
  - 3 existing warnings:
    - `InMemoryGameCOnfigProvider.cs(138,17)` unreachable code.
    - `UIShellBootstrap.cs(370,22)` unassigned `_craftCreateV2SummaryName`.
    - `WorldMapSurfaceBuilder.cs(645,24)` unassigned `FoldedContributorGlyphs`.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile`
  - Attempted.
  - Unity batchmode aborted because another Unity instance has this project open.
  - Automation run dir: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\artifacts\unity-automation\20260512-103759`
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-editmode -TestFilter EphemrialSpiritStarterPet`
  - Attempted.
  - Status: failed because Unity batchmode aborted due another Unity instance already open on the project.
  - `MissingExpectedTestResults: True`.
  - Automation run dir: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\artifacts\unity-automation\20260512-103815`
- `rg` mirror check for `peggy|stanly|ephemrial` under enemy/mirrored catalog paths:
  - Only starter creature registry lines were returned.
- `rg` starter Unknown/special-affinity misuse check:
  - No matches for `AffinityId.Unknown`, `affinityId: "unknown"`, or `affinityId: StarterPetCatalog.EphemrialSpiritStableId` in inspected starter contract files.
- PowerShell image dimension checks:
  - `special-ephemrial-spirit-stanly-1024.png`: 1254x1254, `Format32bppArgb`.
  - `atk-stanly-creature-special-ephemrial-spirit-stanly.png`: 1254x1254, `Format32bppArgb`.
  - `special-ephemrial-spirit-peggy-1024.png`: 1122x1402, `Format24bppRgb`.
  - `util-peggy-creature-special-ephemrial-spirit-peggy.png`: 1254x1254, `Format32bppArgb`.

## Cleanup performed

No scratch files, temporary scripts, generated screenshots, or throwaway logs were created manually.

Unity automation created run artifacts under `artifacts\unity-automation\20260512-103759` and `artifacts\unity-automation\20260512-103815`; these were left in place as check evidence.

No source files, user files, raw evidence, reports, or another worker's work were deleted.

## Risks

- Unity compile/editmode tests did not actually run because another Unity instance has the project open. The dotnet solution build is clean, but the focused Unity test gate still needs a real Unity batchmode run.
- The worktree is heavily dirty and several starter-pet files are currently untracked. Commit/staging should be deliberate and narrow.
- Stanly art remains pending explicit user acceptance.
- Both Stanly 1024-named PNGs are actually 1254x1254. Decide whether to resize to 1024, rename, or accept the mismatch.
- Peggy key art named `special-ephemrial-spirit-peggy-1024.png` is 1122x1402 and `Format24bppRgb`, so it is neither square nor transparent according to the image metadata check.
- Card summary role display may still derive from stat-envelope max values rather than special starter role. Dungeon slot/runtime assignment now uses the protected starter role, but UI role-label polish was outside this task.

## Memory-worthy notes

- Protected starter pets need explicit role authority from `StarterPetDefinition`; raw stat dominance cannot represent Atk/Util roles while also preserving the documented Tier 1 stat envelopes.
- Starter special identity/display lane remains `Ephemrial Spirit`; combat affinities are Faith for Peggy and Might for Stanly.
- Starter skill-card item affinity metadata should use the real A-Series affinity, not `ephemrial_spirit`.
- The `ephemrial` spelling remains unchanged.

## Do not promote to memory

- Do not promote Stanly art as final accepted art yet.
- Do not promote Unity editmode success; the focused Unity tests were blocked by the open Unity instance.
- Do not promote the automation run directories as durable design memory; they are check evidence only.

## Next recommended gate

Close or free the active Unity editor instance, then rerun:

```powershell
powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile
powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-editmode -TestFilter EphemrialSpiritStarterPet
```

After that, ask the user to accept/reject the current Stanly art and decide whether the 1254x1254 assets should be resized or renamed. A later UI-polish gate can decide whether card summary role labels need a special-starter override.
