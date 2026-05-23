# TWB Trenchworks War-Side Readiness Audit

Date: 2026-05-23

Scope: TWB Trenchworks standalone Unity prototype, war side only. This is not The World Beneath main game, Glassroot Garden, Alchemy, or shared account/platform work.

Mode: Full audit using `twb-audit`; child explorer subagents reviewed asset/runtime coverage and troop/mission/combat coverage. No permanent Obsidian wiki files were modified.

## Verdict

The war side is prototype-functional and ready for controlled systems testing, but it is not ready to call "play-ready" or feature-complete.

The strongest live slice is: four runnable squad profiles, front-line establishment, contact, rifle/melee combat, ammo/health/stress, basic support requests, general dispatch text, and manned rifle/MG plus skeletal support emplacement brains.

The main blockers to a true play-ready verdict are:

- Only four squad profiles are normal runtime spawns: `scout_patrol`, `assault_section`, `fortify_engineers`, and `supply_team`.
- The larger 50-template / 33-mission-family command plan is mostly cataloged, not all runnable.
- Many new art packs exist as candidate assets but are not all runtime-accepted through Unity/F9 or packaged-build-safe loading.
- The latest manual Unity simulation-smoke rerun attempted during this audit hung before executing the smoke method; earlier same-day logs still show a passing simulation smoke.
- The front-establishment diagnostic sweep still has 2/21 seed failures on deeper indicators (`6109` front-line MG sockets, `6116` hardpoint pad density).
- Play Mode visual proof was not performed in this audit.

## Evidence Summary

### Asset Coverage

Observed asset roots:

- `Assets/Resources/Art/War/Units/ProceduralV2Full`: 2,805 PNGs.
- `Assets/Resources/Art/War/Emplacements/ProceduralV1`: 20 PNGs.
- `Assets/Resources/Art/War/TrenchTilesets/Blueprints`: 219 PNGs and 25 JSON files.
- `Assets/Art/War/SolidAssets`: 5,366 PNGs, 15 JSON manifests, 15 README files.
- `Assets/Art/War/VFX`: 786 PNGs.
- `Assets/Art/War/UI`: 4,721 PNGs.
- `Assets/Art/Terrain/Transitions`: 2,736 PNGs.

Runtime-wired categories are real but narrower than the full art inventory. `PrototypeBootstrap` references the ProceduralV2Full unit path, base tilemap path, ProceduralV1 emplacements, generated hardpoint pads/structures, frontline MG sockets, logistics, MG dugout orientation, and rifle fighting positions. The 33 war member role mapping is explicit in `Assets/Scripts/Unity/PrototypeBootstrap.cs`.

Candidate-only or insufficiently proven categories include BattlefieldCover, FieldHazards, FieldObstacles, HeavyBattlefield, SectorInfrastructure, SupportEmplacements art pack, SupportTrenchLines, TacticalRoleProps, TrenchUtilities, WarHUDChrome, CommandAndMapMarkers, PersistentMorale, CombatFeedback, and BattlefieldDecals. They may exist as art, but most are not yet proved as live runtime systems.

Obstacle/tank-trap-like exposure: no literal `tank trap` / `tank-trap` script reference was found, but wire/obstacle concepts are still exposed through research/catalog/planning surfaces. This is probably acceptable as future design data, but it should not surface as a normal buildable/player-facing option until obstacle rules are deliberately enabled.

### Troops, Missions, And Combat

The current live squads:

- `scout_patrol`
- `assault_section`
- `fortify_engineers`
- `supply_team`

The planned squad catalog is much larger, but the command compatibility smoke reports `templateProfiles=50`, `runnableProfiles=4`, and `placeholders=14`. That means the plan is broad; the playable implementation is still intentionally narrow.

Combat loops are real:

- Contact detection and heat/visibility logic exist.
- Rifle fire consumes ammo and applies damage.
- Melee exists when contact closes, with recent safety checks preventing broken squads from haphazard charges.
- Squads regroup/withdraw under leader loss, low ammo, open-ground danger, and support pressure.

Mission loops are partial:

- Live mission hints cover scouting, marking, assault, holding, digging/building, supply, regroup, and reserve.
- Broader mission families such as occupy rifle bay, claim/build MG point, mortar support, casualty response, command relay, signal operation, and advanced tier behavior are represented but not all normal player-runnable behavior.
- Member tasks are stronger than before but still partly shadow/telemetry-style for planned families rather than fully independent member execution for every unit type.

### Emplacements

Rifle and MG emplacements are the most convincing live systems:

- Rifle bay can be manned and grants a fire/hit chance bonus.
- MG point can be manned, checks forward arc, spends ammo, suppresses/damages forward targets, and tracks low ammo, crew loss, overrun, and abandoned states.

Support emplacements are wired as support brains:

- Mortar: active support brain, ammo consumption, target/observer-style need and fallback text.
- Aid: active support brain with casualty/medical need and fallback.
- Command: active support brain with command-net need and fallback.
- Supply: active support brain reports need and fallback, while actual supply delivery also exists as squad resupply behavior.

This is enough for controlled testing, but not yet enough to say every emplacement family has complete gameplay.

## Checks Run

- `dotnet build TWB-TrenchWorks.sln --no-restore`: passed, 0 warnings, 0 errors.
- Unity batch command plan smoke:
  - Log: `C:/Users/yrred/Desktop/Unity/TWB-Trenchworks/TWB-TrenchWorks/Logs/codex-war-readiness-audit-command-smoke.log`
  - Result: passed with return code 0.
  - Key evidence: `command plan compatibility passed=True`, `missionFamilies=33/True`, `templateProfiles=50/True`, `runnableProfiles=4`, `placeholders=14`, `member task active subset smoke passed=True`, `man emplacement mode smoke passed=True`, `support emplacement brain smoke passed=True`.
- Unity batch simulation smoke rerun:
  - Log: `C:/Users/yrred/Desktop/Unity/TWB-Trenchworks/TWB-TrenchWorks/Logs/codex-war-readiness-audit-simulation-smoke.log`
  - Result: blocked/hung before smoke output; process was stopped after no progress beyond startup/import.
- Same-day prior simulation evidence reviewed:
  - Log: `C:/Users/yrred/Desktop/Unity/TWB-Trenchworks/TWB-TrenchWorks/Logs/front-cert-simulation-smoke.log`
  - Result: passed with return code 0 and included front establishment, combat stall, contact action, melee fallback, support recovery, and integrated smoke evidence.
- Same-day front-establishment diagnostic reviewed:
  - `passed=19/21`
  - Failures: seed `6109` front-line MG sockets indicator, seed `6116` hardpoint pad density indicator.

## Findings

1. High: The war side should not be called fully play-ready because only four squad profiles are truly runtime-runnable. The rest of the 30-50 intended squad structures are catalog/planning coverage, not player-spawnable live behavior.

2. High: Art coverage is broad, but runtime acceptance is uneven. Core soldiers and key emplacements are wired; many solid/VFX/UI packs are candidate-only until Unity/F9 proves import, sorting, scale, pivots, packaging, and live behavior.

3. Medium: The general/mission system is functional as a prototype layer, but the full military hierarchy is not complete. Mission families and member tasks exist for broad design coverage, but many are placeholder/partial and not complete squad-leader-to-member execution loops.

4. Medium: Rifle/MG emplacements are in good testing shape, but mortar/aid/command/supply are still support-brain skeletons rather than finished gameplay loops.

5. Medium: The failed/hung simulation-smoke rerun during this audit prevents a clean fresh "all smokes pass right now" claim. The earlier same-day pass is encouraging but should be refreshed once the Unity batch hang is understood.

6. Medium: Deeper front-establishment certification is improved but not fully clean across the seed sweep. The current 19/21 result is good enough for prototype observation, not enough for a final certification gate.

7. Low: Wire/obstacle concepts remain present in catalog/research/planning data. Since tank traps specifically were not found by literal name, this is not the old tank-trap issue exactly, but obstacle exposure still needs a player-facing UI check.

## Dissent Preserved

Helpful Genius: There is enough here to start a controlled war-side test: spawn the four live squad types, observe front-line establishment, confirm contact, watch ammo/health/fallback behavior, and manually scenario-test MG/rifle/mortar/aid/command/supply emplacements.

Devil's Advocate: Calling it play-ready would be premature. The design promise was three tiers, 23 soldier roles, and 30-50 squad structures; the current runtime promise is four profiles plus broad future cataloging. Also, candidate art is not runtime art until Unity proves it in-scene.

Doe-Eyed Intern: The system is closer than it sounds. The important loops are not imaginary: things spawn, receive missions, detect enemies, shoot, spend ammo, take damage, regroup, dig, and man emplacements. The next test pass should be narrow and visible, not another giant invisible proof.

## Cleanup Performed

- Stopped the hung Unity batch simulation-smoke process started during this audit.
- Left audit logs in `Logs/` as evidence.
- No source files or permanent Obsidian wiki files were modified.

## Memory-Worthy Notes

- War side is currently "controlled test ready", not "play-ready."
- Current live runtime squads are four prototype aliases: scout, assault, fortify engineer, and supply.
- Soldier art coverage is broad and maps to 33 war member roles, but squad gameplay coverage is much narrower.
- Core soldier combat and fallback loops are real enough to observe in test.
- Rifle/MG man-emplacement mode is the strongest emplacement gameplay proof.
- Mortar/aid/command/supply support emplacements are present as skeletal support brains.
- Broad new art packs should remain candidate/runtime-unaccepted until Unity/F9 proves them.

## Recommended Next Gate

Run a visible Unity Play Mode/F9 war-side proof with a written checklist:

1. Spawn each of the four live squad types through the UI.
2. Confirm the general dispatch panel reports sector and assigned mission.
3. Observe player and enemy squads reaching the front, detecting each other, firing, spending ammo, taking damage, and avoiding dumb open-ground charges.
4. Man and observe rifle bay and MG point behavior.
5. Scenario-place or trigger mortar, aid, command, and supply support brains and confirm their effects are visible.
6. Confirm non-live obstacle/wire/tank-trap-like concepts are not player-facing buildables.
7. Record screenshots/video plus console/log output.

Only after that should the lane move from controlled systems testing to broader playtest readiness.
