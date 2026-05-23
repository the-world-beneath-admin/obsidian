# TWB Unity Starter Pets Worker Report - 2026-05-12 - Merlin Starter Pet Package

## Task

Build Merlin, the large antisocial black-and-white Maine Coon, into a full Ephemrial Spirit guardian angel starter pet package for the main Unity project. Scope was the main game / The World Beneath starter-pet package: runtime contracts, catalogs, cards, skill, Tier 1 stats, art package, and focused verification. No starter selection UI, world-map work, monster mirror, or broad refactor.

## Result

Merlin is implemented as a Cunning attack starter companion.

- Starter id: `starter_ephemrial_spirit_merlin`
- Creature id: `creature_special_ephemrial_spirit_merlin`
- Companion card id: `card_companion_special_ephemrial_spirit_merlin`
- Skill card id: `card_skill_merlin_chitter_pounce`
- Primary skill id: `atkskill_special_merlin_chitter_pounce`
- Role: `Atk`
- Combat affinity: `Cunning`
- Tier 1 starter floor stats: MaxHp 45, Hst 6, Str 10, Mgk 4
- Skill: `Merlin's Chitter Pounce`
- Runtime sprite: `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/atk-merlin-creature-special-ephemrial-spirit-merlin.png`
- Key art sprite: `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/special-ephemrial-spirit-merlin-1024.png`

Catalog/package wiring was added for starter definition, creature definition, companion card, skill card, authored skill definition, attack runtime skill catalog, starter package service, and focused SystemConsole coverage. No monster/enemy mirror version of Merlin was introduced.

## Files touched

- `Assets/_TWB/Scripts/Domain/Creatures/StarterPets/StarterPetCatalog.cs`
- `Assets/_TWB/Scripts/Domain/Creatures/Definitions/C_Special_EphemrialSpirit_Merlin.cs`
- `Assets/_TWB/Scripts/Domain/Creatures/Definitions/C_Special_EphemrialSpirit_Merlin.cs.meta`
- `Assets/_TWB/Scripts/Domain/Creatures/Catalog/CreatureCatalogRegistry.cs`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Definitions/CARD_Companion_Special_EphemrialSpirit_Merlin.cs`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Definitions/CARD_Companion_Special_EphemrialSpirit_Merlin.cs.meta`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Definitions/CARD_Skill_Merlin_Chitter_Pounce_v1.cs`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Definitions/CARD_Skill_Merlin_Chitter_Pounce_v1.cs.meta`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Catalog/ItemCatalogRegistry.cs`
- `Assets/_TWB/Scripts/Domain/Skills/Catalog/Definitions/SkillDef_MerlinChitterPounce.cs`
- `Assets/_TWB/Scripts/Domain/Skills/Catalog/Definitions/SkillDef_MerlinChitterPounce.cs.meta`
- `Assets/_TWB/Scripts/Domain/Skills/Catalog/SkillCatalogRegistry.cs`
- `Assets/_TWB/Scripts/Domain/Skills/Attack/Catalog/AttackSkillCatalog.cs`
- `Assets/_TWB/Scripts/Services/StarterPets/EphemrialSpiritStarterPackageService.cs`
- `Assets/_TWB/Scripts/UnityBridge/Editor/SystemConsole/Tests/EphemrialSpiritStarterPetTests.cs`
- `Assets/_TWB/Scripts/UnityBridge/Editor/SystemConsole/Tests/SystemConsoleTestRegistry.cs`
- `TWB.Domain.csproj`
- `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/atk-merlin-creature-special-ephemrial-spirit-merlin.png`
- `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/atk-merlin-creature-special-ephemrial-spirit-merlin.png.meta`
- `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/special-ephemrial-spirit-merlin-1024.png`
- `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/special-ephemrial-spirit-merlin-1024.png.meta`
- `Documentation/StarterPets/EphemrialSpirit/EPHEMRIAL_SPIRIT_STARTER_SET_PLAN.md`
- `Documentation/StarterPets/EphemrialSpirit/Merlin/MERLIN_STARTER_PET_PROJECT_FILE.md`
- `Documentation/StarterPets/EphemrialSpirit/Merlin/merlin_starter_pet_manifest.json`
- `Documentation/StarterPets/EphemrialSpirit/Merlin/ReferenceImages/`
- `Documentation/StarterPets/EphemrialSpirit/Merlin/GeneratedArt/`
- `.md/T1_Creature_Art_Prompt_System/affinities/special/ephemrial_spirit/atk-merlin-creature-special-ephemrial-spirit-merlin.md`
- `.md/T1_Creature_Art_Prompt_System/affinities/special/ephemrial_spirit/atk-merlin-creature-special-ephemrial-spirit-merlin.png`
- `memory/briefs/current-twb-unity-starter-pets-task.md`
- `memory/short-term/2026-05-12-twb-unity-merlin-starter-pet-package-report.md`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed with 0 errors and 3 existing warnings:
  - `InMemoryGameCOnfigProvider.cs(138,17): CS0162 unreachable code`
  - `UIShellBootstrap.cs(370,22): CS0649 _craftCreateV2SummaryName never assigned`
  - `WorldMapSurfaceBuilder.cs(645,24): CS0649 FoldedContributorGlyphs never assigned`
- PowerShell reflection smoke over `Temp/bin/Debug/TWB.Domain.dll` passed:
  - starter id `starter_ephemrial_spirit_merlin`
  - creature id `creature_special_ephemrial_spirit_merlin`
  - role `Atk`
  - affinity `Cunning`
  - stats `HP=45,HST=6,STR=10,MGK=4`
  - creature catalog entry `Merlin`
  - companion card references exact Merlin creature id
  - skill card references exact Merlin skill id
  - skill catalog contains `atkskill_special_merlin_chitter_pounce`
- `rg` over `Assets/_TWB/Scripts/Domain/Enemies` found no `merlin` matches.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile` attempted. The script emitted `Status: probably-clean`, but Unity batchmode aborted because another Unity instance already had the project open.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-editmode -TestFilter EphemrialSpiritStarterPet` attempted. It reported `Status: failed` / `MissingExpectedTestResults: True` because Unity batchmode aborted for the same already-open-project lock.
- PNG asset validation confirmed both Merlin runtime art files are `1254x1254` RGBA with alpha.

## Cleanup performed

No throwaway code or scratch files were left. Unity automation artifacts were retained under `artifacts/unity-automation/20260512-132135` and `artifacts/unity-automation/20260512-132204` as check evidence. The generated magenta-background source image was copied into Merlin documentation evidence before chroma-key removal; raw reference images were preserved.

## Risks

- Merlin is an `Atk` starter, so he overlaps Stanly's attack role. This follows the user direction for a powerful chitter-before-attack cat, but the starter set may need later selection/balance rules if multiple attack starters are available.
- Merlin art is a first-pass generated asset and should be treated as pending user/art acceptance.
- The generated asset includes a small teal bird-like Cunning glint near Merlin. It fits the bird-watching/chitter theme, but should be accepted or rejected by the user.
- The generated asset is `1254x1254`, matching current image output style. Runtime accepts it with `maxTextureSize: 2048`, but a later art gate may still want a strict 1024 export.
- Unity compile/edit-mode verification could not actually run because the project was open in another Unity instance.

## Memory-worthy notes

- Merlin is now the Ephemrial Spirit attack hunter: large antisocial Maine Coon, bird-watcher, room-lord, and chitter-before-pounce attacker.
- Chosen gameplay identity: Cunning / Attack / `Merlin's Chitter Pounce`.
- Starter package uses the same protected companion-card pattern as Peggy, Stanly, and Nova.
- No `AffinityId.Unknown` was used.
- `special_ephemrial_spirit` was not added to the global biome registry.
- No starter-pet monster mirror was introduced.

## Do not promote to memory

Do not promote this first generated Merlin art as final accepted art until the user explicitly accepts it. Do not promote temporary Unity automation lock status as a design fact. Do not promote any broad dirty-worktree status from outside this Merlin starter-pet scope.

## Next recommended gate

Close the already-open Unity editor instance or run the focused checks from that editor, then rerun:

- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile`
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-editmode -TestFilter EphemrialSpiritStarterPet`

After that, get explicit user acceptance or revision notes on Merlin's generated portrait before treating the art as final.
