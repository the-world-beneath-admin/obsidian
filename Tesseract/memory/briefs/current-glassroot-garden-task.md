# Current Glassroot Garden Task

## Status

Active - updated 2026-05-22 after Garden worker failure during pre-release audit.

## Scope

- Parent project: The World Beneath.
- World Key: The Garden.
- Internal/source name: Glassroot Garden.
- Code directory: `C:\Users\yrred\Desktop\Unity\TWB-Farming`.

This is not a cloud integration, account sync, production deployment, marketing task, main-game task, Trenchworks task, or new art-generation task.

## Worker Role

`glassroot-garden-worker`

This is now a standing worker lane. The worker may continue with the user across multiple Garden tasks, but must write a short-term report when the user says `REPORT`, `report`, `write report`, or `decommission`.

## Latest Worker Report

The 2026-05-19 Garden worker final decommission report completed a mobile/touch review, additional Workbench polish, Garden achievement/pet scaffolding, and a failed bundling-machine art integration attempt.

The current Garden worker reportedly stopped working while finishing a pre-release audit and preparing to audit required sound effects and music. A final decommission report is still needed if the old window will accept input. If it will not, the next worker should treat the 2026-05-19 report plus current source state as the recovery baseline and begin by writing a fresh audit plan from the codebase.

Confirmed:

- Storage Hut / Herbalist Workbench now uses image-backed basement backdrop, wooden work table, wall-mounted drying rack, ornate Notice Board, and raw/dried storage panels.
- Focused mobile/touch review found portrait-phone Scale.FIT makes the Workbench too small; current direction is landscape support/requirement rather than forcing the room into portrait.
- Notice Board and Transfer Bundle recipe data now live in `src\data\bundleCatalog.ts`.
- Generated Notice Board catalog has 100 orders per tier, 500 total.
- Generated Notice Board orders now require exactly 3 distinct plant inputs with varied quantities.
- Expired Notice Board orders refill after a randomized 1-3 minute delay.
- Notice Board cards show single-line titles; detailed inputs are shown in the Bundler panel.
- Transfer Bundles remain repeatable and Notice Board orders remain one-off.
- Raw/dried bins are scrollable, capped at 999 units each, and no longer expose whole-bin compost controls.
- Garden achievement UI/scaffolding and Garden pet board/roster/stamina/subskill scaffolding were advanced.
- Garden pet subskills remain World-Key-specific and separate from main-game pet balance.
- Platform client integration was extended for Garden pet catalog/account-owned pets with graceful local fallback while authoritative endpoints remain a shared-platform concern.
- Finished-bundles rack/package art was processed and wired into Storage Hut.
- The latest v6 bundling-machine runtime sheets were processed and wired, but visual QA failed: moving press/clamp pieces detached from the arms/base because the generated parts did not share stable anchors, sockets, or one compositional footprint.
- `npm run build` passed with the known Vite large chunk warning.
- Browser smoke at `http://127.0.0.1:5173/` loaded and the Workbench could be entered.
- Project folder did not present as a Git repo during the worker's check, so no reliable `git diff` summary was available.

## Current Gate

The active Garden gate is now pre-release readiness recovery and audio planning.

Next narrow gate:

- Salvage a final report from the old Garden worker if possible before archiving it.
- New Garden worker should resume as an open-ended coordinator, not a one-task worker.
- Start by reading the latest Garden memory and source state, then create a current pre-release audit checklist from the live project.
- Continue or reconstruct the pre-release audit from source and existing reports.
- Then perform a focused audio requirements audit: list needed sound effects, music loops, ambience, UI feedback sounds, and priority/implementation notes for The Garden.
- Do not generate audio yet.
- Do not connect external services or deploy.
- Preserve Notice Board lifecycle, Transfer Bundle repeatability, starter-pet board, storage hut/workbench, and current Garden visuals unless a reproducible release-blocking issue is found.
- Run `npm run build` after code changes.

## Current Garden Main-Screen State

- Approved PNG architecture/boundary path is active.
- Main scene file: `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`.
- Main screen has a back wall, worker break entry, tool nook entry, store entry, bottom boundary wall, side walls, corner caps, top wall returns, and top corner planters.
- The grid is 12 plots in a `4 x 3` layout.
- Tier 1-5 plot, well, compost, and compost-fill visuals are wired.
- Tool shed and herbalist hut door marker plaques are installed and visible.
- `SHOW_WALK_DEBUG_OVERLAY = false`.
- Starter-pet selector board is installed and uses Chuck/Peggy/Stanly imagery.
- Chuck, Peggy, and Stanly are wired with icon images and moving sprites.
- The worker-break/pet door uses separate portal-background and door-foreground sprite layers.
- The seed bag is image-backed and uses tier tabs.
- Growing timers live in the plot info panel.
- Drying-room occupied slots can be inspected, and ready bundles can be manually collected while the room is open.
- Notice Board quest bundles are one-off; Transfer Bundles remain repeatable.
- Storage Hut / Herbalist Workbench now uses image-backed room assets: basement brick/floor backdrop, wooden work table, wall-mounted drying rack, ornate Notice Board, and raw/dried storage panels.
- Notice Board / Transfer Bundle data now lives in `src\data\bundleCatalog.ts`.
- Notice Board generated orders are 500 total, 100 per tier, with 3 distinct plant inputs and varied quantities.
- Raw/dried bins are scrollable and capped at 999 units each.
- Portrait phone layout is not the target for the Workbench; require or guide to landscape for the current room scale.
- The v6 bundling-machine runtime art path is failed reference evidence only until reviewed; do not promote it as final art.

## Read First

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\slynyrd-pixelblog-reference.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\external-game-dev-resource-index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\world-keys.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\the-garden\overview.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\the-garden\decisions.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\the-garden\systems.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\the-garden\testing.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\the-garden\art-direction-and-asset-risks.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\the-garden\open-questions.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-18-glassroot-garden-worker-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-19-glassroot-garden-worker-final-decommission-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-17-glassroot-garden-notice-board-lifecycle-hardening-report.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\Garden_Main_Screen_Art_Master.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\Full_Loop_Test_And_Implementation_Plan.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\Loop_Closure_And_Player_Clarity_Implementation_Plan.md`

## Allowed Write Paths

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\` only after checking references and only when the user has approved the source PNG/install step.
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\*.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\`

## Forbidden Write Paths

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\log.md`
- Any permanent Obsidian memory path unless Bob/orchestrator explicitly approves.
- Any newly generated art/media file created by the worker.
- Any external image generation tool from inside Codex.
- Any direct use of rejected/suspect assets as final game art.
- `C:\Users\yrred\.codex\generated_images\`

## Hard Rules

- Do not generate new art inside Codex.
- Do not delete assets without first checking references with `rg`.
- Do not replace installed pet selector board, door assets, seed bag assets, storage card assets, or plant sprites without a narrow user-approved reason.
- Do not remove the Notice Board duplicate-order guard merely to support repeatable daily orders.
- If the old all-plots plant/bar artifact appears again, treat it as an active-save/browser-state risk and document the save context.
- Add any render method before adding its call site.
- Keep tool shed and herbalist hut plaques visible.
- Run `npm run build` after code changes.

## Done Criteria For Next Report

When the user asks the worker to report/decommission:

1. Summarize work completed since hydration.
2. List changed files only.
3. List screenshots or browser evidence captured.
4. Include a pre-release audit checklist with status: Pass, Needs Work, Blocked, or Not Checked.
5. Include an audio requirements list covering SFX, music, ambience, UI feedback, and implementation priority.
6. Confirm `npm run build` result if code changed.
7. Explain cleanup performed.
8. Record risks and memory-worthy notes.
9. Recommend the next Garden release gate.

## Report Destination

`C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\YYYY-MM-DD-glassroot-garden-worker-report.md`
