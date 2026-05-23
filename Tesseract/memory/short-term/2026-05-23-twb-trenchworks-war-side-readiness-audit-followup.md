# TWB Trenchworks War-Side Readiness Audit Follow-Up

Date: 2026-05-23 12:06 -05:00
Scope: Standalone TWB-tagged game, TWB Trenchworks only.

## Decision

The war side is ready for controlled in-editor systems testing: Bob can spawn squads and watch the front establish, squads receive missions, contacts engage, ammo and damage move, emplacements run their first-pass brains, and the enemy general can respond with planned roster picks.

It is not fully play-ready certification yet. Two front-blueprint seed sweep failures remain, and several newer art/VFX/UI packs still need broader live F9/Play visual acceptance before being treated as final runtime presentation.

## Evidence Checked

- Command-plan batch autorun smoke passed.
  - Log: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Logs\codex-war-command-smoke-autorun-current-audit.log`
  - Key proof: `templateProfiles=50`, `runnableProfiles=50`, `allPlannedSpawns=True`, `allPlannedMissions=True`, `planned profile decision hints covered=211 required=211 skippedPlaceholders=30`, man-emplacement mode passed, support-emplacement brain passed, enemy budget difficulty uses planned roster, runtime StreamingAssets mirror passed with `folders=7, files=12578`.

- Full simulation batch autorun smoke passed.
  - Log: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Logs\codex-war-simulation-smoke-autorun-current-audit.log`
  - Key proof: front drill produced `6` pulses, `36` teams, trench plans, close contact/combat stall proof, ammo spending/damage, contact action reasons, no haphazard low-ammo melee, idle/regroup guard, support recovery, legacy duplicate visible war-unit rendering disabled, integrated smoke passed.

- Front establishment certification diagnostic passed the prototype seed and seed `6107`, but the broader seed sweep remains `19/21`.
  - Log: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Logs\codex-war-front-certification-current-audit.log`
  - Remaining failures:
    - Seed `6109`: `frontLineMgSockets=False`.
    - Seed `6116`: `hardpointPadDensity=False`.

- Asset presence checked.
  - War runtime StreamingAssets mirror passed in smoke.
  - Source folders exist for soldier cutouts, emplacements, multi-tile, solid assets, trench extras, UI, and VFX.
  - Important counts from source folders:
    - Support Emplacements V1: `20` PNGs.
    - Hardpoint Pads V1: `90` PNGs.
    - Hardpoint Structures V1: `72` PNGs.
    - Rifle Fighting Positions V1: `336` PNGs.
    - Frontline MG Sockets V1: `420` PNGs.
    - MG Dugout Orientation V1: `288` PNGs.
    - Support Trench Lines V1: `3840` PNGs.
    - Combat Feedback V1: `70` PNGs.
    - Battlefield Decals V1: `162` PNGs.
    - War HUD Chrome V1: `440` PNGs.
  - General and factory coordinator portraits exist in both `Assets/Art/War/UI` and `Assets/StreamingAssets/Art/War/UI`.

## Changes Made During Audit

- Added simulation and front-certification paths to the batch autorun harness:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksBatchSmokeAutorun.cs`
- The existing `-executeMethod` route failed to locate `TrenchworksProjectSetup.RunSimulationSmokeTest` despite clean script compilation. The autorun harness now uses environment variables:
  - `TWB_TRENCHWORKS_AUTORUN_COMMAND_PLAN_SMOKE=1`
  - `TWB_TRENCHWORKS_AUTORUN_SIMULATION_SMOKE=1`
  - `TWB_TRENCHWORKS_AUTORUN_FRONT_CERTIFICATION=1`

## Simulated TWB Audit Triad

Helpful Genius:

- Strong signal: the command and simulation smokes now prove a playable controlled loop, not merely a design document. The 50 planned templates spawn and carry mission snapshots; the old "four runtime squads only" statement is now stale for command spawning.
- Best next improvement: fix seed `6109` and `6116` before calling the front-generation contract stable.

Devil's Advocate:

- High risk: the front certification method currently exits success while the seed sweep is only `19/21`. That is acceptable for diagnostic reporting, but not acceptable as a release gate unless the sweep result becomes a hard assertion or a clearly named warning-only diagnostic.
- Medium risk: support emplacements pass first-pass brain smoke, but mortar, aid, command, and supply are still simple tactical effects compared with the final design ambition.
- Medium risk: newer VFX/UI/overlay packs have files and a runtime loading path, but not all have visual state-switching, sorting, scale, pooling, and packaged-player proof.

Doe-Eyed Intern:

- Simple question: if Bob presses unit buttons, can every visible unit be asked into battle? Current answer: yes through the planned command tree, but the deeper bespoke mission behaviours are still a mix of runnable, partial, and placeholder families.
- Simple question: will enemies fight back? Current answer: yes; the enemy general can spawn planned templates by pressure/difficulty and combat smokes show contact, firing, ammo, suppression, regrouping, and support recovery.
- Simple question: is it ready to "play"? Current answer: ready to observe and test war-side systems in Unity, not yet ready to call the war mode fully complete.

## Findings

- High: Front blueprint sweep is not fully closed. Seeds `6109` and `6116` still fail advanced generation rules. Action: harden front-line MG socket placement and hardpoint pad density, then make the sweep a hard certification gate or rename it as warning-only.
- Medium: Mission families are not all final bespoke behaviours. The smoke proves 33 families are catalogued and 211 required non-placeholder hints are covered, but 14 mission families remain placeholders and several live mappings are marked partial. Action: decide which partial/placeholder families must be completed before Bob's first real war-side playtest.
- Medium: Art is present and mirrored, but not all new solid/VFX/UI packs are visually accepted. Action: run a live F9/Play visual checklist for sorting, scale, anchors, state switching, minimap readability, and packaged-player loading.
- Low: The Unity command-line `-executeMethod` path is unreliable here. Action: keep the autorun harness as the supported batch smoke path.

## Next Gate

Fix the two remaining seed sweep failures first:

1. Seed `6109`: front-line MG socket coverage.
2. Seed `6116`: hardpoint pad density.

Then rerun:

1. `TWB_TRENCHWORKS_AUTORUN_FRONT_CERTIFICATION=1`
2. `TWB_TRENCHWORKS_AUTORUN_COMMAND_PLAN_SMOKE=1`
3. `TWB_TRENCHWORKS_AUTORUN_SIMULATION_SMOKE=1`

After that, do a live Unity Play/F9 visual pass with Bob spawning units through the interface.

