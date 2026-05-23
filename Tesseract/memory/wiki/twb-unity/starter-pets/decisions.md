# Starter Pet Decisions

## Active Decisions

- Decision - Starter pets use the special identity/display lane `Ephemrial Spirit`, but normal runtime combat/content contracts still apply.
- Decision - Starter pets do not receive monster versions.
- Decision - Peggy is a support starter pet with spiritual protection powers.
- Decision - Peggy's skill is Threshold Ward and its combat affinity is `AffinityId.Faith`.
- Decision - Stanly is an attack starter pet.
- Decision - Stanly's skill is Prancing Bite and its combat affinity is `AffinityId.Might`.
- Decision - Peggy and Stanly should be high-end Tier 1, not over-tier.
- Decision - Peggy and Stanly companion cards are `ItemRarity.Legendary`.
- Decision - Starter selection UI is deferred and should not be included in the current starter package wiring gate.
- Decision - Protected starter-pet role resolution must come from `StarterPetDefinition` role metadata, not raw stat dominance, so Atk/Util roles can coexist with the documented Tier 1 envelopes.
- Fact - Peggy's Tier 1 envelope is `MaxHp 45`, `Hst 8`, `Str 8`, `Mgk 6`; Stanly's Tier 1 envelope is `MaxHp 45`, `Hst 8`, `Str 10`, `Mgk 5`.
- Decision - Chuck is a Might / Defense Ephemrial Spirit starter pet.
- Decision - Chuck's skill is `Chuck's Porch Sentinel` with skill id `defskill_special_chuck_porch_sentinel`.
- Decision - Chuck should be an isolated pet sprite only, with no background scene, prop, platform, fruit, mound, or object perch.
- Fact - Chuck's accepted Tier 1 stat line is `MaxHp 45`, `Hst 5`, `Str 9`, `Mgk 3`.

## Superseded Or Rejected

- Superseded - Earlier over-tier stat ideas for Peggy or Stanly are replaced by the user's Tier 1 envelope correction.
- Rejected - `AffinityId.Unknown` is not acceptable for starter skills, creatures, cards, or metadata.
- Rejected - Monster/enemy mirror versions are not created for starter pets.

## Sources

- [[short-term/2026-05-12-twb-starter-pets-working-window-intake]]
- [[short-term/2026-05-13-twb-unity-starter-pets-worker-final-decommission-report]]
