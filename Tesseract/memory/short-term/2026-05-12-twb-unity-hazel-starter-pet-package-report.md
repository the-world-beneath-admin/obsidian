# TWB Unity Starter Pets Worker Report - 2026-05-12 - Hazel Starter Pet Package

## Task

Build Hazel, the Book One squirrel character, into a bounded Ephemrial Spirit guardian angel starter pet package for the main Unity project. Use book/canon material to shape personality, create a starter portrait, wire runtime/catalog/package contracts, and report risks without promoting permanent memory.

## Result

Hazel is implemented as a Cunning utility starter companion. Her canon read is route intelligence, caches, safe paths, fast ways, places gone bad, and fear converted into useful field logistics.

Runtime contract:

- Starter id: `starter_ephemrial_spirit_hazel`
- Creature id: `creature_special_ephemrial_spirit_hazel`
- Creature instance id: `STARTER_EPHEMRIAL_SPIRIT_HAZEL`
- Companion card: `card_companion_special_ephemrial_spirit_hazel`
- Skill card: `card_skill_hazel_safe_cut`
- Primary skill: `utilskill_special_hazel_safe_cut`
- Role: `CreatureRole.Util`
- Combat affinity: `AffinityId.Cunning`
- Tier 1 floor stats: MaxHp 42, Hst 10, Str 5, Mgk 7
- Skill: Hazel's Safe Cut
- Modifier loadout: utility amp I, II, III

Catalog/package wiring was added for the creature catalog, item/card catalog, skill catalog, utility skill runtime catalog, starter package service, and SystemConsole starter-pet test registry. No monster/enemy mirror was introduced.

Generated art was placed at:

- `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/util-hazel-creature-special-ephemrial-spirit-hazel.png`
- `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/special-ephemrial-spirit-hazel-1024.png`

Art correction after user review: the first generated Hazel image included a platform/scene element, which is wrong for a pet sprite. It was replaced with an isolated transparent Hazel sprite with no perch, prop, platform, or background object.

## Files touched

- `Assets/_TWB/Scripts/Domain/Creatures/StarterPets/StarterPetCatalog.cs`
- `Assets/_TWB/Scripts/Domain/Creatures/Definitions/C_Special_EphemrialSpirit_Hazel.cs`
- `Assets/_TWB/Scripts/Domain/Creatures/Catalog/CreatureCatalogRegistry.cs`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Definitions/CARD_Companion_Special_EphemrialSpirit_Hazel.cs`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Definitions/CARD_Skill_Hazel_Safe_Cut_v1.cs`
- `Assets/_TWB/Scripts/Domain/Domain/Items/Catalog/ItemCatalogRegistry.cs`
- `Assets/_TWB/Scripts/Domain/Skills/Catalog/Definitions/SkillDef_HazelSafeCut.cs`
- `Assets/_TWB/Scripts/Domain/Skills/Catalog/SkillCatalogRegistry.cs`
- `Assets/_TWB/Scripts/Domain/Skills/UtilitySkillCatalog.cs`
- `Assets/_TWB/Scripts/Services/StarterPets/EphemrialSpiritStarterPackageService.cs`
- `Assets/_TWB/Scripts/UnityBridge/Editor/SystemConsole/Tests/EphemrialSpiritStarterPetTests.cs`
- `Assets/_TWB/Scripts/UnityBridge/Editor/SystemConsole/Tests/SystemConsoleTestRegistry.cs`
- `TWB.Domain.csproj`
- `Assets/Resources/GameArt/TWB_HoloGlyph_T1/PetIcons/Special/EphemrialSpirit/*hazel*`
- `Documentation/StarterPets/EphemrialSpirit/Hazel/*`
- `.md/T1_Creature_Art_Prompt_System/affinities/special/ephemrial_spirit/util-hazel-creature-special-ephemrial-spirit-hazel.*`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` - passed with 0 warnings and 0 errors after the Hazel package was complete.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile` - blocked because another Unity instance has this project open. Artifact run dir: `artifacts/unity-automation/20260512-135835`.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-editmode -TestFilter EphemrialSpiritStarterPet` - blocked for the same open-project Unity instance guard. Artifact run dir: `artifacts/unity-automation/20260512-135850`.

## Cleanup performed

No scratch source files were created. The original generated image remains in Codex's generated image store as raw generation evidence. The Unity automation artifact folders were kept because they document the project-open blocker.

## Risks

- Hazel has no real-world reference image, so the generated portrait is canon/personality-driven and needs user art acceptance.
- The corrected generated transparent image is 1536x1024, not square. Unity importer metadata matches that rectangle. The existing `special-ephemrial-spirit-hazel-1024.png` naming follows prior key-art naming but should not be read as square-format confirmation.
- Book voice setup labels Hazel as a recurring human character, while the cast wiki and manuscript clearly describe Hazel as a squirrel. I followed the squirrel canon per the user request and source cast note.
- Focused Unity compile/edit-mode verification is still pending because the current project is open in another Unity instance.

## Memory-worthy notes

- Hazel approved direction candidate: Ephemrial Spirit starter, Cunning utility scout, route/cache intelligence, Hazel's Safe Cut, floor stats 42/10/5/7.
- Hazel should remain distinct from Nova: not tank/defender, but pathing/logistics support.
- Hazel should remain distinct from Peggy: utility yes, but Cunning field-intelligence rather than Faith warding.

## Do not promote to memory

- Do not promote the generated art as final accepted art until the user accepts it.
- Do not promote prompt wording or exact image filename implementation details as design canon unless Bob/orchestrator chooses to.
- Do not promote Unity automation blocker artifacts as durable project truth beyond this run's check status.

## Next recommended gate

User/Bob art acceptance for Hazel, then rerun Unity compile and focused `EphemrialSpiritStarterPet` edit-mode tests after the existing Unity editor instance is closed or the automation can attach safely.
