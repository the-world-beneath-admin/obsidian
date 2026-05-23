# Starter Pet Contracts

## Runtime Contract

Future starter pets must have:

- a `CreatureCatalogRegistry` entry
- a companion card that references the exact creature id
- valid Tier 1 stat envelope
- `ItemRarity.Legendary` companion card
- a real A-Series combat affinity
- skill, card, and catalog metadata
- starter package service support when assigned
- no monster or enemy mirror version

## Special Identity Rule

The starter identity/display lane may be special, such as `Ephemrial Spirit`, but runtime combat and content contracts still use normal validated systems.

- Do not use `AffinityId.Unknown` for starter creatures, skills, cards, or metadata.
- Do not weaken validators to force starter pets through.
- Do not add `special_ephemrial_spirit` to the global biome registry merely to satisfy starter pets.
- Do not rename `ephemrial` casually; it is existing file/id spelling and needs migration if changed.

## Known Stat Envelopes

- Peggy target envelope: HP 42-45, Hst 7-8, Str 6-8, Mgk 5-6.
- Stanly target envelope: HP 42-45, Hst 6-8, Str 9-10, Mgk 3-5.
- Tier 1 maximums called out by the user: Hst <= 8, Mgk <= 6, Str <= 10, MaxHp <= 45.
- Fact - Chuck's accepted starter stats are `45/5/9/3`.
- Superseded - Earlier Chuck `48/4/9/3` memory is replaced by the later validation fix.

## Current Starters

- Peggy: support starter, Faith utility, Threshold Ward.
- Stanly: attack starter, Might attack, Prancing Bite.
- Chuck: defensive starter, Might defense, `Chuck's Porch Sentinel`.

## Sources

- [[short-term/2026-05-12-twb-starter-pets-working-window-intake]]
- [[short-term/2026-05-13-twb-unity-starter-pets-worker-final-decommission-report]]
