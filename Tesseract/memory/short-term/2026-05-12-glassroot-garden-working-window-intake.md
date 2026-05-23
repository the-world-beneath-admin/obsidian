# Working Window Intake - 2026-05-12 - Glassroot Garden

## Project Identity
- Project/window name: TWB Farming World Key - Glassroot Garden
- Main goal: Build and refine a browser Phaser/Vite farming World Key prototype with a complete local loop from planting through harvesting, drying, bundling, contracts, XP, compost, and shared World Key transfers.
- Scope: Local in-browser prototype, Phaser hand-drawn placeholder art, UI-heavy game loop, storage/workbench systems, progression balance, and player-facing clarity. Cloud/persistence beyond local save is not in scope yet.
- Code/project directory: C:\Users\yrred\Desktop\Unity\TWB-Farming
- Related Obsidian lane, if known: The World Beneath / World Key farming systems, exact lane not confirmed.
- Suggested future worker role name: glassroot-garden-worker

## Current State
The Glassroot Garden prototype has a playable garden screen with 9 plots, Companion planting/harvesting automation, a storage hut/workbench overlay, raw and dried plant bins, drying rack, Bundler, Notice Board contracts, Transfer Bundles, finished bundle rack, compost heap, mastery XP, tier progression, and debug helpers.

Recent work focused on closing the core loop and correcting compost/progression behavior:
- Normal plants can be planted from a mobile-friendly seed bag using click/select/commit.
- Companions till, fetch seed, plant, handle optional work windows, harvest, and deliver outputs.
- Harvested normal crops go to raw bins unless failed, in which case they go to compost feedstock.
- Raw plants can be dried in batches of 5. Finished drying moves to dried bins when space exists.
- Dried plants can be loaded into Bundler recipes.
- Notice Board bundles award tokens, Notice Board completion credit, and XP.
- Transfer Bundles move to World Key shared storage without XP.
- Compost bin clean-out exists for raw/dried bins.
- Comfreygrass is the compost filler plant. It is free to plant, grows for 2 minutes, harvests into 5 curing compost, and does not consume ready compost.
- Compost feedstock cures into ready compost at 1 unit per 15 seconds.
- Tier-based growth timing was slowed: T1 60s, T2 90s, T3 120s, T4 180s, T5 240s.
- Optional work windows were widened across the growth cycle so a player can reasonably attempt them.
- Storage/workbench art direction moved toward a 2.5D herbalist workbench with a back board and table surface, but art is still placeholder Phaser shapes.

Currently in progress: user was about to test the full local loop after the dev server was rebooted.

Not yet started or not complete:
- Tutorial/onboarding.
- Final art assets.
- Cloudflare/database integration.
- Full production persistence.
- Formal automated test suite.
- Final balance pass after real playtesting.

## Files And Areas Touched
- C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts
- C:\Users\yrred\Desktop\Unity\TWB-Farming\src\main.ts
- C:\Users\yrred\Desktop\Unity\TWB-Farming\src\style.css
- C:\Users\yrred\Desktop\Unity\TWB-Farming\Loop_Closure_And_Player_Clarity_Implementation_Plan.md
- C:\Users\yrred\Desktop\Unity\TWB-Farming\Full_Loop_Test_And_Implementation_Plan.md
- C:\Users\yrred\Desktop\Unity\TWB-Farming\Next_Phase_Magitech_Processing_And_Contracts_Plan.md
- C:\Users\yrred\Desktop\Unity\TWB-Farming\Storage_Workbench_Redesign_Implementation_Plan.md
- C:\Users\yrred\Desktop\Unity\TWB-Farming\Storage_Workbench_Bin_Module_Refinement_Plan.md
- C:\Users\yrred\Desktop\Unity\TWB-Farming\Magitech_Farming_Work_Stages_Implementation_Plan.md
- C:\Users\yrred\Desktop\Unity\TWB-Farming\TWB_Glassroot_Garden_GPT_Pro_Research_Plan.md
- Possible generated browser test output: C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\
- Build output: C:\Users\yrred\Desktop\Unity\TWB-Farming\dist\

## Decisions Made
- Decision - Use "Companion" in UI terminology where practical.
- Source - User preference and implemented UI copy.

- Decision - Seed planting should be mobile-friendly: select seed, then press Plant Selected. Do not rely on drag/drop planting.
- Source - User instruction and implemented seed bag flow.

- Decision - Storage/workbench should feel like an old herbalist/alchemical workbench, not a full room or data dashboard.
- Source - User art direction with screenshots and implementation passes in GlassrootGardenScene.ts.

- Decision - Raw, drying, dried, compost, finished bundle, and board information should live near the relevant object, not in one general summary strip.
- Source - User correction with screenshot boxes/arrows.

- Decision - Notice Board contracts give XP/rewards. Transfer Bundles are for World Key shared storage and do not give XP.
- Source - User progression instruction and implemented recipe behavior.

- Decision - Tier unlock requirements are 200 T1 XP/units to unlock T2, 500 T2 to unlock T3, 1000 T3 to unlock T4, and 10000 T4 to unlock T5.
- Source - User balance instruction and implemented tier constants.

- Decision - XP should appear as floating ticks at action locations rather than many static XP indicators.
- Source - User balance/UI instruction and implemented XP tick behavior.

- Decision - Comfreygrass is a free compost filler plant. It does not cost ready compost and harvests into curing compost.
- Source - User correction and implemented compostOnly crop behavior.

- Decision - Normal plant growth is slowed by tier: T1 60s, T2 90s, T3 120s, T4 180s, T5 240s. Comfreygrass remains 120s.
- Source - User request to slow growth and latest implemented timing constants.

## Memory-Worthy Facts
- Fact - The project is a Phaser 3.90 + TypeScript + Vite browser prototype.
- Source - Project package/scripts and handoff context.

- Fact - Main source file is C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts.
- Source - Project structure and repeated implementation work.

- Fact - Required build check after code changes is npm run build.
- Source - User instruction.

- Fact - Local dev server command is npm run dev from C:\Users\yrred\Desktop\Unity\TWB-Farming.
- Source - User instruction and latest server reboot.

- Fact - Local test URL is http://127.0.0.1:5173/.
- Source - User instruction and server check returned 200.

- Fact - The project currently is not a git repository, so do not rely on git diff/status unless initialized later.
- Source - User handoff context.

- Fact - World Key shared storage is separate from main game inventory.
- Source - User design instruction.

- Fact - The crop roster includes 20 folklore/alchemical plants plus the compost filler plant Comfreygrass, whose internal id remains "middenbloom" for compatibility.
- Source - Implemented crop table and save-compatibility decision.

- Fact - Compost has two states: curing/feedstock and ready compost. Curing compost converts to ready compost at 1 per 15 seconds.
- Source - Implemented compost system and user instruction.

- Fact - Comfreygrass should create compost and must not consume ready compost.
- Source - User correction and focused smoke test.

## Risks / Warnings
- Warning - The entire prototype is heavily concentrated in GlassrootGardenScene.ts, increasing merge/conflict and regression risk.
- Warning - The workbench visuals are still Phaser shape placeholders; future asset integration may require layout rework.
- Warning - Local state is in-memory/local save style and may reset or diverge during dev server reloads.
- Warning - No git repository means there is no easy diff/rollback safety unless a repo is initialized later.
- Warning - The internal id for Comfreygrass is still "middenbloom"; renaming the id directly could break saved data unless migrated carefully.
- Warning - XP/balance values are early tuning and should be playtested with real full-loop timing.
- Warning - The game has debug helpers on window.__glassrootDebug; useful for tests but should be gated or removed for production.
- Warning - Vite build warns about a large Phaser chunk. This is expected for now but may matter later.
- Warning - There is no tutorial yet, so player comprehension for drying, compost, bundling, and transfer rules is not fully validated.

## Open Questions
- Should Comfreygrass continue to create curing compost first, or should it bypass curing and add ready compost directly? Current system keeps the 1 per 15s curing rule.
- Should optional "Feed Soil" eventually spend ready compost, or stay a free Companion action?
- What is the final Obsidian lane name for this World Key farming project?
- Should persistence be localStorage-only for the prototype or moved next to Cloudflare/D1?
- What final art asset pipeline will replace Phaser placeholder shapes?
- How much tutorial scaffolding is needed for younger players and older players to understand the full loop without reading debug-like UI?
- Should tier XP represent plant units, full processed plants, contract completions, or a blended mastery model long-term?

## Do Not Promote
- Temporary screenshot markup colors, arrows, and box coordinates.
- One-off visual complaints such as "looks like I am tripping" except as evidence that skewed UI panels should be avoided.
- Failed table/bench layout attempts with disjointed legs and clutter.
- Any old claim that Middenbloom/Comfreygrass costs ready compost.
- Raw implementation scratch coordinates unless they become stable layout constants.
- Browser tab content outside the game; screenshots included unrelated open tabs and should not become memory.

## Current Blockers
- No hard blocker for local prototype testing.
- Full loop still needs current manual playtest after the latest timing and compost fixes.
- No formal automated regression suite yet.

## Checks Run
- npm run build passed after code changes. Vite large chunk warning appeared and is expected.
- Playwright/headless browser smoke tested Comfreygrass planting from the seed bag.
- Smoke result: Comfreygrass selected text said it is free, grows for 2m 00s, and harvests into 5 curing compost.
- Smoke result: planting Comfreygrass kept ready compost at 0 and queued/planted normally.
- Smoke result: forced ready Comfreygrass harvest produced 5 curing compost, rawTotal stayed 0, and plot entered harvest lockdown.
- Dev server rebooted with npm run dev and http://127.0.0.1:5173/ returned HTTP 200.
- Earlier full-loop audit smoke tests were run using window.__glassrootDebug and Playwright-style checks; they covered planting, raw-to-drying-to-dried, Notice Board XP/tokens, transfer storage without XP, failed harvest compost, compost conversion, tier unlock, save/reload, and Comfreygrass compost routing.

## Cleanup Needed
- C:\Users\yrred\Desktop\Unity\TWB-Farming\dist\ is generated build output.
- C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\ may contain screenshots or temporary audit artifacts.
- Dev server process may still be running for user testing.
- Stale planning docs may still contain old terms or outdated visual notes beyond the specific Comfreygrass correction already made.
- No cleanup was performed.

## Recommended Obsidian Tree
- memory/wiki/the-world-beneath/glassroot-garden/overview.md
- memory/wiki/the-world-beneath/glassroot-garden/decisions.md
- memory/wiki/the-world-beneath/glassroot-garden/systems.md
- memory/wiki/the-world-beneath/glassroot-garden/open-questions.md
- memory/wiki/the-world-beneath/glassroot-garden/testing.md
- memory/reports/the-world-beneath/glassroot-garden/
- memory/short-term/

## Recommended Worker Agent
- Agent name: glassroot-garden-worker
- Purpose: Continue implementation, audit, and player-facing refinement for the TWB Farming World Key - Glassroot Garden Phaser prototype.
- Read-first files:
  - C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts
  - C:\Users\yrred\Desktop\Unity\TWB-Farming\Full_Loop_Test_And_Implementation_Plan.md
  - C:\Users\yrred\Desktop\Unity\TWB-Farming\Loop_Closure_And_Player_Clarity_Implementation_Plan.md
  - C:\Users\yrred\Desktop\Unity\TWB-Farming\Next_Phase_Magitech_Processing_And_Contracts_Plan.md
  - C:\Users\yrred\Desktop\Unity\TWB-Farming\Storage_Workbench_Redesign_Implementation_Plan.md
- Allowed write paths:
  - C:\Users\yrred\Desktop\Unity\TWB-Farming\src\
  - C:\Users\yrred\Desktop\Unity\TWB-Farming\*.md
  - C:\Users\yrred\Desktop\Unity\TWB-Farming\output\
  - C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\
- Forbidden write paths:
  - C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\
  - C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md
  - C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md
  - C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\log.md
  - Any permanent Obsidian memory path unless Bob/orchestrator explicitly approves.
- Done criteria:
  - User can complete planting -> optional work -> harvest -> raw bin -> drying -> dried bin -> bundling -> Notice Board XP/tokens.
  - User can complete dried transfer bundle -> World Key shared storage without XP.
  - User can use compost loop: failed harvest/bin clean-out/Comfreygrass -> curing compost -> ready compost.
  - npm run build passes after code changes.
  - Browser smoke test or manual verification is reported.
  - Any handoff goes to memory/short-term/ only.
- Report destination: memory/short-term/

## Next Recommended Gate
Have Bob/orchestrator review this intake, then run a fresh manual full-loop playtest at http://127.0.0.1:5173/ before making more balance or UI changes.
