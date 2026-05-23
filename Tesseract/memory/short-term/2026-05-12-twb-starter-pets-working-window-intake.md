# Working Window Intake - 2026-05-12 - TWB Starter Pets

## Project Identity
- Project/window name: TWB Starter Pets / Ephemrial Spirit starter pets
- Main goal: Build special starter pets for The World Beneath, beginning with Peggy and Stanly, as game-ready archive and dungeon-usable companions.
- Scope: Unity project starter-pet data contracts, creature/item/skill registries, starter package service, tests, pet art assets, and starter pet project documentation. Starter selection UI is explicitly deferred.
- Code/project directory: C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype
- Related Obsidian lane, if known: Unknown; likely TWB_Phase1_IdlePrototype or starter pets.
- Suggested future worker role name: Ephemrial Spirit Starter Pet Worker

## Current State
Peggy and Stanly starter-pet work has been performed in the Unity project, including art/assets/docs and runtime/catalog wiring. The latest user-provided cross-window summary clarified the canonical contract: special starter identity is allowed, but normal runtime combat and content contracts still apply.

Peggy is intended as the first support starter pet: a calico guardian cat with spiritual protection powers. Stanly is intended as an attack starter pet: a small black-and-white dog with pompous British butler energy who prances, growls, jumps, and bites.

Current implementation is paused for this memory intake. Starter selection UI is not started and should remain out of scope until Bob/orchestrator assigns that work.

Stanly image generation had rejected artifact-ridden cleanup attempts. The latest direction was to regenerate Stanly from the original references rather than continue trying to fix the flawed cutout. A regenerated sprite was created using a high-contrast lime-green matte workflow and chroma-keyed to transparent, but Bob/orchestrator should confirm whether the user accepts that asset before more pet work continues.

## Files And Areas Touched
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\StarterPets\StarterPetDefinition.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\StarterPets\StarterPetCatalog.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Services\StarterPets\EphemrialSpiritStarterPackageService.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\Definitions\C_Special_EphemrialSpirit_Peggy.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\Definitions\C_Special_EphemrialSpirit_Stanly.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\Definitions\CARD_Companion_Special_EphemrialSpirit_Peggy.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\Definitions\CARD_Companion_Special_EphemrialSpirit_Stanly.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\Definitions\CARD_Skill_Peggy_Threshold_Ward_v1.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\Definitions\CARD_Skill_Stanly_Prancing_Bite_v1.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Skills\Catalog\Definitions\SkillDef_PeggyThresholdWard.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Skills\Catalog\Definitions\SkillDef_StanlyPrancingBite.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Skills\Attack\Catalog\AttackSkillCatalog.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Skills\Utility\Catalog\UtilitySkillCatalog.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\Catalog\CreatureCatalogRegistry.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\Catalog\ItemCatalogRegistry.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Skills\Catalog\SkillCatalogRegistry.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\EphemrialSpiritStarterPetTests.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\CreatureCatalog\CreatureCatalogIntegrityTest.cs
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\PetIcons\Special\EphemrialSpirit\util-peggy-creature-special-ephemrial-spirit-peggy.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\PetIcons\Special\EphemrialSpirit\special-ephemrial-spirit-peggy-1024.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\PetIcons\Special\EphemrialSpirit\atk-stanly-creature-special-ephemrial-spirit-stanly.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\PetIcons\Special\EphemrialSpirit\special-ephemrial-spirit-stanly-1024.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\StarterPets\EphemrialSpirit\Peggy\
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\StarterPets\EphemrialSpirit\Stanly\STANLY_STARTER_PET_PROJECT_FILE.md
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\StarterPets\EphemrialSpirit\Stanly\stanly_starter_pet_manifest.json
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\StarterPets\EphemrialSpirit\Stanly\ReferenceImages\
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\atk-stanly-creature-special-ephemrial-spirit-stanly.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\atk-stanly-creature-special-ephemrial-spirit-stanly.md
- Peggy reference images: C:\Users\yrred\Downloads\IMG_1604.jpg through C:\Users\yrred\Downloads\IMG_1610.jpg
- Stanly reference images: C:\Users\yrred\Downloads\IMG_1621.jpg through C:\Users\yrred\Downloads\IMG_1625.jpg

## Decisions Made
- Decision - Starter pets use the special identity/display lane "Ephemrial Spirit", but runtime combat/content contracts still require valid normal affinities, catalog entries, and tier-valid stats.
- Source - User TLDR for Bob on 2026-05-12.

- Decision - Starter pets do not receive monster versions.
- Source - User explicitly stated Peggy and all starter pets will not get monster versions.

- Decision - Peggy is a support starter pet with spiritual protection powers.
- Source - User Peggy starter pet request.

- Decision - Peggy's skill is Threshold Ward and its combat affinity is AffinityId.Faith.
- Source - User TLDR for Bob on 2026-05-12.

- Decision - Stanly is an attack starter pet.
- Source - User Stanly starter pet request.

- Decision - Stanly's skill is Prancing Bite and its combat affinity is AffinityId.Might.
- Source - User TLDR for Bob on 2026-05-12.

- Decision - Peggy and Stanly should be high-end Tier 1, not over-tier.
- Source - User TLDR for Bob on 2026-05-12.

- Decision - Peggy stat envelope: HP 42-45, Hst 7-8, Str 6-8, Mgk 5-6.
- Source - User TLDR for Bob on 2026-05-12.

- Decision - Stanly stat envelope: HP 42-45, Hst 6-8, Str 9-10, Mgk 3-5.
- Source - User TLDR for Bob on 2026-05-12.

- Decision - Peggy and Stanly companion cards are ItemRarity.Legendary.
- Source - User TLDR for Bob on 2026-05-12.

- Decision - Future pet sprite generation should start from original references and use high-contrast lime-green or bright-pink matte checks to avoid cutout artifacts.
- Source - User corrections during Stanly art cleanup.

## Memory-Worthy Facts
- Fact - Future starter pets must have a CreatureCatalogRegistry entry, companion card references to the exact creature ID, valid Tier 1 stat envelope, Legendary companion card, real A-Series combat affinity, skill/card/catalog metadata, and no monster mirror.
- Source - User TLDR for Bob on 2026-05-12.

- Fact - The project currently spells the starter special affinity as "Ephemrial Spirit".
- Source - User explicitly supplied "Ephemrial Spirit" as the affinity.

- Fact - Creature tier 1 stat maxes include Hst <= 8, Mgk <= 6, Str <= 10, and MaxHp <= 45.
- Source - User TLDR for Bob on 2026-05-12.

- Fact - If pet art is artifact-ridden, regenerate from original references rather than endlessly patching the flawed image.
- Source - User Stanly art correction.

- Fact - Starter selection UI is deferred and should not be included in the current starter package wiring gate.
- Source - User stated not to worry about how starter pets are selected yet.

- Fact - Peggy was a calico cat, a support pet, a family touchstone, and should be represented with spiritual protection and gravity.
- Source - User Peggy starter pet request.

- Fact - Stanly is a funny small black-and-white dog with pompous British butler energy who prances, growls, jumps, and bites.
- Source - User Stanly starter pet request.

## Risks / Warnings
- Warning - Do not use AffinityId.Unknown for starter skills, old attack/utility skill catalogs, starter pet metadata, or creature definitions.
- Warning - Do not exceed Tier 1 stat envelopes even when describing starters as high-end Tier 1.
- Warning - Special starter identity does not excuse missing registry, card, skill, archive, or dungeon-use contracts.
- Warning - Do not create monster/enemy mirrored versions for starter pets.
- Warning - Avoid patching bad art cutouts for too long; regenerate clean source using contrast matte when artifacts persist.
- Warning - The file special-ephemrial-spirit-stanly-1024.png may be named as 1024 while the generated asset was checked at 1254x1254; confirm intended naming and size.
- Warning - The worktree is very dirty with many unrelated changes; do not revert unrelated user or generated work.
- Warning - Generated scratch files in Temp and .codex\generated_images may exist; do not delete without explicit approval.

## Open Questions
- Is the latest regenerated Stanly sprite accepted by the user?
- Should special-ephemrial-spirit-stanly-1024.png be resized or renamed, or is the current generated size acceptable?
- What is the exact next starter pet identity, role, skill, and combat affinity?
- Where will the starter selection UI live, and what flow will choose Peggy, Stanly, and future starters?
- Should "Ephemrial Spirit" remain display-only while individual combat mechanics use Faith, Might, and other normal A-Series affinities?

## Do Not Promote
- Old flawed Stanly cutout and artifacted sprite attempts.
- Failed edge-cleaning scripts as a durable workflow.
- Any idea that skills or creatures can use AffinityId.Unknown.
- Earlier over-tier combat stat ideas from before the user's TLDR correction.
- Temporary assumption that cyan flares should or should not stay; the durable rule is clean regeneration and user acceptance.
- Temporary contrast preview files and scratch image composites.

## Current Blockers
- Bob/orchestrator review is required before continuing implementation.
- User acceptance is needed for the regenerated Stanly sprite before treating it as final.
- The next starter pet cannot be implemented until its identity, role, and references are provided.

## Checks Run
- Test-Path confirmed C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term exists.
- dotnet build TWB.Domain.csproj --no-restore
- dotnet build TWB.Services.csproj --no-restore
- dotnet build TWB.UnityBridge.EditorTools.csproj --no-restore
- dotnet build TWB.UnityBridge.Tests.csproj --no-restore
- Pillow image checks verified Stanly PNGs as RGBA, 1254x1254, with alpha range (0, 255).
- Lime green, hot pink, and black preview composites were used to inspect Stanly cutout artifacts.
- Regenerated Stanly sprite was created on a lime matte and chroma-keyed to transparent.
- Note: after the cross-window TLDR fixes, final build status should be verified in the implementing window if not already verified there.

## Cleanup Needed
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Temp\stanly-*preview*.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Temp\stanly-clean-preview*.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Temp\stanly-regenerated-*.png
- C:\Users\yrred\.codex\generated_images\019e19a2-5202-72c2-8d51-ddecbd92e2d1\
- Old or failed Stanly generated variants in .codex\generated_images should remain unless the user asks to delete them.
- Confirm whether the "1024" key-art filename is acceptable despite the current 1254x1254 asset dimensions.

## Recommended Obsidian Tree
- memory/wiki/twb-phase1/starter-pets/overview.md
- memory/wiki/twb-phase1/starter-pets/contracts.md
- memory/wiki/twb-phase1/starter-pets/decisions.md
- memory/wiki/twb-phase1/starter-pets/open-questions.md
- memory/wiki/twb-phase1/art-pipeline/pet-sprites.md
- memory/reports/twb-phase1/starter-pets/
- memory/short-term/

## Recommended Worker Agent
- Agent name: Ephemrial Spirit Starter Pet Worker
- Purpose: Implement and verify special starter pets as valid Tier 1 runtime content, including art assets, creature/card/skill definitions, catalogs, starter package service, and tests.
- Read-first files: C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\StarterPets\StarterPetDefinition.cs; C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\StarterPets\StarterPetCatalog.cs; C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Services\StarterPets\EphemrialSpiritStarterPackageService.cs; C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\Catalog\CreatureCatalogRegistry.cs; C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\Catalog\ItemCatalogRegistry.cs; C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Skills\Catalog\SkillCatalogRegistry.cs; C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\README.md; C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\01_CREATE_PET_ART_MASTER_PROMPT.md.
- Allowed write paths: C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\; C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\; C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Skills\; C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Services\StarterPets\; C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\; C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\PetIcons\Special\EphemrialSpirit\; C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\StarterPets\EphemrialSpirit\; C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\; C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\.
- Forbidden write paths: C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\; C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md; C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md; C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\log.md; unrelated UI work unless explicitly assigned; unrelated catalog refactors; destructive git operations.
- Done criteria: Sprite accepted; contracts valid; creature/card/skill catalog registrations complete; no monster mirror exists; Tier 1 stat envelope valid; real combat affinity used; Legendary companion card created; starter package creates an archive-ready and dungeon-usable pet; tests/builds pass; final report goes to memory/short-term/.
- Report destination: memory/short-term/

## Next Recommended Gate
Bob/orchestrator should review this short-term intake, promote durable starter-pet contract rules into permanent memory if desired, then confirm whether regenerated Stanly art is accepted before assigning the next starter pet.
