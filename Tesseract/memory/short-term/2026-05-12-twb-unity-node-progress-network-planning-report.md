# TWB Unity Worker Report - 2026-05-12 - Node Progress Network Planning

## Task

Research and plan a main-game world-map progression system where defeating dungeons/events under a node raises that node's player-facing `Node Progress` percentage from 0% to 100%. At 100%, the node becomes secured and unlocks nearby nodes so the player builds an expanding network from their starter location.

## Result

Planning pass completed. No Unity source changes were made.

Recommended system shape:

- Store player-owned node progress on `PlayerWorldMapState`, not in UI-only snapshots.
- Treat territory node IDs as the canonical conquest node IDs, because world dungeons already use `WorldDungeonInstance.CountyId` mapped to territory node IDs.
- Award Node Progress when a world dungeon run report is claimed, after `WorldDungeonSpawnService.TryClaimRun` succeeds and before `MapRevision++`.
- Cap Node Progress at 100%. At 100%, mark the node as secured once and unlock deterministic neighbors from the existing territory connection graph.
- Start with dungeons only, then add world events as a second source once the dungeon flow is stable.
- Use route/lane connections for unlocks instead of raw geographic radius. This avoids unstable "nearby" behavior in the procedural overlay.

Suggested domain model:

- `PlayerWorldMapNodeProgressRecord`
  - `NodeId`
  - `ProgressPercent`
  - `State` (`Locked`, `Frontier`, `InProgress`, `Secured`)
  - `DiscoveredAtUtcSeconds`
  - `SecuredAtUtcSeconds`
  - optional small source ledger for idempotence, such as applied run IDs
- Add a `List<PlayerWorldMapNodeProgressRecord>` to `PlayerWorldMapState`.
- Keep state serializable and deterministic, following the existing public-field domain style.

Suggested service/API shape:

- Add a narrow world-map node progress service or `WorldMapService` helpers:
  - ensure starter node progress exists after starter home selection
  - resolve a dungeon's node ID from `WorldDungeonInstance.CountyId`
  - apply Node Progress from a claimed run
  - secure a node at 100%
  - unlock connected neighbor nodes
  - project progress/status into snapshots
- Gate dungeon starts only after the first domain pass is stable:
  - secured nodes remain runnable for reward farming
  - frontier/in-progress nodes are runnable for progression
  - locked nodes return a clear "node not in network" failure

Suggested tuning:

- Starter tutorial should take about 3-4 successful dungeon/event actions, not ten errands in a nice coat.
- First pass: successful dungeon claim adds 25-35% Node Progress based on tier/difficulty/boss.
- Failed claims should add 0% Node Progress initially. Add consolation progress later only if playtesting shows frustration.
- Repeat farming should not add repeated Node Progress from the same claimed run. Use the claim state plus a small applied-source guard if needed.

Suggested UI projection:

- Territory node snapshot: add Node Progress percent, node network state, and attackability.
- World dungeon snapshot: add Node Progress reward preview and locked/frontier state reason.
- Node dungeon list: show "Node Progress 42%" and whether the node is locked, frontier, in-progress, or secured.
- Dungeon inspect modal: show the Node Progress reward and 100% secure threshold.
- Map overlay: secured nodes should read as a connected network; frontier nodes should be visually distinct; locked neighbors should be visible but muted.

Suggested implementation milestones:

1. Add persistent node progress records and deterministic unit/system-console tests.
2. Seed the starter node when home/starter location is locked.
3. Award Node Progress on successful world dungeon claim and secure at 100%.
4. Unlock connected neighbors from the existing territory connection projection.
5. Gate world dungeon start by node network state with clear failure messages.
6. Add minimal UI readouts to the node list and inspect modal.
7. Add events as another Node Progress source after dungeon-only behavior is tested.
8. Add tutorial scripting once the mechanics are stable.

Open design questions for Bob/user:

- Should the player be allowed to run dungeons in secured nodes forever for rewards, with no further Node Progress gain? Recommended: yes.
- How many neighbors should unlock from one secured node: all direct route/lane connections, only route connections, or the top N strongest? Recommended first pass: all direct connections projected in the current territory graph, then tune.
- Should failed dungeon attempts ever add Node Progress? Recommended first pass: no.
- Should home relocation move the network root? Recommended first pass: no; starter network remains permanent.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-12-twb-unity-node-progress-network-planning-report.md`

## Checks run

Research-only pass; no Unity source changes and no build required.

Read/reviewed:

- `memory/hot.md`
- `memory/index.md`
- `memory/wiki/game-dev/project-hierarchy.md`
- `memory/wiki/game-dev/main-game-systems.md`
- `memory/wiki/twb-unity/overview.md`
- `memory/wiki/twb-unity/world-map-territory-overlay.md`
- `Assets/_TWB/Scripts/Domain/WorldMap/PlayerWorldMapState.cs`
- `Assets/_TWB/Scripts/Services/WorldMapService.cs`
- `Assets/_TWB/Scripts/Services/UIBoundary/UiWorldMapCommandHandler.cs`
- `Assets/_TWB/Scripts/Services/WorldMapDungeons/WorldDungeonSpawnService.cs`
- `Assets/_TWB/Scripts/Domain/UIBoundary/WorldMapUiSnapshot.cs`
- `Assets/_TWB/Scripts/Domain/WorldMapDungeons/WorldDungeonInstance.cs`
- `Assets/_TWB/Scripts/Domain/WorldMapDungeons/WorldDungeonRun.cs`

## Cleanup performed

No temporary files or generated artifacts were created.

## Risks

- Use `NodeProgress` / `ProgressPercent` internally and "Node Progress" externally. Do not introduce a second player-facing or domain-facing "influence" term for this system.
- Territory connections are currently projected from visible territory nodes. Implementation must ensure the same deterministic graph can be reconstructed for persisted/unlocked nodes, even when the camera/zoom changes.
- If progress is awarded at run start instead of claim, players can receive conquest progress before outcome/reward resolution. Recommended award point is claim.
- If repeat dungeon runs add Node Progress without source guarding, players can farm one dungeon to unlock the whole network. That may be desirable later, but it should be a conscious tuning decision.

## Memory-worthy notes

- World dungeons already map to territory nodes through `WorldDungeonInstance.CountyId`, and `WorldMapService.ApplyTerritoryDungeonSpawnContract` sets summary `CountyId` to the territory node ID.
- `PlayerWorldMapState` is the right persistent place for node network progress.
- `UiWorldMapCommandHandler.DispatchClaimWorldDungeon` is the clean first integration point for dungeon-sourced Node Progress.
- Use the territory connection graph for "nearby nodes" instead of raw radius.

## Do not promote to memory

- Exact Node Progress reward values are provisional.
- UI wording is now standardized as "Node Progress" with percent display.
- No implementation decision is final until Bob/user approves the next bounded implementation gate.

## Next recommended gate

Implement milestone 1 only: add the player node-progress data model plus deterministic helper methods/tests for seeding a starter node, adding Node Progress, capping at 100%, and securing/unlocking neighbors in a testable graph. Do not touch visual polish or tutorial scripting in the first implementation slice.
