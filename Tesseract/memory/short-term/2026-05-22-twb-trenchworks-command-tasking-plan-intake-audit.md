# TWB Trenchworks Command Tasking Plan Intake Audit - 2026-05-22

## Scope

Standalone TWB-tagged Unity game: TWB Trenchworks.

## Summary

Intook `C:\Users\yrred\Downloads\twb-trenchworks-command-tasking-system-plan.zip` as raw source evidence, preserved a copy, extracted all package files, and created a combined verbatim transcript with file boundaries. The original downloaded ZIP was not modified.

Ran a full TWB audit using the Helpful Genius / Devil's Advocate / Doe-Eyed Intern triad. The package is a strong future architecture source, but it is not ready to implement directly without a repo-bound Gate 0 verification pass.

## Intake Artifacts

- Original ZIP: `C:\Users\yrred\Downloads\twb-trenchworks-command-tasking-system-plan.zip`
- Original SHA256: `F8E7B8A65F0867EB6E1541688D7A005C969DD6AE06EA733FBB9814B70116CE8A`
- Preserved copy: `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\raw\game-dev\twb-trenchworks-command-tasking-system-plan\2026-05-22\twb-trenchworks-command-tasking-system-plan.zip`
- Extracted files: `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\raw\game-dev\twb-trenchworks-command-tasking-system-plan\2026-05-22\extracted`
- Combined verbatim transcript: `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\raw\game-dev\twb-trenchworks-command-tasking-system-plan\2026-05-22\twb-trenchworks-command-tasking-system-plan-transcript.md`
- Intake manifest: `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\raw\game-dev\twb-trenchworks-command-tasking-system-plan\2026-05-22\intake-manifest.md`

## Package Contents Transcribed

- `00_readme_and_package_manifest.md`
- `01_current_system_analysis.md`
- `02_command_hierarchy_architecture.md`
- `03_data_contracts_and_state_model.md`
- `04_player_general_mission_assignment.md`
- `05_enemy_general_spawn_tasking_difficulty.md`
- `06_squad_mission_catalog.md`
- `07_squad_leader_task_state_machines.md`
- `08_member_role_action_and_reaction_trees.md`
- `09_front_hardpoint_supply_contact_integration.md`
- `10_telemetry_debug_ui_and_playtest_tools.md`
- `11_implementation_gates.md`
- `12_tests_smokes_and_acceptance_criteria.md`
- `13_open_questions_and_risk_register.md`

## Audit Findings

### High - Do Not Implement Directly Yet

The package explicitly says the actual Unity project was not inspected. It should be treated as architecture source material, not as a live implementation brief.

Action: Add a command-system Gate 0 repo-confirmation pass before coding. Confirm exact integration points in `TrenchworksSimulation.cs`, `IntegratedPrototypeSystems.cs`, `WarTeamSlice.cs`, `WarTeamEntities.cs`, `WarIntegrationFacade.cs`, and `PrototypeBootstrap.cs`.

### High - Current Active Gate Conflict

The active Trenchworks brief still says the current gate is contract-v3 trench-art overview review plus a one-biome Unity/F9 runtime proof. Command/tasking-system implementation would displace that lane unless Bob explicitly redirects.

Action: Park this command package as future war-side architecture intake unless Bob says the general system now supersedes the trench-art proof gate.

### High - Existing Claim/Support Systems Must Be Mapped First

The plan proposes a future `CommandClaimRegistry`, but live code already has member socket claims, support requests, front blueprint claims, and related support-resolution helpers.

Confirmed live anchors:

- `WarSubUnit.ClaimedSocketId`
- `WarTeam.SetActiveFrontBlueprintClaim(...)`
- `WarTeamSlice.SupportRequests`
- `WarTeamSlice.FrontBlueprintClaims`
- `WarSupportRequest`
- support request assignment/resolution helpers in `WarTeamSlice.cs`

Action: Do not create a second reservation truth. Gate 0 should document existing claim/support lifecycles and decide whether a command registry wraps, consumes, or replaces only a narrow part later.

### Medium - Gate 1 Is Still Too Large

The proposed Gate 1 includes mission contracts, priorities, general intent, enemy difficulty, score breakdowns, event kinds, mission records, and logs. That is more surface than can be proven by a "no behavior change" gate.

Action: Split Gate 1:

- Gate 1A: event log, director stub, spawn-observed event, no behavior change.
- Gate 1B: minimal mission placeholder/readback only.
- Defer `EnemyDifficultyProfile`, full scoring breakdowns, and member task state until they are needed.

### Medium - Debug Readback Must Arrive Earlier

The plan relies on visibility to prevent hidden AI state, but its debug UI sequencing is inconsistent. Gate 1/2 need at least a minimal readback route or Bob cannot verify "visible mission/reason."

Action: Gate 1 should show only observed spawn/no active mission/recent event. Gate 2 should show mission and assignment reason. Gate 3 can become the richer selected-squad panel.

### Medium - Enemy General Needs Shadow Comparison

Live code currently queues delayed enemy responses from `TrenchworksSimulation.SpawnPlayerWarTeamFromInterface(...)`. Replacing that directly risks changing too many variables at once.

Action: When Enemy General work starts, run the new budgeted director in debug/shadow comparison against the old delayed response before switching behavior. Keep the old path behind a debug fallback until stable.

### Medium - Performance Checks Need Earlier Teeth

The package names performance risk but does not require early allocation/event churn checks. Mission scoring, retasking, and member tasks can become hot-loop trouble if introduced casually.

Action: Add command tick/event-log counters and retask/event rate diagnostics before Gate 4 decision bias or Gate 6 retasking.

## Confirmed Useful Current-Code Anchors

- `WarCommandResult` has `AffectedTeamId`, so the command layer can cleanly identify a newly spawned team.
- `TrenchworksSimulation.SpawnPlayerWarTeamFromInterface(...)` receives the spawn result before queuing the current enemy response.
- `IntegratedPrototypeSystems.SpawnWarTeam(...)` routes through `WarIntegrationFacade.ApplyCommand(new SpawnTeamCommand(...))`.
- Current low-level vocabulary exists: `WarTeamKind`, `WarMemberRole`, `WarOrder`, `WarPosture`, `ContactState`, `TeamDecisionKind`, `HoldReason`, `ContactActionKind`, `TeamTacticalPhase`, and `WarSupportRequestKind`.
- `WarTeamSlice.ChooseDecisionCore(...)` exists and should not become the command-system monolith.

## Child Subagent Results

Helpful Genius:

- The plan has good bones and correctly keeps C# simulation authority.
- Recommended preserving it as future source until the active trench-art runtime proof is resolved or Bob explicitly redirects.
- Recommended Gate 0 repo verification, then Gate 1A/1B split.

Devil's Advocate:

- Main risk is treating prompt-derived facts as repo-verified facts.
- Strongly warned against a second claim/support/front reservation truth.
- Recommended a one-page safe Gate 1 brief after repo confirmation.

Doe-Eyed Intern:

- Identified undefined terms and worker-confusion risks around selected lane/zone, mission state ownership, support requests, hardpoint sockets, claim tokens, visibility, and doctrine.
- Recommended a glossary/preflight checklist before implementation.
- Asked what visible proof Bob wants first: event log, selected-squad mission label, or actual player mission assignment.

## Files Touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\raw\game-dev\twb-trenchworks-command-tasking-system-plan\2026-05-22\intake-manifest.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\raw\game-dev\twb-trenchworks-command-tasking-system-plan\2026-05-22\twb-trenchworks-command-tasking-system-plan-transcript.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\raw\game-dev\twb-trenchworks-command-tasking-system-plan\2026-05-22\twb-trenchworks-command-tasking-system-plan.zip`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\raw\game-dev\twb-trenchworks-command-tasking-system-plan\2026-05-22\extracted\*`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-twb-trenchworks-command-tasking-plan-intake-audit.md`

## Checks Run

- Listed ZIP entries via .NET compression APIs.
- Copied ZIP to raw evidence and verified preserved-copy hash matches original.
- Extracted 14 markdown files from the package.
- Created a combined transcript containing each file's content between `BEGIN FILE` / `END FILE` markers.
- Verified original ZIP after intake:
  - Length: `63727`
  - LastWriteTime: `5/22/2026 11:32:03 AM`
  - SHA256: `F8E7B8A65F0867EB6E1541688D7A005C969DD6AE06EA733FBB9814B70116CE8A`
- Read active Trenchworks brief, current game-dev task, `hot.md`, `index.md`, and project hierarchy.
- Ran three read-only child subagent audits.
- Spot-checked current Unity code for spawn result, support requests, claim fields, and existing enum vocabulary.

## Risks / Fragile Areas

- The package could derail the current trench-art runtime-proof gate if treated as immediate implementation.
- The plan's future `CommandClaimRegistry` could duplicate existing support/front/socket claim state.
- Gate 1 could become too large unless split.
- Enemy General replacement is high risk unless shadow-compared first.
- Debug UI must avoid leaking hidden enemy state in normal player-facing UI.

## Memory-Worthy Notes

- The GPT Pro command/tasking package is preserved as raw source material and transcribed under `memory/raw/game-dev/twb-trenchworks-command-tasking-system-plan/2026-05-22/`.
- The package is planning-only and says the live Unity project was not inspected.
- The safest first implementation stance is shadow-only: event log, command director stub, spawn observation, no behavior change.
- Existing claim/support/front systems must be audited before adding a new command claim registry.
- Open question: whether command/tasking work now supersedes the active trench-art Unity/F9 proof gate.

## Do Not Promote

- Do not promote the detailed enum/class lists as confirmed implementation truth yet.
- Do not promote enemy difficulty values or scoring formulas yet.
- Do not treat the full mission catalog as accepted phase-1 scope yet.
- Do not treat this intake as Unity/F9 art validation.

## Cleanup Performed

No temporary extraction folders were left outside the preserved raw intake folder. No source files, user files, reports, or raw evidence were deleted.

## Next Recommended Gate

Create a no-code Gate 0 command-system preflight brief: map the package assumptions to current Unity code, decide sidecar-vs-entity mission state for Gate 1, define the first visible proof Bob wants, and park command implementation behind the current trench-art runtime proof unless Bob explicitly redirects.
