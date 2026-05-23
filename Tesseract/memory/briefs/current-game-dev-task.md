# Current Game Dev Task - TWB Trenchworks Controlled War-Side Proof

## Scope

Standalone TWB-tagged game: TWB Trenchworks only.

## Project

- Code directory: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`
- Active lane brief: `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- Report destination: `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term`

## Task

Run a visible controlled war-side proof for the live TWB Trenchworks prototype:

- Start from the active lane brief and latest short-term reports.
- Treat the war side as controlled-systems-test ready, not play-ready.
- Confirm the four legacy opening-drill profiles still work: Scout Patrol, Assault Section, Fortify Engineer Crew, and Supply Team.
- Confirm the broader 50 planned template roster remains runtime-spawnable through command/UI request paths before treating the unit tree as valid.
- Confirm the general dispatch panel reports sector and assigned mission.
- Observe player and enemy squads establishing a front, detecting enemies, firing, spending ammo, taking damage, regrouping/withdrawing, and avoiding dumb open-ground charges.
- Man or scenario-trigger rifle bay, MG point, mortar, aid, command, and supply support brains.
- Confirm generated art that is now runtime-wired renders acceptably in Unity Play Mode/F9 before treating it as accepted runtime art.
- Preserve the 50 squad / 33 role / 12 emplacement ambition as catalog/future scope for behaviour that has not been visually or smoke verified, while recognizing that the 50 planned templates are now command-smoke runtime-spawnable.
- Write a short-term report with screenshots/log paths, checks run, failures, and next gate.

## Constraints

- Do not modify raw Obsidian GPT Pro packages.
- Do not work in other TWB projects.
- Do not update permanent Obsidian wiki/index/hot/log memory.
- Use bounded child subagents for substantive audit slices.
- Set a short heartbeat while child subagents work.
- Do not stage, commit, reset, or broad-clean.
- Do not claim code, Unity Play Mode, import, scene, or visual verification unless actually run.

## Current Evidence Boundary

- The command/general/mission plan has already been tailored and partially implemented in scoped form.
- The 2026-05-23 command smoke now proves the 50-template roster is runtime-spawnable and has non-placeholder mission decision hints where required. The older "only four runtime squads" statement now applies only to the legacy opening drill, not the whole command/unit-tree roster.
- War-art runtime wiring now gives selected generated art a rendering path, but Play Mode/F9 visual acceptance and packaged-build-safe loading remain unproven.
- Front-establishment certification passes for deterministic seed `6107`, while the broader `6100-6120` sweep still has two residual failures: seed `6109` front-line MG socket coverage and seed `6116` hardpoint pad density.
- The latest readiness audit found the war side suitable for controlled systems testing, not broad playtest readiness.

## Checks

- Run the relevant Unity menu/batch smokes when practical: simulation smoke, command plan smoke, and front-establishment certification diagnostic.
- Use Play Mode/F9 for visible war-side proof, because `dotnet build` is a weak signal for this Unity project.
- Capture screenshots or video plus console/log evidence.
- Record whether the two residual seed-sweep failures are fixed, still present, or deliberately deferred.
