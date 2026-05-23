# Current TWB Unity Starter Pets Task

## Status

Active - corrected 2026-05-20; current gate is Chuck/Stanly verification after the Chuck package, not a new Merlin/Nova implementation pass.

## Scope

Main game / The World Beneath.

## Project

`C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`

## Goal

Run a narrow verification pass for the current Ephemrial Spirit starter-pet package state while preserving the starter-pet runtime contracts.

## Current Gate

- Rerun Unity compile after the open Unity editor no longer blocks batchmode.
- Rerun focused `EphemrialSpiritStarterPet` edit-mode tests.
- Verify Chuck runtime/catalog/card/skill contracts.
- Confirm Chuck's accepted Tier 1 stat line stays at `MaxHp 45`, `Hst 5`, `Str 9`, `Mgk 3`.
- Verify no monster/enemy mirrors exist for starter pets.
- Review Stanly and Chuck art acceptance status.
- Do not create more starter pets in this verification pass.

## Not In Scope

- Starter selection UI.
- New Merlin, Nova, Hazel, or other starter-pet implementation until the Chuck/Stanly verification gate is closed or Bob explicitly reopens that lane.
- Monster/enemy mirrors for starter pets.
- Broad art-pipeline automation.
- Broad catalog refactors.
- Renaming `ephemrial`.
- Main-game world-map polish.

## Historical Planning Notes

The Merlin and Nova notes below are retained as historical planning context only. They are not the current active gate and should not be used to start new starter-pet implementation without a fresh Bob/orchestrator decision.

## Merlin Package - 2026-05-12

Scope: Main game / The World Beneath.

User-provided direction:

- Name: Merlin.
- Form: Maine Coon.
- Personality: antisocial, prefers lying alone in his room, watches birds, powerful, chitters before he attacks.
- Reference images:
  - `C:\Users\yrred\Downloads\IMG_6397.jpg` - 2160x2880.
  - `C:\Users\yrred\Downloads\IMG_6189.jpg` - 2160x2880.
  - `C:\Users\yrred\Downloads\IMG_7246.jpg` - 2160x2880.

Implementation contract:

- Role: `CreatureRole.Atk`.
- Special affinity id: `StarterPetSpecialAffinityId.EphemrialSpirit`.
- A-Series combat affinity: `AffinityId.Cunning`, chosen for solitary hunter, bird-stalker, chitter-before-pounce behaviour.
- Starter: `starter_ephemrial_spirit_merlin`
- Creature: `creature_special_ephemrial_spirit_merlin`
- Instance: `STARTER_EPHEMRIAL_SPIRIT_MERLIN`
- Companion card: `card_companion_special_ephemrial_spirit_merlin`
- Skill card: `card_skill_merlin_chitter_pounce`
- Primary skill: `atkskill_special_merlin_chitter_pounce`
- Skill display: `Merlin's Chitter Pounce`
- Tier 1 attack floor/envelope target: MaxHp 45, Hst 6, Str 10, Mgk 4.
- Modifier cards: `card_mod_attack_amp_i_t1`, `card_mod_attack_amp_ii_t1`, `card_mod_attack_amp_iii_t1`.
- No starter pet monster/enemy mirror.

Art notes:

- Visual identity: large black-and-white Maine Coon, long shaggy fur, white chest ruff, white muzzle/blaze, white paws, long whiskers, full plume tail, green-yellow eyes.
- Generated art should remain pending user acceptance until explicitly approved.

## Nova Intake - 2026-05-12

Scope: Main game / The World Beneath.

User-provided direction:

- Name: Nova.
- Form: corgi.
- Story role: main book companion / one of the main characters.
- Starter role target: tank / stalwart defender of the starter set.
- Reference images:
  - `C:\Users\yrred\Downloads\IMG_1615.jpg` - 2160x2880.
  - `C:\Users\yrred\Downloads\IMG_1616.jpg` - 2160x2880.
  - `C:\Users\yrred\Downloads\IMG_1617.jpg` - 2160x2880.
  - `C:\Users\yrred\Downloads\IMG_1619.jpg` - 2880x2160.
  - `C:\Users\yrred\Downloads\IMG_1618.jpg` - 2880x2160.
  - `C:\Users\yrred\Downloads\IMG_1613.jpg` - 2160x2880.
  - `C:\Users\yrred\Downloads\IMG_1614.jpg` - 2160x2880.
  - `C:\Users\yrred\Downloads\IMG_1620.jpg` - 2880x2160.

Book/canon sources checked:

- `C:\Users\yrred\Desktop\Archive\preeditaudiobook\full_manuscript\The_World_Beneath_Initiation_2ndPass_StudioReady.txt`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\WikiSystem\pages\CanonWiki\Characters\Book_One_Source_Cast.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\TWB_World_Canon_Mastersheet.md`

Nova personality contract:

- Companion-first, not equipment; her agency must remain visible.
- Loyal, direct, brave, pack-minded, and centered on home being alive.
- Immediate threat response: she moves first, body-checks danger, and protects Carl rather than chasing domination.
- Blunt, hopeful, stubborn, funny in a practical way; not sage-like or solemn.
- Best design anchor: "hold what we can hold" / porchline defense / home-line guardian.

Recommended starter contract for the next implementation gate:

- Role: `CreatureRole.Def`.
- Special affinity id: `StarterPetSpecialAffinityId.EphemrialSpirit`.
- Recommended A-Series combat affinity: `AffinityId.Faith`, because Nova reads as loyalty, vow, sanctuary, home, and defense under pressure. Risk: Peggy is already Faith, so Bob/user should explicitly accept the starter-set repeat.
- Alternate A-Series combat affinity if starter affinity spread matters more than book truth: `AffinityId.ArcaneFighting`, framed as warded stance and guarded circles. This is less character-true than Faith.
- Do not use `AffinityId.Unknown`.
- Proposed IDs:
  - Starter: `starter_ephemrial_spirit_nova`
  - Creature: `creature_special_ephemrial_spirit_nova`
  - Instance: `STARTER_EPHEMRIAL_SPIRIT_NOVA`
  - Companion card: `card_companion_special_ephemrial_spirit_nova`
  - Skill card: `card_skill_nova_porchline_stand`
  - Primary skill: `defskill_special_nova_porchline_stand`
- Proposed display names:
  - Companion Card - Nova (Ephemrial Spirit)
  - Skill Card - Nova's Porchline Stand
- Proposed Tier 1 DEF floor/envelope target: MaxHp 45, Hst 6, Str 8, Mgk 5; keep all values within locked T1 starter maxima.
- Proposed modifier cards: `card_mod_defense_amp_i_t1`, `card_mod_defense_amp_ii_t1`, `card_mod_defense_amp_iii_t1`.
- No starter pet monster/enemy mirror.
- Companion card must be Legendary and reference `creature_special_ephemrial_spirit_nova` exactly.

Art notes:

- Visual identity: black tri-color corgi, tan eyebrows/cheeks/legs, white chest and front paws, narrow white forehead blaze, dark saddle/back, oversized upright ears, long low body.
- Strong reference coverage exists for front face, side silhouette, back markings, and posture. Some images are cropped or motion-blurred; use them as secondary evidence rather than final key-art acceptance.

Next gate:

- Bob/user should approve Nova's combat affinity and final skill name, then assign a bounded Unity registration pass.

## Read First

- [[hot]]
- [[index]]
- [[wiki/game-dev/project-hierarchy]]
- [[wiki/game-dev/build-test-commands]]
- [[wiki/game-dev/slynyrd-pixelblog-reference]]
- [[wiki/game-dev/external-game-dev-resource-index]]
- [[wiki/twb-unity/overview]]
- [[wiki/twb-unity/starter-pets-guardian-angels]]
- [[wiki/twb-unity/starter-pets/overview]]
- [[wiki/twb-unity/starter-pets/contracts]]
- [[wiki/twb-unity/starter-pets/decisions]]
- [[wiki/twb-unity/starter-pets/art-pipeline]]
- [[wiki/twb-unity/starter-pets/testing]]
- [[wiki/twb-unity/starter-pets/open-questions]]

## Key Source Files

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\StarterPets\StarterPetDefinition.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\StarterPets\StarterPetCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Services\StarterPets\EphemrialSpiritStarterPackageService.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\Catalog\CreatureCatalogRegistry.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\Catalog\ItemCatalogRegistry.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Skills\Catalog\SkillCatalogRegistry.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\EphemrialSpiritStarterPetTests.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\README.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\01_CREATE_PET_ART_MASTER_PROMPT.md`

## Allowed Write Paths

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Skills\`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Services\StarterPets\`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\PetIcons\Special\EphemrialSpirit\`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\StarterPets\EphemrialSpirit\`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\`

## Forbidden Write Paths

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\log.md`
- unrelated UI work unless explicitly assigned
- unrelated catalog refactors
- destructive git operations
- broad cleanup of `Temp` or `.codex\generated_images` without explicit user approval

## Checks

Run from:

```powershell
cd C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype
```

Required after code changes:

```powershell
dotnet build TWB_Phase1_IdlePrototype.sln --no-restore
```

If practical:

```powershell
powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile
powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-editmode -TestFilter EphemrialSpiritStarterPet
```

## Done Criteria

- Unity compile result is reported, or the active editor/batchmode blocker is clearly documented.
- Focused `EphemrialSpiritStarterPet` edit-mode test result is reported, or the exact blocker is documented.
- Chuck runtime/catalog/card/skill contracts are checked.
- Chuck's accepted Tier 1 stat line remains `MaxHp 45`, `Hst 5`, `Str 9`, `Mgk 3`.
- No starter pet monster/enemy mirror is introduced.
- Stanly and Chuck art acceptance status is reviewed without treating unapproved art as final.
- No new starter pet package is implemented unless Bob explicitly reopens that lane.
- Build/check status is reported after code changes.
- Temporary files created by the worker are cleaned up or explained.
- A report is written to `memory/short-term/`.
