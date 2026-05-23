# TWB Trenchworks War-Side Readiness Audit Report

Date: 2026-05-23
Worker: TWB Trenchworks standing worker
Scope: TWB Trenchworks war side, Unity project at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

## Verdict

The war side is ready for controlled war-side testing, not ready to be called fully play-ready yet.

The core runtime loops now pass smoke coverage for planned squad spawning, mission assignment, mission decision hints, member task subsets, combat contact, ammo spend, damage, regroup/withdraw fallback, rifle/MG manned emplacements, support emplacement brains, enemy general planned roster responses, and runtime war art mirroring.

The remaining reason not to call it fully play-ready is visual/human acceptance: a visible Unity Play Mode/F9 pass still needs to prove the whole war-mode surface is understandable and that the exposed 50 planned templates do not create a confusing or misleading player-facing roster.

## Audit Findings

- High: The old "only four runtime squads" concern is stale. Current command smoke proves 50 template profiles and all planned spawns are runnable. Evidence: `codex-war-mission-controller-command-smoke-3.log` reports `templateProfiles=50`, `runnableProfiles=50`, and `allPlannedSpawns=True`.
- High: Planned squads previously had catalogue missions without guaranteed live decision hints. I added stricter smoke coverage and patched the controller so partial support/emplacement mission families now produce concrete decision preferences.
- High: One semantic bug was found by the stricter smoke: `planned_ammunition_relay_team` was being resolved as `BuildHardpoint` because it references an MG point. I changed that path to `ResupplyHardpoint`, since an ammo relay should supply hardpoints, not build them.
- Medium: Support emplacements are functional at smoke level, but still need live UI/Play Mode proof. The smoke proves mortar, aid, command, and supply support brains activate and choose needs, but not that the player can read and enjoy the loop yet.
- Medium: Front establishment is functioning and the simulation smoke passes, but deeper advanced certification still has explicit deferred items such as full role-depth placement and support hardpoint depth. This should remain a known gate, not be buried under green smoke.
- Medium: Assets are present for runtime smoke. The command smoke verifies the `StreamingAssets` runtime mirror with 7 folders and 12,578 files, but a packaged Windows build proof has not been run in this pass.

## Code Changes

- `Assets\Scripts\Simulation\War\Command\SquadMissionController.cs`
  - Added decision hints for `ScreenFlank`, `OccupyRifleBay`, `ClaimBuildMgPoint`, `MortarSupport`, `CommandRelay`, and `CasualtyResponse`.
- `Assets\Scripts\Simulation\War\Command\CommandMissionCatalog.cs`
  - Broadened mission/team compatibility for shared/fallback missions such as rifle bay occupancy, MG point claiming, line holding, reserve hold, and regroup/withdraw.
- `Assets\Scripts\Simulation\War\Command\PlayerGeneral.cs`
  - Added scoring for screen, rifle bay, mortar support, command relay, casualty response, and emergency regroup mission choices.
- `Assets\Scripts\Simulation\War\Command\EnemyGeneral.cs`
  - Mirrored scoring coverage so enemy-assigned planned profiles can choose the same mission families sensibly.
- `Assets\Scripts\Simulation\War\Command\WarMissionFamilyTaskCoverageSmoke.cs`
  - Added `PlannedDecisionHintsCovered`, requiring every non-placeholder planned profile mission family to be allowed and produce a mission decision hint.
  - Added diagnostic detail in the summary so future failures name the missing mission path.
- `Assets\Scripts\Simulation\War\Command\WarCommandPlanCompatibilityCatalog.cs`
  - Changed supply templates tied to MG hardpoints to resolve as `ResupplyHardpoint` instead of `BuildHardpoint`.

## Verification

- `dotnet build TWB-TrenchWorks.sln --no-restore`
  - Passed with 0 warnings and 0 errors.
- Unity command plan smoke:
  - Log: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Logs\codex-war-mission-controller-command-smoke-3.log`
  - Passed with return code 0.
  - Key proof: `plannedDecisionHints=True`, `planned profile decision hints covered=211 required=211 skippedPlaceholders=30`, `allPlannedSpawns=True`, `plannedRoster=True`, `war runtime StreamingAssets mirror passed=True, folders=7, files=12578`.
- Unity simulation smoke:
  - Log: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Logs\codex-war-side-readiness-simulation-smoke.log`
  - Passed with return code 0.
  - Key proof: combat contact true, ammo spent, health changed, fighting true, support recovery true, melee safety fallback true, open-ground idle guard true, front establishment umbrella true, integrated smoke true.

## Child Audit Summary

Helpful Genius verdict: the systems are strong enough for controlled runtime testing, but not final play-readiness without visible Play Mode/F9 proof.

Devil's Advocate verdict: the biggest risk is accidentally treating all 50 planned templates as production-ready just because they spawn and have mission coverage. The UI/roster boundary must be visually tested before claiming player readiness.

The Doe-Eyed Intern role could not be spawned because the thread agent limit was reached. I covered the simple-question lane directly in this report.

## Cleanup

- No scratch scripts were created.
- Unity logs created during verification were left in the project `Logs` folder as evidence.
- No permanent Obsidian memory files were updated.
- No git staging, commit, reset, or broad cleanup was performed.

## Remaining Risks

- 14 mission families remain explicitly placeholder/future in the command plan compatibility catalogue.
- 30 placeholder profile mission paths were skipped by the new decision-hint smoke by design.
- Advanced front-establishment certification still has deferred deeper guarantees, even though the main simulation smoke passes.
- Runtime asset mirror is proven in editor command smoke, not in a packaged Windows build.
- Visible Play Mode/F9 acceptance has not been completed in this pass.

## Recommended Next Gate

Run a visible Unity Play Mode/F9 war-side test with the current 50-template UI exposed:

1. Spawn a mixed player roster from several tiers.
2. Confirm the general dispatch text assigns readable missions.
3. Let enemy general responses spawn and fight.
4. Confirm squads see enemies, fire, spend ammo, take damage, suppress, regroup, and withdraw.
5. Confirm rifle bays, MG nests, mortar pit, aid post, command dugout, and supply niche are visually understandable.
6. Capture screenshots and log proof before declaring the war side play-ready.

