# Final Decommission Report - 2026-05-13 - TWB Unity Starter Pets Worker

## Window identity
- Project/window name: TWB Unity Starter Pets Worker
- Scope: Main game / The World Beneath starter pets; final handled task was Chuck, a defensive Ephemrial Spirit groundhog starter pet.
- Code/project directory: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`
- Related Obsidian lane, if known: `memory/wiki/twb-unity/starter-pets/` and `memory/short-term/`

## Current state
Chuck exists as a full Ephemrial Spirit starter pet package in the main Unity project.

Working:
- Chuck is registered in the starter catalog as Might / Defense.
- Chuck has a creature definition, Legendary companion card, rare skill card, primary skill definition, defense runtime catalog entry, service package helpers, and SystemConsole starter-pet test coverage.
- Chuck's companion card references exact creature id `creature_special_ephemrial_spirit_chuck`.
- Chuck's skill card references exact skill id `defskill_special_chuck_porch_sentinel`.
- Chuck uses Tier 1 stats `48/4/9/3` and a matching Tier 1 envelope.
- Chuck uses real A-Series affinity `AffinityId.Might`.
- No monster/enemy mirror for Chuck was introduced.
- Chuck's final art asset is an isolated transparent groundhog pet sprite with no porch, prop, platform, fruit, mound, or background.

Unfinished:
- Unity batch compile and focused edit-mode tests still need to run successfully after the open Unity editor instance is closed or the checks are run from the active editor.
- Chuck's generated sprite needs user/Bob art acceptance.

## Files changed
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\StarterPets\StarterPetCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\Definitions\C_Special_EphemrialSpirit_Chuck.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\Definitions\C_Special_EphemrialSpirit_Chuck.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\Catalog\CreatureCatalogRegistry.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\Definitions\CARD_Companion_Special_EphemrialSpirit_Chuck.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\Definitions\CARD_Companion_Special_EphemrialSpirit_Chuck.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\Definitions\CARD_Skill_Chuck_Porch_Sentinel_v1.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\Definitions\CARD_Skill_Chuck_Porch_Sentinel_v1.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\Catalog\ItemCatalogRegistry.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Skills\Catalog\Definitions\SkillDef_ChuckPorchSentinel.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Skills\Catalog\Definitions\SkillDef_ChuckPorchSentinel.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Skills\Catalog\SkillCatalogRegistry.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Skills\Defense\Catalog\DefenseSkillCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Services\StarterPets\EphemrialSpiritStarterPackageService.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\EphemrialSpiritStarterPetTests.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\SystemConsoleTestRegistry.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\PetIcons\Special\EphemrialSpirit\def-chuck-creature-special-ephemrial-spirit-chuck.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\PetIcons\Special\EphemrialSpirit\def-chuck-creature-special-ephemrial-spirit-chuck.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\PetIcons\Special\EphemrialSpirit\special-ephemrial-spirit-chuck-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\PetIcons\Special\EphemrialSpirit\special-ephemrial-spirit-chuck-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\def-chuck-creature-special-ephemrial-spirit-chuck.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\def-chuck-creature-special-ephemrial-spirit-chuck.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\StarterPets\EphemrialSpirit\Chuck\CHUCK_STARTER_PET_PROJECT_FILE.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\StarterPets\EphemrialSpirit\Chuck\chuck_starter_pet_manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\StarterPets\EphemrialSpirit\Chuck\GeneratedArt\def-chuck-creature-special-ephemrial-spirit-chuck-source-magenta.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\StarterPets\EphemrialSpirit\Chuck\GeneratedArt\def-chuck-creature-special-ephemrial-spirit-chuck-transparent.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\TWB.Domain.csproj`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-unity-chuck-starter-pet-package-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-unity-starter-pets-worker-final-decommission-report.md`

## Important decisions or discoveries
- Chuck should be Might / Defense, not Faith / Defense, so he complements Nova instead of duplicating Nova's Faith team-cover identity.
- Chuck's skill is `Chuck's Porch Sentinel`, a self-targeted Might defensive skill using `def_might_boulder_guard` and `def_might_bristling_carapace`.
- Chuck's art must follow the corrected starter-pet sprite rule: isolated pet only, no background scene or object perch.
- The project currently has a very dirty/untracked working tree unrelated to this task. Do not assume all dirty files came from this worker.

## Tests or checks run
- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore`
  - Result: passed, 0 warnings, 0 errors.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile`
  - Result: attempted; Unity batchmode aborted because another Unity instance has `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype` open.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-editmode -TestFilter EphemrialSpiritStarterPet`
  - Result: attempted; Unity batchmode aborted because another Unity instance has the project open.
- `rg -n "Chuck|chuck" ...`
  - Result: Chuck references were found in starter package/catalog/service/test paths, not in enemy mirror paths.
- PNG alpha validation with Pillow
  - Result: final runtime and key art PNGs are 1254x1254 RGBA with transparent corners.

## Cleanup performed
- No scratch files were removed because no throwaway project scratch files were created.
- Generated project artifacts were retained because they are deliverables or evidence.
- Unity automation artifacts remain at:
  - `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\artifacts\unity-automation\20260513-111537`
  - `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\artifacts\unity-automation\20260513-111600`
  They remain as evidence for blocked Unity compile/edit-mode attempts.
- Original generated image remains at:
  - `C:\Users\yrred\.codex\generated_images\019e1cca-ee11-78e2-8398-e66d710fbb3c\ig_0ac9c3603147d143016a04a0c4a24c8196a1713dcea6b8266b.png`
  It was left in place per generated-image handling guidance.

## Risks / warnings
- Do not run broad cleanup or revert operations; the worktree contains many unrelated dirty/untracked/deleted files.
- Do not add `special_ephemrial_spirit` to the global biome registry just to satisfy starter pets.
- Do not rename `ephemrial` casually.
- Do not create monster/enemy mirror versions of starter pets.
- Do not treat Chuck art as accepted until Bob/user explicitly accepts it.
- Unity focused tests remain unverified because of the open Unity editor lock.

## Blockers
- Unity editor/project lock blocked batchmode compile and edit-mode test automation.
- Chuck art acceptance is still pending.
- No blocker remains for C# solution build.

## Memory-worthy notes
- Chuck is an Ephemrial Spirit Might / Defense starter pet.
- Chuck uses `starter_ephemrial_spirit_chuck`, `creature_special_ephemrial_spirit_chuck`, and `defskill_special_chuck_porch_sentinel`.
- Chuck's Tier 1 stats are `48/4/9/3`; envelope is MaxHp 46-48, Hst 4-5, Str 8-9, Mgk 2-3.
- Chuck is the second defensive starter after Nova, but his identity is self-anchor Might tank rather than Faith team-cover.
- Starter-pet art acceptance rule should stay explicit: isolated pet sprite only, no scenic background or sitting object.

## Do not promote to memory
- Do not promote the exact generated-image prompt unless Chuck's sprite is accepted.
- Do not promote Unity automation artifact paths.
- Do not promote the unrelated dirty worktree inventory.
- Do not promote the temporary failure state of Unity automation beyond the actionable warning that the editor was open.

## Next recommended gate
Run a narrow verification worker after closing the open Unity editor instance: rerun Unity compile and focused Ephemrial Spirit starter-pet edit-mode tests, then record whether Chuck's sprite is accepted or needs one art revision.
