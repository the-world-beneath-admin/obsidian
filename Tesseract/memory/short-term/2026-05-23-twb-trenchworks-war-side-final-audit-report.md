# TWB Trenchworks War-Side Final Audit Report

Date: 2026-05-23
Scope: Standalone TWB Trenchworks war side
Decision: whether Bob can begin controlled war-side Play Mode testing, excluding the unfinished supply-line gameplay.

## Verdict

The war side is ready for controlled prototype testing, with caveats.

It is not release-ready, and it should not be sold to ourselves as fully certified. The important war loops are in place: players can spawn squads through the command/general path, the enemy general can spawn planned responses, squads receive missions and member task hints, front-line establishment runs, combat contact resolves with ammunition/damage/suppression/withdrawal logic, and rifle/MG/support emplacements have smoke coverage.

The remaining risk is not "nothing works"; the risk is that several deeper certification and polish gates are still future-facing: supply-line gameplay, packaged-build proof, broader visual combat proof over long sessions, and a few stale/deferred front-establishment guarantees.

## Evidence

- Command-plan smoke passed before this final audit pass:
  - 50 template profiles present.
  - 50 runnable profiles.
  - all planned spawns passed.
  - planned decision hints covered 211 of 211 required non-placeholder paths.
  - member-task active subset passed.
  - man-emplacement mode passed.
  - support-emplacement brain passed for mortar, aid, command, and supply.
  - enemy budget/difficulty smoke passed and uses planned roster responses.
  - runtime art StreamingAssets mirror passed with 12,578 files.

- Simulation smoke passed before this final audit pass:
  - integrated prototype smoke passed.
  - phase-one front establishment umbrella passed.
  - front blueprint, fairness, variety, claim allocation, movement/build, visibility passed.
  - combat stall smoke passed with contact, ammo spent, damage applied, and teams staying in the fight.
  - contact-action, socket occupation, melee fallback, idle guard, range/spotting/posture, and support recovery smokes passed.

- Visible Play Mode proof was captured:
  - `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\trenchworks-war-visible-proof-20260523\war-visible-proof-f8-f9-window.png`
  - `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\trenchworks-war-visible-proof-20260523\war-visible-proof-front-running-window.png`
  - `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\trenchworks-war-visible-proof-20260523\war-visible-proof-accelerated-front-window.png`

- The visible proof shows:
  - general portrait/dispatch panel active.
  - minimap active.
  - F9 debug overlay active.
  - front blueprint/trench lines/hardpoint pads visible.
  - 4 player teams and 4 enemy teams in the accelerated front proof.
  - assigned Fortify and Assault missions visible in the side summary.

## Fix Applied During Audit

The telemetry recorder was reading old macro `WarWorld.Units` counters while the live war UI used the integrated team/front snapshot. That produced false summaries such as 0 player alive, 0 enemy alive, 0 trenches, and `FORCE_COLLAPSE` while the screen clearly showed active 4v4 integrated teams.

Patched:

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
  - added integrated telemetry metrics.
  - telemetry now prefers `WarBattlefieldSnapshot` / integrated `WarSubsystemSnapshot` when live team-member facts exist.
  - summary now reports its metric source.
  - counts integrated living members, dead members, command leaders, fighting/digging/holding/scouting/retreating teams, low ammo teams, contacts, casualties, blueprint progress proxies, and active/static integrated teams.

Verification after patch:

- `dotnet build TWB-TrenchWorks.sln --no-restore` passed.
- Unity script compilation accepted the patch in batch/editor startup.

Verification caveat:

- A fresh Unity `-executeMethod` command smoke launch compiled scripts but did not reach the execute method before it had to be stopped. The older command and simulation smoke results remain valid for the system state immediately before the telemetry patch; the telemetry patch itself was compile-verified, but the post-patch smoke method did not complete.

## Readiness By Area

Assets:

- War runtime art mirror is present and smoke-covered.
- Solid art packs are wired far enough for testing: trenches, base tilemap, MG/rifle emplacements, mortar pit, aid post, command/supply support assets, VFX/UI/support solid batches.
- Visual art acceptance is not the same as asset-production completion. Decoration assets and final polish remain separate future passes.

Troops and tasking:

- 50 planned template profiles are runtime-spawnable through the command compatibility path.
- Mission families have coverage for the current planned non-placeholder profiles.
- Squad leaders have active subset task coverage for observation, work, supply, rifle bay, medical, combat, and support loops.
- Placeholder/future profiles still exist and are deliberately locked or skipped where not ready.

Combat:

- Squads can detect/contact/fight.
- Combat smokes prove ammo spending, health changes, suppression, fallback from unsafe melee, socket occupation, support requests, and recovery.
- This supports controlled testing where Bob spawns troops and watches the front fight.

Emplacements:

- Rifle bay and MG man-emplacement mode have smoke proof.
- MG facing/arc proof is present in smoke: forward morale affected, rear morale not affected.
- Support emplacements are no longer purely skeletal: mortar, aid, command, and supply support brains have active-state/fallback smoke proof.

Generals:

- Player general assigns spawned teams into command missions.
- Enemy general has budget/difficulty response logic and can spawn planned-roster responses.
- Enemy is adequate for prototype opposition, not yet a finished RTS AI personality.

UI:

- War mode overlay UI, dispatch panel, minimap, tracker toggle work visually in Play Mode.
- Visible proof confirms modern overlay direction is in place.

## High-Severity Risks

1. Supply-line gameplay is still excluded from readiness.
   - Action: test war-side combat without treating supply production/logistics as finished.

2. Fresh post-telemetry Unity command smoke did not complete.
   - Action: rerun command smoke from a clean editor state before declaring the telemetry patch fully smoke-certified.

3. Visible accelerated front proof did not visibly reach live contact during the screenshot window.
   - Action: run a longer Play Mode observation or a forced-contact visual scenario to prove the player-facing view shows fighting, not only the simulation harness.

4. Some deeper certification rules remain deferred/stale around strict front-establishment seed guarantees.
   - Action: split stale tests from real missing guarantees, especially seed 6107 topology/depth/socket/hardpoint expectations.

5. Packaged Windows build proof has not been run.
   - Action: before calling the war side externally testable, create and launch a Windows build or a controlled editor test checklist.

## Final Call

Bob can start war-side prototype testing in the editor now, with the explicit understanding that this is a controlled testing gate, not release readiness. The system is coherent enough to spawn troops and watch the war layer behave, other than the known supply-line exclusion.

The next practical gate is a visible forced-contact Play Mode test: spawn opposing squads close enough to create contact, confirm bullets/ammo/health/deaths/emplacements are visible to the player, and then rerun the command smoke from a clean Unity state.
