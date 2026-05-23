# 2026-05-22 - TWB Trenchworks Soldier Mission Tasking Audit

## Scope

- Project: TWB Trenchworks standalone Unity project.
- Project path: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`
- Scope category: The World Beneath / TWB Trenchworks World Key lane.
- Request: Audit whether soldiers have proper mission sets, can fight each other, engage when they see enemies, receive squad-member tasks, and have fallbacks when assigned missions become impossible.

## Worker Setup

- Read project memory entry points:
  - `memory/hot.md`
  - `memory/index.md`
  - `memory/wiki/game-dev/project-hierarchy.md`
- Updated current task brief:
  - `memory/briefs/current-game-dev-task.md`
- Used lightweight `twb-audit` triad.
- Set a 2-minute heartbeat while child audit agents worked.
- Spawned three bounded child audit agents:
  - Helpful Genius lens: integration strengths and least-disruptive next fix.
  - Devil's Advocate lens: failure modes and haphazard-charge risks.
  - Doe-Eyed Intern lens: unclear definitions and missing checklists.
- Closed all child agents and deleted the heartbeat after review.

## Short Answer

The current prototype soldiers can fight each other and will respond to visible/heard contact through the core `WarTeamSlice` tactical layer. They do not simply ignore enemies: contact detection, rifle exchange, melee exchange, suppression, socket shifting, withdrawal, digging in, and support requests all exist.

However, the full "every unit has a mission, every squad member knows its role, every mission has a fallback" system is not complete. The current four spawnable prototype team types have partial mission assignment and shadow member tasks. Future team types such as machine gun, mortar, aid, and command have catalog entries and role/task vocabulary, but they are not yet fully wired through assignment, decision hints, squad-leader tasks, mission-specific fallback, and smoke coverage.

## Fix Applied During Audit

The audit found one critical behaviour mismatch: an ammo-empty team in open ground could choose `Attack` through the close-assault fallback before combat-effectiveness safety checks ran.

Changed:

- `Assets\Scripts\Simulation\War\WarTeamSlice.cs`
  - `TryCreateOpenGroundMeleeDecision` now refuses close assault when the team has fewer than two living members or is not combat-effective.
  - This preserves desperate melee for an intact, cohesive team, while stopping broken/lone squads from haphazard charging.

- `Assets\Scripts\Simulation\War\WarFrontCombatStallSmoke.cs`
  - Added `BrokenSquadAvoidedMelee` coverage to the open-ground melee fallback smoke.
  - Added a deterministic broken-squad scenario: one surviving ammo-empty assault member in open ground sees an enemy and must not receive a melee attack decision.
  - Adjusted the smoke pass condition to use the stronger proof of melee damage plus the broken-squad guard. The old final-distance assertion was brittle because teams can inflict melee damage and then later separate while recovering/withdrawing.

## Findings

### Confirmed Working

- The command layer is attached to runtime integration:
  - `WarIntegrationFacade` owns `WarCommandDirector`.
  - `WarTeamSlice.MissionDecisionProvider` receives mission hints.
  - Command state appears in snapshots.
- Current player squad spawn flow assigns missions for:
  - Scout
  - Assault
  - FortifyEngineer
  - Supply
- Current combat engagement exists at team level:
  - Teams detect visible/heard enemy contact.
  - Rifle and melee exchanges can apply damage.
  - Contact decisions can hold fire lanes, suppress, shift sockets, dig in, withdraw, request support, or mark unresolved sectors.
- Mission bias is conservative:
  - Mission hints do not override obvious safety/contact/regroup/support decisions.

### Gaps

- Enemy squads currently receive `NoActiveMission` in the command layer.
  - They still fight through core team tactics.
  - They do not yet have a true enemy-general mission assignment path.

- Future unit types are not fully actionable yet.
  - Catalog entries exist for machine gun, mortar, aid, and command missions.
  - `PlayerGeneral` falls back to `ReserveHold` for unsupported kinds.
  - Prototype spawn templates currently cover only scout, assault, engineer, and supply.

- Several catalogued missions lack decision-hint coverage:
  - `OccupyRifleBay`
  - `ClaimBuildMgPoint`
  - `MortarSupport`
  - `CasualtyResponse`
  - `CommandRelay`

- Squad-member tasks are still mostly a shadow/posture layer.
  - `SquadLeaderBrain` assigns tasks.
  - `MemberTaskController.ApplySafeTaskEffect` mainly changes posture.
  - Not every member task directly advances mission outcomes yet.

- Fallbacks exist, but they are broad rather than mission-specific.
  - Combat ineffective or stalled teams can retask to `RegroupWithdraw`.
  - Contact logic handles low ammo, unsafe contact, and supply withdrawal.
  - Missing: explicit "mission impossible" fallbacks such as no valid supply target, unsafe MG point, build target gone, no construction stock, or unreachable objective.

## Checks Run

- `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln --nologo`
  - Result: exited successfully, but warning reported no project to restore. This is not a meaningful Unity gameplay compile check.

- Temporary pure-simulation smoke harness under `Temp\SoldierMissionAuditHarness`
  - Included simulation and data source files.
  - Ran:
    - `WarOpenGroundMeleeFallbackSmoke.RunPrototypeSmoke()`
    - `WarSquadMissionControllerSmoke.RunPrototypeSmoke()`
    - `SquadLeaderBrainSmoke.RunPrototypeSmoke()`
    - `WarMissionRetaskSmoke.RunPrototypeSmoke()`
  - Result: passed.
  - Key output:
    - `open ground melee fallback smoke melee=True, distance=10/49, health=400/349|400/349, brokenAvoidedMelee=True`
    - `squad mission controller smoke passed=True`
    - `squad leader brain smoke passed=True`
    - `mission retask smoke passed=True`

## Cleanup

- Removed temporary harness:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\SoldierMissionAuditHarness`
- Deleted the audit heartbeat.
- Closed child audit agents.

## Files Touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarFrontCombatStallSmoke.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-twb-trenchworks-soldier-mission-tasking-audit-report.md`

Temporary files created and removed:

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\SoldierMissionAuditHarness`

## Risks

- Unity Play Mode was not run in this worker pass.
- The enemy-general command layer remains incomplete.
- Machine gun, rifle bay, mortar, aid, and command mission families are not ready to be called complete.
- Existing task names and reaction policy vocabulary can mislead future workers into assuming behaviour exists where only telemetry/posture exists.

## Memory-Worthy Notes

- Current Trenchworks soldier combat is team-level first and mission-biased second.
- Present prototype teams can fight, but "soldier mission system complete" would be an overclaim.
- The next implementation gate should be mission coverage, not more art/UI.

## Recommended Next Gate

Create a mission coverage hardening pass:

1. Add a diagnostic smoke that enumerates every `WarSquadMissionType` and records whether it has:
   - catalog entry
   - player/enemy assignment route
   - decision hint
   - squad-leader task mapping
   - role permission
   - smoke coverage
   - explicit future-placeholder status
2. Wire the next real mission family first:
   - Recommended first slice: `ClaimBuildMgPoint`
   - Then `OccupyRifleBay`
   - Then `CasualtyResponse`, `MortarSupport`, and `CommandRelay`
3. Add enemy-general mission assignment instead of `NoActiveMission`.
4. Add mission-specific impossible-target fallbacks.
5. Add scenario smokes proving visible enemy contact leads to tactical decisions and actual damage/support/withdraw outcomes.
