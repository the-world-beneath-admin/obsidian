# TWB Unity Starter Pets Worker Report - 2026-05-13 - Chuck Starter Pet Package

## Task

Build Chuck, the local front-porch groundhog, into a defensive Ephemrial Spirit guardian angel starter pet for the main Unity project. Keep the work bounded to starter-pet package wiring, starter contracts, focused tests, and isolated pet-sprite art.

## Result

Implemented Chuck as a Might / Defense Ephemrial Spirit starter pet.

- Starter id: `starter_ephemrial_spirit_chuck`
- Creature id: `creature_special_ephemrial_spirit_chuck`
- Companion card: `card_companion_special_ephemrial_spirit_chuck`
- Skill card: `card_skill_chuck_porch_sentinel`
- Primary skill: `defskill_special_chuck_porch_sentinel`
- Defense runtime contract: `DefenseSkillTargetRule.Self`
- Defense states: `def_might_boulder_guard`, `def_might_bristling_carapace`
- Tier 1 stats: `48/4/9/3` MaxHp/Hst/Str/Mgk
- Tier 1 envelope: MaxHp 46-48, Hst 4-5, Str 8-9, Mgk 2-3
- Starter modifier loadout: Defense Amp I, II, III

Generated and installed an isolated transparent Chuck pet sprite. No porch, fruit, props, platform, dirt mound, or scenery are present in the final transparent asset.

## Files touched

- `Assets/_TWB/Scripts/Domain/Creatures/StarterPets/StarterPetCatalog.cs`
- `Assets/_TWB/Scripts/Domain/Creatures/Definitions/C_Special_EphemrialSpirit_Chuck.cs`
- `Assets/_TWB/Scripts/Domain/Creatures/Definitions/C_Special_EphemrialSpirit_Chuck.cs.meta`
- `Assets/_TWB/Scripts/Domain/Creatures/Catalog/CreatureCatalogRegistry.cs`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Definitions/CARD_Companion_Special_EphemrialSpirit_Chuck.cs`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Definitions/CARD_Companion_Special_EphemrialSpirit_Chuck.cs.meta`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Definitions/CARD_Skill_Chuck_Porch_Sentinel_v1.cs`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Definitions/CARD_Skill_Chuck_Porch_Sentinel_v1.cs.meta`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Catalog/ItemCatalogRegistry.cs`
- `Assets/_TWB/Scripts/Domain/Skills/Catalog/Definitions/SkillDef_ChuckPorchSentinel.cs`
- `Assets/_TWB/Scripts/Domain/Skills/Catalog/Definitions/SkillDef_ChuckPorchSentinel.cs.meta`
- `Assets/_TWB/Scripts/Domain/Skills/Catalog/SkillCatalogRegistry.cs`
- `Assets/_TWB/Scripts/Domain/Skills/Defense/Catalog/DefenseSkillCatalog.cs`
- `Assets/_TWB/Scripts/Services/StarterPets/EphemrialSpiritStarterPackageService.cs`
- `Assets/_TWB/Scripts/UnityBridge/Editor/SystemConsole/Tests/EphemrialSpiritStarterPetTests.cs`
- `Assets/_TWB/Scripts/UnityBridge/Editor/SystemConsole/Tests/SystemConsoleTestRegistry.cs`
- `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/def-chuck-creature-special-ephemrial-spirit-chuck.png`
- `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/def-chuck-creature-special-ephemrial-spirit-chuck.png.meta`
- `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/special-ephemrial-spirit-chuck-1024.png`
- `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/special-ephemrial-spirit-chuck-1024.png.meta`
- `.md/T1_Creature_Art_Prompt_System/affinities/special/ephemrial_spirit/def-chuck-creature-special-ephemrial-spirit-chuck.md`
- `.md/T1_Creature_Art_Prompt_System/affinities/special/ephemrial_spirit/def-chuck-creature-special-ephemrial-spirit-chuck.png`
- `Documentation/StarterPets/EphemrialSpirit/Chuck/CHUCK_STARTER_PET_PROJECT_FILE.md`
- `Documentation/StarterPets/EphemrialSpirit/Chuck/chuck_starter_pet_manifest.json`
- `Documentation/StarterPets/EphemrialSpirit/Chuck/GeneratedArt/def-chuck-creature-special-ephemrial-spirit-chuck-source-magenta.png`
- `Documentation/StarterPets/EphemrialSpirit/Chuck/GeneratedArt/def-chuck-creature-special-ephemrial-spirit-chuck-transparent.png`
- `TWB.Domain.csproj`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` - passed, 0 warnings, 0 errors.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile` - attempted; Unity batchmode aborted because another Unity instance has this project open.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-editmode -TestFilter EphemrialSpiritStarterPet` - attempted; Unity batchmode aborted because another Unity instance has this project open.
- `rg -n "Chuck|chuck" ...` over starter/catalog/service/test/enemy paths - confirmed Chuck appears in starter package/catalog/test paths and not as a monster/enemy mirror.
- PNG alpha validation - final runtime and key art PNGs are 1254x1254 RGBA with transparent corners.

## Cleanup performed

No throwaway scratch files were created in the project workspace. Unity automation artifacts were left under `artifacts/unity-automation/20260513-111537` and `artifacts/unity-automation/20260513-111600` as command evidence. The original generated image remains under Codex generated-images storage; project copies are installed in the Unity project.

## Risks

- Unity compile/edit-mode test commands did not execute fully because the Unity project is open in another Unity instance.
- Final Chuck art is generated and should receive user art acceptance, especially because groundhog identity/readability is subjective at icon scale.
- The runtime and key art files are 1254x1254, matching recent special starter art outputs, despite the resource filename retaining the existing `1024` naming convention.
- The Unity worktree was already heavily dirty/untracked before this task; no unrelated changes were reverted.

## Memory-worthy notes

- Chuck is the second tank-style Ephemrial Spirit starter after Nova, but he is Might / Defense and self-anchor, not Faith team-cover.
- Chuck's gameplay identity: porch-sentinel groundhog, sturdy and friendly, using `Chuck's Porch Sentinel`.
- Chuck's stats: `48/4/9/3`, envelope MaxHp 46-48, Hst 4-5, Str 8-9, Mgk 2-3.
- Chuck art rule: isolated pet sprite only, no porch/background/props/platform.

## Do not promote to memory

- Do not promote the exact generated-image prompt as permanent canon unless the art is accepted.
- Do not promote Unity automation artifact paths.
- Do not promote any unrelated dirty worktree status observed during this task.

## Next recommended gate

Close the open Unity editor instance or run the checks from inside the active editor, then rerun focused Ephemrial Spirit starter pet edit-mode tests. After that, user/Bob should accept or reject Chuck's final sprite.
