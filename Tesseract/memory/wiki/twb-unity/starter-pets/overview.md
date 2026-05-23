# TWB Unity Starter Pets

## Summary

This lane covers special starter pets for the main **The World Beneath** Unity project.

## Project

- Parent project: The World Beneath.
- Project type: Main Unity game.
- Local Unity source: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`.
- Current starter family/display lane: `Ephemrial Spirit`.

## Current State

Peggy, Stanly, and Chuck are special starter pets being wired as archive-ready and dungeon-usable companions.

- Peggy is a calico guardian cat and support starter with spiritual protection powers.
- Stanly is a small black-and-white dog and attack starter with pompous butler energy, prancing, growling, jumping, and biting.
- Chuck is a defensive groundhog starter, reported as Might / Defense with the skill `Chuck's Porch Sentinel`; the later validation fix aligned his accepted stats to `MaxHp 45`, `Hst 5`, `Str 9`, `Mgk 3`.
- Starter selection UI belongs to the website account-creation flow, not the Unity starter-pet package wiring pass.
- The latest Stanly regenerated sprite still requires user acceptance before it should be treated as final.
- Chuck's generated sprite also requires user acceptance before it should be treated as final.

## Current Next Gate

Run a narrow verification pass after the Chuck package:

- rerun Unity compile after the open Unity editor no longer blocks batchmode
- rerun focused Ephemrial Spirit starter-pet edit-mode tests
- verify Chuck runtime/catalog/card/skill contracts
- confirm Chuck's accepted Tier 1 stat line stays at `MaxHp 45`, `Hst 5`, `Str 9`, `Mgk 3`
- verify no monster/enemy mirrors exist for starter pets
- review Stanly and Chuck art acceptance status
- run the appropriate Unity build/test checks

Do not create more starter pets in this verification pass.

## Sources

- [[short-term/2026-05-12-twb-starter-pets-working-window-intake]]
- [[short-term/2026-05-13-twb-unity-starter-pets-worker-final-decommission-report]]
- [[wiki/twb-unity/starter-pets-guardian-angels]]
