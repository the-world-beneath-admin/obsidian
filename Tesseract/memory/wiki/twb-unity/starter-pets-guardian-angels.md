# Starter Guardian Pets

## Summary

Peggy and Stanly are special "guardian angel" starter pets in the main Unity project. Their file and id family spelling currently uses `ephemrial`; do not casually rename it without a migration plan.

Detailed starter-pet contract memory now lives in [[wiki/twb-unity/starter-pets/overview]].

## Current Decisions

- Peggy is a Faith utility starter.
- Stanly is a Might attack starter.
- Starter guardians should be high-end Tier 1 Legendary creatures, not over-tier stat outliers.
- Do not add `special_ephemrial_spirit` to the global biome registry just to satisfy starter pets.
- Do not weaken tier/stat/skill validators to make Peggy or Stanly pass.
- Special protected starter creatures may skip regular biome/family slice validation, but they still must pass creature envelope, tier, and skill affinity contracts.
- Starter pet special identity and combat A-Series affinity are separate concepts.
- Skills still need exactly one valid A-Series `PrimaryAffinity`.

## Current Risks

- Unity static initialization can leave stale catalog state after validation exceptions until a domain reload/play-mode restart.
- Several starter pet files and catalog files may be untracked or part of a heavily dirty worktree; review carefully before commit.
- The number of planned guardian angel starter pets and their intended A-Series affinities/roles is still open.

## Read-First Implementation Files

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\Catalog\CreatureCatalogAuthority.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Taxonomy\FamilyMetadataRules.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\StarterPets\StarterPetCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\Definitions\C_Special_EphemrialSpirit_Peggy.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Creatures\Definitions\C_Special_EphemrialSpirit_Stanly.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\Definitions\CARD_Companion_Special_EphemrialSpirit_Peggy.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Domain\Items\Definitions\CARD_Companion_Special_EphemrialSpirit_Stanly.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Skills\Catalog\Definitions\SkillDef_PeggyThresholdWard.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\Skills\Catalog\Definitions\SkillDef_StanlyPrancingBite.cs`

## Sources

- [[short-term/2026-05-12-twb-unity-worldmap-working-window-intake]]
- [[short-term/2026-05-12-twb-starter-pets-working-window-intake]]
