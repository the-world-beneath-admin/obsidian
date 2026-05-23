# TWB Unity Starter Pets Worker Report - 2026-05-12 - Nova Starter Pet Package

## Task

Build Nova, the black tri-color corgi book character, into a full Ephemrial Spirit guardian angel starter pet package for the main Unity project. Scope was the main game / The World Beneath starter-pet package: runtime contracts, catalogs, cards, skill, Tier 1 stats, art package, and focused verification. No starter selection UI, world-map work, monster mirror, or broad refactor.

## Result

Nova is implemented as the starter set's defense-role guardian.

- Starter id: `starter_ephemrial_spirit_nova`
- Creature id: `creature_special_ephemrial_spirit_nova`
- Companion card id: `card_companion_special_ephemrial_spirit_nova`
- Skill card id: `card_skill_nova_porchline_stand`
- Primary skill id: `defskill_special_nova_porchline_stand`
- Role: `Def`
- Combat affinity: `Faith`
- Tier 1 starter floor stats: MaxHp 45, Hst 6, Str 8, Mgk 5
- Skill: `Nova's Porchline Stand`
- Runtime sprite: `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/def-nova-creature-special-ephemrial-spirit-nova.png`
- Key art sprite: `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/special-ephemrial-spirit-nova-1024.png`

Catalog/package wiring was added for starter definition, creature definition, companion card, skill card, authored skill definition, defense runtime skill catalog, starter package service, and focused SystemConsole coverage. No monster/enemy mirror version of Nova was introduced.

## Files touched

- `Assets/_TWB/Scripts/Domain/Creatures/StarterPets/StarterPetCatalog.cs`
- `Assets/_TWB/Scripts/Domain/Creatures/Definitions/C_Special_EphemrialSpirit_Nova.cs`
- `Assets/_TWB/Scripts/Domain/Creatures/Definitions/C_Special_EphemrialSpirit_Nova.cs.meta`
- `Assets/_TWB/Scripts/Domain/Creatures/Catalog/CreatureCatalogRegistry.cs`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Definitions/CARD_Companion_Special_EphemrialSpirit_Nova.cs`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Definitions/CARD_Companion_Special_EphemrialSpirit_Nova.cs.meta`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Definitions/CARD_Skill_Nova_Porchline_Stand_v1.cs`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Definitions/CARD_Skill_Nova_Porchline_Stand_v1.cs.meta`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Catalog/ItemCatalogRegistry.cs`
- `Assets/_TWB/Scripts/Domain/Skills/Catalog/Definitions/SkillDef_NovaPorchlineStand.cs`
- `Assets/_TWB/Scripts/Domain/Skills/Catalog/Definitions/SkillDef_NovaPorchlineStand.cs.meta`
- `Assets/_TWB/Scripts/Domain/Skills/Catalog/SkillCatalogRegistry.cs`
- `Assets/_TWB/Scripts/Domain/Skills/Defense/Catalog/DefenseSkillCatalog.cs`
- `Assets/_TWB/Scripts/Services/StarterPets/EphemrialSpiritStarterPackageService.cs`
- `Assets/_TWB/Scripts/UnityBridge/Editor/SystemConsole/Tests/EphemrialSpiritStarterPetTests.cs`
- `Assets/_TWB/Scripts/UnityBridge/Editor/SystemConsole/Tests/SystemConsoleTestRegistry.cs`
- `TWB.Domain.csproj`
- `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/def-nova-creature-special-ephemrial-spirit-nova.png`
- `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/def-nova-creature-special-ephemrial-spirit-nova.png.meta`
- `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/special-ephemrial-spirit-nova-1024.png`
- `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/special-ephemrial-spirit-nova-1024.png.meta`
- `Documentation/StarterPets/EphemrialSpirit/EPHEMRIAL_SPIRIT_STARTER_SET_PLAN.md`
- `Documentation/StarterPets/EphemrialSpirit/Nova/NOVA_STARTER_PET_PROJECT_FILE.md`
- `Documentation/StarterPets/EphemrialSpirit/Nova/nova_starter_pet_manifest.json`
- `Documentation/StarterPets/EphemrialSpirit/Nova/ReferenceImages/`
- `Documentation/StarterPets/EphemrialSpirit/Nova/GeneratedArt/`
- `.md/T1_Creature_Art_Prompt_System/affinities/special/ephemrial_spirit/def-nova-creature-special-ephemrial-spirit-nova.md`
- `.md/T1_Creature_Art_Prompt_System/affinities/special/ephemrial_spirit/def-nova-creature-special-ephemrial-spirit-nova.png`
- `memory/briefs/current-twb-unity-starter-pets-task.md`
- `memory/short-term/2026-05-12-twb-unity-nova-starter-pet-intake-report.md`
- `memory/short-term/2026-05-12-twb-unity-nova-starter-pet-package-report.md`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed with 0 warnings and 0 errors.
- PowerShell reflection smoke over `Temp/bin/Debug/TWB.Domain.dll` passed:
  - starter id `starter_ephemrial_spirit_nova`
  - creature id `creature_special_ephemrial_spirit_nova`
  - role `Def`
  - affinity `Faith`
  - stats `HP=45,HST=6,STR=8,MGK=5`
  - creature catalog entry `Nova`
  - companion card references exact Nova creature id
  - skill card references exact Nova skill id
  - skill catalog contains `defskill_special_nova_porchline_stand`
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile` attempted. The script emitted `Status: probably-clean`, but Unity batchmode aborted because another Unity instance already had the project open.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-editmode -TestFilter EphemrialSpiritStarterPet` attempted. It reported `Status: failed` / `MissingExpectedTestResults: True` because Unity batchmode aborted for the same already-open-project lock.
- PNG asset validation confirmed both Nova runtime art files are `1254x1254` RGBA with alpha.

## Cleanup performed

No throwaway code or scratch files were left. Unity automation artifacts were retained under `artifacts/unity-automation/20260512-122127` and `artifacts/unity-automation/20260512-122147` as check evidence. The generated magenta-background source image was copied into Nova documentation evidence before chroma-key removal; raw reference images were preserved.

## Risks

- Nova is `Faith`, which is book-true and guardian-true, but Peggy is also `Faith`. This is a design-balance concern for the starter set, not a runtime blocker.
- Nova art is a first-pass generated asset and should be treated as pending user/art acceptance.
- The generated asset is `1254x1254`, matching the current AI output style. Runtime accepts it with `maxTextureSize: 2048`, but a later art gate may still want a strict 1024 export.
- Unity compile/edit-mode verification could not actually run because the project was open in another Unity instance.

## Memory-worthy notes

- Nova is now the Ephemrial Spirit defense guardian: companion-first, book-canon corgi, home-line protector, and "hold what we can hold" tank.
- Chosen gameplay identity: Faith / Defense / `Nova's Porchline Stand`.
- Starter package uses the same protected companion-card pattern as Peggy and Stanly.
- No `AffinityId.Unknown` was used.
- `special_ephemrial_spirit` was not added to the global biome registry.
- No starter-pet monster mirror was introduced.

## Do not promote to memory

Do not promote this first generated Nova art as final accepted art until the user explicitly accepts it. Do not promote temporary Unity automation lock status as a design fact. Do not promote any broad dirty-worktree status from outside this Nova starter-pet scope.

## Next recommended gate

Close the already-open Unity editor instance or run the focused checks from that editor, then rerun:

- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile`
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-editmode -TestFilter EphemrialSpiritStarterPet`

After that, get explicit user acceptance or revision notes on Nova's generated portrait before treating the art as final.
