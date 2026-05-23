# TWB Trenchworks Command Plan Fit Audit Report

Date: 2026-05-22
Worker: TWB Trenchworks standing worker
Scope: TWB Trenchworks standalone Unity 2D game

## What Changed

Audited the transcribed command-system implementation packet against the live TWB Trenchworks Unity project and wrote a tailored implementation audit:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\implementation-packets\command-system-2026-05-22\19_twb_plan_fit_audit_and_tailored_implementation.md`

Also retargeted the current game-dev brief from the completed GPT Pro packaging task to this plan-fit audit/tailoring task.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\implementation-packets\command-system-2026-05-22\19_twb_plan_fit_audit_and_tailored_implementation.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-twb-trenchworks-command-plan-fit-audit-report.md`

## Checks Run

- Read required memory context: `hot.md`, `index.md`, `project-hierarchy.md`, and `current-twb-trenchworks-task.md`.
- Confirmed the transcribed implementation packet exists under project docs.
- Inspected live code surfaces for roster, roles, hardpoints, command, general assignment, enemy response, mission hints, squad leader tasks, claim registry, front blueprint anchors, and UI unit buttons.
- Spawned one bounded read-only child subagent for an independent code-fit audit; it made no file edits.
- Confirmed the tailored audit doc exists and contains the next-gate, mission-family, enemy-general, and emplacement sections.

No Unity compile, Play Mode, or C# test run was performed because this was a documentation/audit pass only.

## Audit Verdict

The GPT Pro packet is a strong target model, but it is ahead of the runtime and must be tailored through adapters and diagnostics before implementation.

Confirmed live strengths:

- The live project already has 33 member roles, 50 planned squad templates, and 12 hardpoint families.
- The command scaffolding already exists: `WarCommandDirector`, `PlayerGeneral`, `CommandMissionCatalog`, `SquadMissionController`, `SquadLeaderBrain`, `MemberTaskController`, `CommandClaimRegistry`, enemy difficulty/budget code, and enemy shadow response logic.
- The front/blueprint system already has anchors, hardpoint pads, front claims, and socket occupancy data that should be reused for emplacements.

Primary gaps:

- Runtime spawning still uses only four prototype ids: `scout_patrol`, `assault_section`, `fortify_engineers`, and `supply_team`.
- Packet mission names do not directly match live `WarSquadMissionType` values.
- Enemy squads can spawn reactively, but command-layer enemy missions still become `NoActiveMission`.
- Emplacement brains/classes do not yet exist; they should be built as a thin layer over existing front anchors and claim data.
- The UI still has four hardcoded unit buttons, not a catalog-driven Tier 1/2/3 unit tree.

## Tailored Next Gate

Do not implement the whole packet at once.

Recommended first implementation gate:

1. Add a compatibility map for prototype ids, planned ids, packet mission names, live mission types, hardpoint family ids, and runtime anchors.
2. Add diagnostics for 50 template coverage, 33 role task coverage, 12 hardpoint-family coverage, mission-family fallback coverage, and prototype alias coverage.
3. Keep live spawning behavior unchanged until diagnostics pass.

## Risks

- Copying packet names directly into code would create parallel systems rather than improving the current game.
- Switching runtime spawn to all 50 planned templates too early would likely break current UI, research unlocks, and smokes.
- Building all 12 emplacement brains before proving rifle-bay/MG-point manning would create high rework risk.
- Tier 3 specialty units should remain locked behind working normal mission families.

## Memory-Worthy Notes

- Treat the command packet as doctrine and coverage target, not runtime truth.
- The live code already contains a strong partial bridge: 50 planned templates and 12 hardpoint families are data-present, but not runtime-spawn-present.
- The next code gate should be compatibility diagnostics, not new combat behavior.
- Man-emplacement mode should wrap `WarFrontAnchorKind`, `WarFrontBlueprintPiece`, socket claims, hardpoint family definitions, and `CommandClaimRegistry`.

## Cleanup Performed

- Closed the child subagent after receiving its final audit.
- Deleted the heartbeat automation after completing this pass.

## Follow-Up Recommendations

1. Implement the compatibility map and diagnostics as a no-behavior-change gate.
2. Add a mission-family mapping table before expanding `WarSquadMissionType`.
3. Wire enemy command missions before tuning enemy difficulty.
4. Prove only rifle bay and MG point for the first man-emplacement implementation.
