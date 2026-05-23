# TWB Trenchworks Command / Tasking System Plan

## Package purpose

This package is an implementation-planning set for a multi-tier command and tasking system in **TWB Trenchworks**, a standalone Unity 2D factory/logistics and automated trench-war simulation under The World Beneath umbrella.

The goal is to give a Codex worker a safe, staged, deterministic plan for moving from the current local `WarTeamSlice.ChooseDecisionCore(...)`-centered behavior toward a bounded command stack:

```text
General Strategy / Spawn Policy
  -> Squad Mission Assignment
    -> Squad Leader Task State
      -> Member Role Task
        -> Member Action / Reaction Tree
```

This is not production code. It is an architecture and implementation plan. Real-world tactics are intentionally abstracted into game simulation behavior such as lane pressure, contact heat, hardpoint sockets, support requests, and front depth.

## Source and scope note

This plan is grounded in the provided planning prompt and its listed current-code vocabulary. The actual Unity project files were not inspected in this package pass. When the prompt lists concrete classes, methods, enums, and current flow, those are treated as confirmed project facts for planning purposes. Any proposed new type, enum, state machine, or gate is marked as a recommendation.

## Files included

| File | Purpose |
|---|---|
| `00_readme_and_package_manifest.md` | Package overview, reading order, executive summary, roadmap. |
| `01_current_system_analysis.md` | Current spawn/team/front/contact/enemy-response analysis and preservation guidance. |
| `02_command_hierarchy_architecture.md` | Proposed command hierarchy, ownership boundaries, sequence diagrams, lifecycle diagrams. |
| `03_data_contracts_and_state_model.md` | Proposed data contracts, enums, records, serialization and determinism notes. |
| `04_player_general_mission_assignment.md` | Player General mission-scoring and retasking plan by squad type. |
| `05_enemy_general_spawn_tasking_difficulty.md` | Enemy General virtual budget, spawn policy, mission assignment, difficulty knobs. |
| `06_squad_mission_catalog.md` | Bounded mission catalog by squad/team type. |
| `07_squad_leader_task_state_machines.md` | Squad Leader state machines and task conversion rules. |
| `08_member_role_action_and_reaction_trees.md` | Member role action catalogs and deterministic reaction trees. |
| `09_front_hardpoint_supply_contact_integration.md` | Front, trench, hardpoint, supply, contact, visibility, and reservation integration. |
| `10_telemetry_debug_ui_and_playtest_tools.md` | Debug overlay, telemetry event names, explainability strings. |
| `11_implementation_gates.md` | Small implementation gates with files touched, tests, acceptance criteria, rollback risks. |
| `12_tests_smokes_and_acceptance_criteria.md` | Deterministic smoke tests and manual Play Mode checks. |
| `13_open_questions_and_risk_register.md` | Open design questions, risk register, recommended next decision before coding. |

## Recommended reading order

1. `01_current_system_analysis.md`
2. `02_command_hierarchy_architecture.md`
3. `03_data_contracts_and_state_model.md`
4. `04_player_general_mission_assignment.md`
5. `05_enemy_general_spawn_tasking_difficulty.md`
6. `06_squad_mission_catalog.md`
7. `07_squad_leader_task_state_machines.md`
8. `08_member_role_action_and_reaction_trees.md`
9. `09_front_hardpoint_supply_contact_integration.md`
10. `10_telemetry_debug_ui_and_playtest_tools.md`
11. `11_implementation_gates.md`
12. `12_tests_smokes_and_acceptance_criteria.md`
13. `13_open_questions_and_risk_register.md`

## Executive summary

The safest path is to add a **command layer above the existing war simulation without breaking current combat**. Keep `WarTeamSlice`, `WarFrontAssignmentPlanner`, `WarTeam`, `WarSubUnit`, and the existing enums as the simulation authority. Add a `WarCommandDirector` that owns a `PlayerGeneral`, `EnemyGeneral`, mission registry, reservation/claim registry, and command event log. In Phase 1, squads receive bounded `WarSquadMission` records, but existing team decision logic continues to perform movement/contact/combat. Then, gate by gate, move broad local decisions into `SquadMissionController`, `SquadLeaderBrain`, and `MemberTaskController`. The enemy should become an RTS-style opponent with a virtual supply/pressure budget, difficulty profiles, fair information limits, and readable spawn reasons rather than a direct “player spawned, enemy replies” prototype.

## One-page implementation roadmap

### Gate 1 — Shadow command contracts and event log

Add mission/difficulty/task/claim/event data contracts and a compact command event log. Attach a current-mission field to `WarTeam` or a sidecar command state map, but do not change squad behavior yet. This gate proves serialization, deterministic IDs, debug strings, and safe observability.

### Gate 2 — Player General mission assignment on spawn

Route player UI spawns through `PlayerGeneral.AssignMissionForNewSquad(...)` after `IntegratedPrototypeSystems.SpawnWarTeam(...)`. Existing `WarOrder` still seeds behavior. Add mission scoring and debug reasons. This gate should visibly label squads with missions but should not require full member task execution.

### Gate 3 — Debug overlay and telemetry

Give Bob a selected-squad command panel: mission, mission reason, leader task state, current order, contact state, support request, retask cooldown, and recent command events. Also add a debug-only enemy director panel after Enemy General exists.

### Gate 4 — Squad mission controller

Add `SquadMissionController` as the bridge between assigned mission and existing `TeamDecisionKind`. It should influence the existing decision selection, not replace it all at once. Example: a `BuildConnectTrench` mission biases decisions toward `ConnectTrenches`, `DigIn`, `ImprovePosition`, or `Stall` with explainable reasons.

### Gate 5 — Reservation/claim registry

Prevent chaos by adding deterministic claim tokens for hardpoints, trench sockets, support requests, and build tasks. Start with hardpoint build and occupancy claims only. Keep TTLs short and visible in debug.

### Gate 6 — Enemy General replacement

Replace the delayed enemy-response prototype with `EnemyGeneral` virtual budget, spawn cadence, lane scoring, mission assignment, and difficulty profiles. Keep “response to player pressure” behavior, but make it budgeted, capped, explainable, and testable.

### Gate 7 — Member task shadow mode, then active mode

Add member task records and per-role action catalogs. At first, record intended tasks for debug only. Then allow a small subset of tasks to affect posture/movement/working state for scouts, riflemen, sappers, medics, and porters.

### Gate 8 — Expand team templates and hardpoint families slowly

Use the 50 planned templates as a shelf, not immediate scope. Add MG, aid, mortar, command/signals, and special support teams only after the mission/task stack is stable for the existing four live templates.

## Non-goals

- No production C# implementation.
- No art generation.
- No ML/LLM runtime behavior inside the game.
- No cloud services.
- No real-world tactical instruction.
- No attempt to activate all 50 planned squad templates at once.
