# TWB Trenchworks Full Command Research Package Report

Date: 2026-05-22

## Scope

Standalone TWB-tagged game: TWB Trenchworks only.

## What Changed

- Created a comprehensive GPT Pro upload package at:
  - `C:\Users\yrred\Downloads\twb-trenchworks-full-command-research-package.zip`
- Added a dedicated GPT Pro usage guide:
  - `HOW_TO_USE_IN_GPT_PRO.md`
- Updated the package README with a file map and explicit upload instructions.
- Updated the current game-dev task brief to reflect this research-package gate.

## Package Contents

- `README.md`
- `HOW_TO_USE_IN_GPT_PRO.md`
- `00_MASTER_GPT_PRO_PROMPT.md`
- `01_CURRENT_SYSTEM_AND_SCOPE.md`
- `02_FULL_ORDER_OF_BATTLE_50_SQUADS.md`
- `03_SOLDIER_ROLES_33.md`
- `04_HARDPOINT_EMPLACEMENT_FAMILIES_12.md`
- `05_MAN_EMPLACEMENT_MODE_REQUIREMENTS.md`
- `06_REQUIRED_OUTPUT_PACKET.md`
- `07_SINGLE_PASTE_PROMPT_FULL_CONTEXT.md`

## Coverage

The package explicitly includes:

- all 50 planned deployable squad templates
- all 33 soldier/member roles
- all 12 hardpoint/emplacement families
- the 4 current live bootstrap squads
- the 3 player-facing tier model
- the distinction between soldier role, deployable squad, and emplacement
- man-emplacement mode where the emplacement becomes the local tactical brain
- Player General and Enemy General planning requirements
- deterministic output requirements: mission matrices, fallback matrices, state machines, scoring rules, and tests

## Checks Run

- Verified package folder contents.
- Verified key terms for 50 squad templates, 33 roles, 12 hardpoint families, and man-emplacement mode appear across the package.
- Built the zip with PowerShell `Compress-Archive`.
- Inspected the zip entries after compression.

## Child Review

Child audit feedback was incorporated before packaging:

- make the package usable without code access
- explicitly list all 50 deployable templates, 33 roles, and 12 hardpoint families
- distinguish soldier roles from squad templates
- include the 3-tier player-facing mapping
- include man-emplacement mode and emplacement local-brain behaviour
- require reusable mission families with template-specific overrides
- require deterministic fallback and test coverage instead of vague AI language

## Cleanup Performed

- No Unity source files were modified for this task.
- No raw GPT Pro/Obsidian package files were modified.
- No staging, commits, resets, or broad cleanup were performed.

## Risks

- GPT Pro may still try to summarize instead of generating the requested markdown packet; `HOW_TO_USE_IN_GPT_PRO.md` includes a warning and exact starter prompt to counter that.
- The package is planning-oriented and not code-derived line-by-line; implementation workers must still reconcile the returned plan against the live Unity code.
- The full 50-template system is intentionally larger than the current 4-unit bootstrap and will need gated implementation.

## Memory-Worthy Notes

- The intended Trenchworks command system is a full 50 squad-template / 33 soldier-role / 12 hardpoint-family design, not the current 4-unit bootstrap.
- Emplacements should be planned as local tactical brains once manned, with squads supplying crew and leaders acting as command links/fallback authorities.
- The research output should use deterministic doctrine: scoring, state machines, fallback matrices, and tests.

## Follow-Up Recommendations

1. Upload the zip to GPT Pro and require the 18-file markdown implementation packet.
2. Audit GPT Pro's returned packet against the 50/33/12 acceptance checklist.
3. Only then create a Unity implementation gate for roster diagnostics, General assignment, Enemy General assignment, and emplacement-brain foundations.
