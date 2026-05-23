# TWB Unity Starter Pets Worker Report - 2026-05-12 - Nova Intake

## Task

Intake Nova, the user's corgi and book companion, as the next special starter pet candidate for the main Unity project. Read project memory, locate/read book/canon material, identify Nova's personality, and recommend a starter-pet tank contract without making unapproved Unity catalog changes.

## Result

Nova is a strong fit for the starter set's DEF/tank role. Book and canon evidence point to a companion-first guardian: loyal, direct, brave, pack-minded, home-centered, stubbornly hopeful, and quick to put herself between Carl and danger.

Recommended contract for the next gate:

- Role: `CreatureRole.Def`.
- Special affinity: `StarterPetSpecialAffinityId.EphemrialSpirit`.
- Recommended combat affinity: `AffinityId.Faith`, because Nova's strongest signals are loyalty, vow, sanctuary, home, and defense under pressure.
- Affinity risk: Peggy is already Faith. If starter affinity spread is more important than book truth, `AffinityId.ArcaneFighting` is the cleaner alternate, but it is less character-true.
- Candidate skill: `Porchline Stand`.
- Candidate primary skill id: `defskill_special_nova_porchline_stand`.
- Candidate companion card id: `card_companion_special_ephemrial_spirit_nova`.
- Candidate skill card id: `card_skill_nova_porchline_stand`.
- Candidate Tier 1 DEF floor target: MaxHp 45, Hst 6, Str 8, Mgk 5.

No Unity source changes were made in this Nova intake pass.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-unity-starter-pets-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-12-twb-unity-nova-starter-pet-intake-report.md`

## Checks run

- Read required project memory:
  - `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
  - `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
  - `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md`
  - starter-pet overview and contract notes.
- Located and searched book/canon Nova sources:
  - `C:\Users\yrred\Desktop\Archive\preeditaudiobook\full_manuscript\The_World_Beneath_Initiation_2ndPass_StudioReady.txt`
  - `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\WikiSystem\pages\CanonWiki\Characters\Book_One_Source_Cast.md`
  - `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\TWB_World_Canon_Mastersheet.md`
- Checked Unity starter-pet contract shape in:
  - `StarterPetDefinition.cs`
  - `StarterPetCatalog.cs`
  - `CreatureRoleResolver.cs`
  - Peggy/Stanly creature, card, and skill definitions.
- Checked Nova reference image dimensions:
  - `IMG_1615.jpg` 2160x2880
  - `IMG_1616.jpg` 2160x2880
  - `IMG_1617.jpg` 2160x2880
  - `IMG_1619.jpg` 2880x2160
  - `IMG_1618.jpg` 2880x2160
  - `IMG_1613.jpg` 2160x2880
  - `IMG_1614.jpg` 2160x2880
  - `IMG_1620.jpg` 2880x2160
- Build/tests were not run because no Unity code changed.

## Cleanup performed

No temporary files were created.

## Risks

- Nova's recommended `AffinityId.Faith` duplicates Peggy's combat affinity. This is defensible from the book, but Bob/user should approve the repeat before implementation.
- `AffinityId.ArcaneFighting` is the best alternate if starter affinity spread is required, but it weakens the direct loyalty/home/sanctuary read.
- Skill name `Porchline Stand` is a recommendation, not an approved final.
- Art has reference coverage but no generated/accepted starter art yet. Some reference photos are cropped or motion-blurred and should remain secondary evidence.
- Nova is not yet registered in Unity catalogs, cards, skills, package wiring, or tests.

## Memory-worthy notes

- Nova is companion-first and not equipment; her agency should remain visible.
- Canon personality: loyal, direct, brave, pack-minded, home-centered, and immediate in threat response.
- Book anchor for design: "hold what we can hold" and the porchline/home-line defense idea.
- Strong visual identifiers: black tri-color corgi, tan eyebrows/cheeks/legs, white chest and front paws, narrow white forehead blaze, dark saddle/back, oversized upright ears, long low body.

## Do not promote to memory

- Proposed IDs, stat target, and skill name are working recommendations pending Bob/user approval.
- Do not promote the Faith-vs-ArcaneFighting choice as final until the affinity gate is explicitly approved.

## Next recommended gate

Approve Nova's combat affinity and final skill name, then run a bounded Unity implementation pass for catalog registration, companion card, skill card, DEF skill definition, Tier 1 envelope/test updates, and starter package wiring if assigned.
