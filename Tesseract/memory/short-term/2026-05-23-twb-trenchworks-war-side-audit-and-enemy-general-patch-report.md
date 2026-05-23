# TWB Trenchworks War-Side Audit And Enemy-General Patch Report

Date: 2026-05-23

Scope: standalone TWB Trenchworks war side. Not main TWB Unity, not Glassroot Garden, not Alchemy, not shared platform. Permanent Obsidian memory was not edited.

## Verdict

The war side is now strong enough for controlled war-side runtime observation in the editor: units can spawn, receive missions/tasks, detect/contact enemies, fight, consume ammo, take damage/stress, use rifle/MG/support emplacement loops, recover/withdraw under unsafe conditions, and trigger enemy-general responses.

It is not yet a final play-ready certification. The remaining hard gaps are:

- 14 mission families are still explicitly placeholder-locked.
- Several partial mission families still have generic tasking rather than bespoke behaviour.
- Several generated solid asset packs are still candidate-only and not runtime-referenced.
- Runtime generated-art loading is editor-friendly but not packaged-build-safe yet.
- No new live F9/screenshot visual proof was run in this pass.

## What Changed

Patched `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`:

- Replaced the old enemy-response selector that mostly returned `assault_section`/`scout_patrol`.
- Added planned-catalog response scoring so the enemy general can pick from planned templates by difficulty tier, enemy/player team pressure, team kind, and profile status.
- Added planned/prototype alias equivalence for the enemy-general shadow comparison so legacy `assault_section` and planned `planned_assault_section` compare as the same response family.

Patched `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\EnemyGeneralBudgetDifficultySmoke.cs`:

- Added `PlannedRosterResponses`.
- Added smoke checks proving enemy responses can select planned roster IDs instead of only old prototype IDs.

Patched `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`:

- Added the enemy budget/difficulty/planned-roster smoke to `RunCommandPlanSmokeTest`, so future command-plan smokes catch regressions.

## Audit Findings

Mission/tasking:

- All 50 planned squad templates now have runtime profiles and spawn coverage.
- Squad leaders assign member tasks for scout, trench/build, supply, assault, hold, MG, casualty, mortar, and command relay families.
- Member task effects exist for combat fire/suppression, MG operation, medical treatment/carry, mortar operation, spotting, and command relay.
- Remaining issue: 14 mission families remain placeholders, and several partial families still need richer `SquadMissionController` decision hints.

Assets:

- Runtime-referenced solid packs: `HardpointPads`, `HardpointStructures`, `FrontlineMGSockets`, `FrontlineLogistics`, `MGDugoutOrientation`, `RifleFightingPositions`.
- Candidate-only/not broadly runtime-referenced packs include `BattlefieldCover`, `FieldHazards`, `FieldObstacles`, `HeavyBattlefield`, `SectorInfrastructure`, `SupportEmplacements`, `SupportTrenchLines`, `TacticalRoleProps`, and `TrenchUtilities`.
- Runtime generated solid assets currently load through loose `Application.dataPath` files first. `Resources.Load` fallback exists, but generated solid assets are not mirrored under `Assets\Resources\Art\War\SolidAssets`, so packaged builds remain at risk.

Combat/emplacements:

- Existing smokes prove contact detection, firing, ammo drain, health damage, suppression/contact actions, unsafe open-ground melee avoidance, regroup/withdraw, support requests, rifle-bay manning bonus, MG forward-arc suppression, and support emplacement brain effects for mortar/aid/command/supply.
- Remaining issue: these are deterministic smoke proofs, not yet a fresh live F9 visual review.

## Checks Run

- `dotnet build TWB-TrenchWorks.sln --no-restore`
  - Passed: 0 warnings, 0 errors.

- Unity command-plan smoke:
  - Log: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Logs\codex-war-side-audit-command-smoke-2.log`
  - Passed with return code 0.
  - Key result: command plan passed, 50 template profiles, all planned spawns true, mission family task coverage true, man emplacement true, support emplacement true, enemy budget difficulty true, planned roster true.

- Unity simulation smoke:
  - Log: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Logs\codex-war-side-audit-simulation-smoke-2.log`
  - The shell wrapper timed out while waiting, but follow-up log inspection showed Unity completed batchmode successfully with return code 0.
  - Key result: `TWB Trenchworks smoke test passed`, combat stall true, contact actions true, open-ground melee fallback true, support recovery true, integrated smoke true.

## Cleanup

- Child explorer agents were closed after reporting.
- No raw GPT Pro package files were touched.
- No permanent Obsidian wiki/index/hot/log files were edited.
- No broad cleanup or source deletion was performed.

## Risks

- Playtesting in the editor is reasonable now, but packaged builds may miss generated art unless the asset loading path is hardened.
- The UI can expose planned units, but not every planned unit has bespoke behaviour yet; some depend on placeholder/partial mission family mappings.
- Candidate-only solid assets should not be treated as accepted gameplay objects until runtime render/pathing/collision/sorting proof exists.
- Support/emplacement art state mapping currently uses only a subset of generated states, mostly blueprint/active-style states.

## Recommended Next Gate

Run a live Play Mode/F9 war-side visual test with Bob spawning several planned unit families, including assault, scout, engineer, supply, MG, mortar, aid, and command. Capture screenshots/logs and verify:

- units enter through the UI and receive readable general dispatch text,
- the enemy general responds with planned roster units,
- both sides reach front positions and engage,
- rifle/MG/mortar/aid/command support effects are visible enough,
- generated solid art resolves in the editor,
- no severe stall or first-trench hiccup returns.

After that, do the packaged-build art loading fix before calling this play-ready outside the editor.
