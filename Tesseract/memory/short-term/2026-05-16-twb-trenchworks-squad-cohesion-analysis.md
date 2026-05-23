# 2026-05-16 TWB Trenchworks Squad Cohesion Analysis

Scope: Standalone TWB-tagged game / TWB Trenchworks prototype at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

Worker constraints: code analysis only. No source edits. No wiki/index/hot/log edits.

## Concise Findings

- `TrenchworksSimulation.WarWorld` currently models visible war actors as independent `WarUnit` instances. `WarUnit` has no squad id, leader id, or commander relationship; it only stores faction, type, position, entry lane, patrol offsets, health, morale, ammo, and state.
- Wave drill spawn groups already imply squads: `SpawnWaveDrillGroup` spawns 4 units per lane and makes `index == 0` a `Command` unit. However, after spawning, those four units are not linked, so every unit independently runs `TickUnit`, `MoveScoutWithDrillPace`, and `MoveScout`.
- Current jerky movement is mostly cadence and teleporting-by-cell: `TrenchworksSimulation.FixedStepSeconds` is 0.1s, but war agent logic only runs when `TickIndex % 10 == 0`, so visible war units make strategic jumps once per second. In wave drill, `MoveScoutWithDrillPace` applies 4 `MoveScout` steps in that same strategic second, making the jump look abrupt.
- `TickWarAgents` iterates all units independently in random offset order each strategic second. That gives variety, but it also means subordinate units can move before/after nearby commanders without a squad-level plan.
- `MoveScout` and `ScoreScoutCell` already bias forward movement, lane waviness, unscouted cells, cover, trenches, and crowding. It is not pure random, but because the stable wander score is large and each unit has its own patrol offset/noise, squads visually scatter.
- `MoveTowardCoverOrStandoff` and `ScoreStandoffCell` already contain the right future hook for cover/standoff behavior during contact.
- A newer integrated war subsystem already has better squad primitives: `WarTeam`, `WarSubUnit`, `WarTeamTemplate.CohesionRadius`, `WarTeam.Leader`, `WarTeam.Anchor`, `WarTeamSlice.MoveTeamToward`, contact states, cover map, trench plans, and team smoke scenarios. However, its `MoveTeamToward` currently teleports subordinates directly into formation around the leader each tick and does not enforce a 15-square pin or commander-death chaos rule.
- The UI currently draws both older `WarWorld.Units` and integrated `WarSnapshot.Teams`, so a future implementation should decide whether squad cohesion is added to the older visible layer or the newer team subsystem becomes the primary visual layer. The small safe path is to patch the older visible layer first, because that is the user-visible wave drill behavior.

## Recommended Small Implementation Plan

1. Add squad identity to the visible `WarUnit` layer.
   - Change type: `WarUnit`.
   - Add: `SquadId`, `LeaderId`, `FormationIndex`, and `IsSquadLeader` or derive leader from `Type == WarUnitType.Command`.
   - Set these in `SpawnWaveDrillGroup` and, if desired, in `SpawnFactionUnits` by grouping initial units in batches of 4.
   - Keep default values permissive for existing scenarios.

2. Add lightweight squad lookup helpers in `WarWorld`.
   - Change type: `WarWorld`.
   - Add helpers such as `FindSquadLeader(WarUnit unit)`, `GetSquadMembers(int squadId)`, `IsLeaderAlive(WarUnit unit)`, and `DistanceToLeader(WarUnit unit)`.
   - Keep implementation local to `TrenchworksSimulation.cs` unless the team subsystem is promoted as the primary runtime later.

3. Replace fully independent scouting with leader-directed scouting.
   - Change methods: `TickUnit`, `MoveScoutWithDrillPace`, `MoveScout`, `ScoreScoutCell`.
   - If unit is a living squad leader: use current scout scoring, but tune it toward forward, non-straight movement.
   - If unit is a subordinate and not in contact: target a formation cell around its leader, not its own independent `DesiredScoutY`.
   - If subordinate is outside 15 Manhattan cells of the living commander, heavily prefer movement back toward the commander and suppress outward wandering.

4. Allow controlled break-apart during contact.
   - Change methods: `TickUnit`, `MoveTowardCoverOrStandoff`, `ScoreStandoffCell`.
   - When `FindEnemyInRange` or `HasRecentContactNear` is true, allow members to choose cover/standoff cells independently, but keep a soft squad pull if they exceed 15 cells from the leader.
   - If the squad leader dies, relax the pull and increase noise/lateral movement, with reason text such as "leader down; acting on local contact".

5. Smooth movement cadence without rewriting rendering.
   - Change method: `MoveScoutWithDrillPace`.
   - Reduce wave drill `moveCount` from 4 to 1 or 2. If faster front advance is needed, increase spawn/pulse tempo rather than moving one actor four cells in one strategic second.
   - Optional prototype-safe alternative: run `War.TickStrategicSecond` more often than once per second only for visual movement, but that risks changing economy/combat balance. Prefer tuning `moveCount` first.

6. Later, when cover/obstacles mature, promote cover preference into squad target selection.
   - Change methods: `ScoreScoutCell`, `ScoreStandoffCell`, or newer `WarTeamSlice.SampleInfluence`.
   - Raise cover/trench score and reduce straight-forward/no-cover advance, but avoid making units halt forever behind the first cover tile.

## Risks

- The old visible `WarWorld` and newer `WarTeamSlice` duplicate war concepts. Implementing cohesion in both would create drift. Choose one owner for visible behavior.
- Hard 15-cell pinning can look artificial if it teleports or overrules combat too aggressively. Use a strong score bias first; only hard-block extreme outliers.
- Current occupancy uses `unit.Id` as an index into `units`. This works because ids currently match list indices and units are not removed, but any future squad container/removal refactor must not break this assumption.
- Reducing wave-drill movement from 4 to 1 may make the front feel slow unless pulse intervals or map scale are tuned.

## Suggested Smoke Test

- Extend `TrenchworksProjectSetup.RunSimulationSmokeTest` after the existing wave drill assertions.
- Create `TrenchworksSimulation.CreateWarWaveDrillScenario()`.
- Tick at least 20 strategic seconds.
- For each living non-command unit with a living leader in the same squad and not currently `Retreating`, assert Manhattan distance to leader is `<= 15`.
- Assert at least one squad has advanced forward, at least one unit enters `Fighting` or contact appears, and after contact no subordinate exceeds a looser emergency radius such as `<= 22`.
- Add one scenario where a command unit is killed or marked dead, then assert surviving squad members remain valid, move without exceptions, and show more local/chaotic behavior rather than freezing.

## Cleanup

No temporary files, source edits, screenshots, or logs were created by this worker. This report is the only file written.
