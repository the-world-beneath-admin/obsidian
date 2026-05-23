# Account Creation Starter Pet Selection

## Requirement

During website account creation, the player must choose exactly 3 starter pets:

- 1 ATK starter
- 1 DEF starter
- 1 UTIL starter

The account creation UI must show:

- pet picture
- brief description
- pet role
- `0/1 ATK`, `0/1 DEF`, and `0/1 UTIL` meters that fill as the player selects
- a clear warning that this is a one-time account-locked choice

## Required Warning Copy

The UI should clearly communicate:

```text
This is a one-time account-locked starter choice. After you create your account, the other starter pets will no longer be available to this account.
```

Exact public copy may be polished, but the warning must remain unambiguous.

## Backend Rules

- The server must validate exactly one selected starter per role.
- The server must reject changes after the account has a completed starter selection.
- The chosen starters should become account-level companion cards.
- Unchosen starter pets should not remain claimable later through the starter-selection path.
- The selection should be auditable through a platform ledger or starter-selection table.

## Current Starter Knowledge

Current known starter pets:

- Peggy: Faith utility, Threshold Ward.
- Stanly: Might attack, Prancing Bite.
- Chuck: Might defense, `Chuck's Porch Sentinel`.

This provides a reported first role-complete trio: one UTIL, one ATK, and one DEF. The full account-creation starter set still needs final images, public descriptions, acceptance status, and any additional choices beyond one pet per role.

## Open Implementation Choice

The worker should decide whether the safest first implementation is:

- registration endpoint accepts starter selection atomically during account creation
- or registration creates the account and immediately requires a first-login starter-selection completion step before the account can use game features

Preference: account creation should feel like one flow to the player.

## Sources

- User requirement on 2026-05-12
- [[wiki/twb-unity/starter-pets/overview]]
- [[wiki/twb-unity/starter-pets/contracts]]
- [[short-term/2026-05-13-twb-unity-starter-pets-worker-final-decommission-report]]
