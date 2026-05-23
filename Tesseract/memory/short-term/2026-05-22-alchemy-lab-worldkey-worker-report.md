# Alchemy Lab World Key Worker Report - 2026-05-22

## Scope

Parent project: The World Beneath.

World Key: The Alchemy Lab.

Task shifted during the run from a narrow cave/pet-loop prototype pass to a broader audit and release-planning packet for the full Alchemy Lab game.

## Summary

Read the worker hydration prompt and required Alchemy/TWB context. Spawned a bounded child worker for the original cave/pet-loop pass, then interrupted and redirected it when Bob changed the objective. Used read-only advisory child subagents for audit/planning lenses and consolidated the result into a project-local release-planning packet under `docs/release-planning`.

No permanent Obsidian memory was updated.

## Work completed

- Audited current Alchemy implementation and docs.
- Verified current automated checks.
- Ran a short browser smoke of the current app and cave view.
- Created a detailed markdown release-planning packet:
  - `docs/release-planning/00_index.md`
  - `docs/release-planning/01_current_audit.md`
  - `docs/release-planning/02_release_scope_and_cut_sheet.md`
  - `docs/release-planning/03_three_stage_crafting_screen.md`
  - `docs/release-planning/04_cave_harvesting_isometric.md`
  - `docs/release-planning/05_pet_exploration_contract.md`
  - `docs/release-planning/06_art_animation_multimask_pipeline.md`
  - `docs/release-planning/07_inventory_online_integration.md`
  - `docs/release-planning/08_achievements_progression.md`
  - `docs/release-planning/09_tutorial_help_info.md`
  - `docs/release-planning/10_testing_release_roadmap.md`
- Continued the packet with component-level planning:
  - `docs/release-planning/11_world_key_canon_alignment.md`
  - `docs/release-planning/12_recipe_economy_and_materials.md`
  - `docs/release-planning/13_screen_ux_and_player_flow.md`
  - `docs/release-planning/14_system_architecture_refactor_plan.md`
  - `docs/release-planning/15_release_assets_packaging_and_launch.md`
  - `docs/release-planning/16_worker_briefs_and_backlog.md`
- Integrated GPT Pro's art production package into the plan after the system-building gates:
  - `docs/release-planning/17_gpt_pro_art_package_integration.md`
- Audited the comprehensive plan for release-readiness holes and patched the packet with:
  - `docs/release-planning/18_release_readiness_gap_audit.md`
  - `docs/release-planning/19_lab_identity_settings_accessibility_audio.md`
  - `docs/release-planning/20_save_error_offline_and_debug_hardening.md`
  - `docs/release-planning/21_near_release_ready_acceptance_matrix.md`
  - `docs/release-planning/22_playtest_and_feedback_plan.md`
- Updated the roadmap and worker backlog so lab identity, settings/accessibility/audio, save/error/offline/debug hardening, structured playtests, and acceptance evidence are explicit gates.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\00_index.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\01_current_audit.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\02_release_scope_and_cut_sheet.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\03_three_stage_crafting_screen.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\04_cave_harvesting_isometric.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\05_pet_exploration_contract.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\06_art_animation_multimask_pipeline.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\07_inventory_online_integration.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\08_achievements_progression.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\09_tutorial_help_info.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\10_testing_release_roadmap.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\11_world_key_canon_alignment.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\12_recipe_economy_and_materials.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\13_screen_ux_and_player_flow.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\14_system_architecture_refactor_plan.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\15_release_assets_packaging_and_launch.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\16_worker_briefs_and_backlog.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\17_gpt_pro_art_package_integration.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\18_release_readiness_gap_audit.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\19_lab_identity_settings_accessibility_audio.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\20_save_error_offline_and_debug_hardening.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\21_near_release_ready_acceptance_matrix.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\release-planning\22_playtest_and_feedback_plan.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-alchemy-lab-worldkey-worker-report.md`

Generated build output in `dist\` was refreshed by `npm run build` during verification.

## Checks run

From `C:\Users\yrred\Desktop\Unity\TWB-Alchemy`:

- `npm run typecheck` - passed.
- `npm run build` - passed with known large chunk warning.
- `npm run dev` - served at `http://127.0.0.1:5174/`.
- Browser smoke - loaded app and cave view; no console errors in the short pass.
- Continued markdown-only pass verified packet coverage and reran `npm run typecheck`.
- GPT Pro art package inspected at `C:\Users\yrred\Downloads\the_alchemy_lab_art_codex_package.zip`; plan updated to run it as Gate G after the system-building gates.
- Release-readiness audit pass verified new docs are indexed, roadmap/backlog gates are visible, and `npm run typecheck` still passes.

## Cleanup performed

- Interrupted the original child worker when the task objective changed.
- Child worker reported stopping a leftover Vite server and removing temporary Vite logs it created.
- A temporary Vite server was started for browser smoke during this worker pass, then stopped during cleanup.

## Risks

- The current app is not release-ready for the requested new goal: crafting is still one-click timed brewing, not a three-stage machine.
- Current cave is a fixed top-down maze, not the requested generated 2.5D/isometric block cave.
- Online inventory is not ready; current shared inventory is browser localStorage.
- `window.__alchemyDebug` is useful for development but must be dev-gated or removed before public/account-connected release.
- `AlchemyLabScene.ts` remains a large single-scene implementation and should not absorb every release system without small module extraction.
- Browser smoke did not clear localStorage, so clean first-run testing remains required.
- The plan now covers lab identity, settings, accessibility, audio, save migration, corrupt save recovery, offline/account wording, debug exposure, playtest protocol, and acceptance evidence; implementation still remains to be done.

## Memory-worthy notes

- The Alchemy release target has changed materially: release planning now targets a two-screen World Key with a harvesting cave and one-screen three-stage crafting machine.
- The old "not true isometric" cave direction is superseded for future planning by a new requested 2.5D/isometric-style block cave target, but this needs precise projection and generation contracts before implementation.
- Online inventory, account pet locks, and server achievements are platform gates, not local prototype polish.
- GPT Pro's art package should be treated as the first art-production vertical-slice runbook after the three-stage crafting/cave preview systems exist, not before.
- "Very close to release ready" now means the near-release-ready acceptance matrix is complete or exceptions are explicitly accepted, not merely that the prototype boots.

## Do not promote to memory

- Do not promote the exact markdown plan as a final design decision until Bob/orchestrator reviews it.
- Do not promote localStorage keys as production API contracts.
- Do not promote current cave visuals as final art direction.

## Next recommended gate

Review `docs/release-planning/16_worker_briefs_and_backlog.md` and commission Gate A or Gate B depending on appetite. Keep Gate D1 and Gate F1 in the near-term sequence before GPT Pro art production, because settings/save/debug hardening will prevent expensive art integration churn later.
