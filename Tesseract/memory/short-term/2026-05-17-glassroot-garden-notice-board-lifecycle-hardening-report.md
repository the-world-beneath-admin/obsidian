# Glassroot Garden Notice Board Lifecycle Hardening Report

## Task

Verify and harden the Notice Board / finished bundle lifecycle for The Garden World Key, internal/source project Glassroot Garden / TWB-Farming.

Scope:

- Parent project: The World Beneath.
- World Key: The Garden.
- Code directory: `C:\Users\yrred\Desktop\Unity\TWB-Farming`.
- Focus: Notice Board one-off orders, finished bundle rack state, Transfer Bundle repeatability, and practical save/reload behavior.

## Result

Passed. No source change was needed.

`npm run build` passed on 2026-05-17. The focused Playwright/browser pass verified the current Notice Board lifecycle on a clean local save and through save/reload checks. The finished bundle rack remained readable in the captured 1280 x 720 review image.

## Notice Board Lifecycle Findings

- Clean save Greenward Order started as `Open`.
- After bundling, Greenward Order moved to `Awaiting completion` with one active finished bundle rack entry.
- Save/reload while awaiting preserved the active awaiting bundle.
- A duplicate Greenward Order attempt while awaiting was blocked with event text: `Greenward Order is already awaiting completion on the finished bundle rack.`
- After forcing the rack processing complete, Greenward Order moved to `Complete`, awarded 18 tokens, and recorded one Notice Board completion.
- Save/reload after completion preserved the completed order state.
- A duplicate Greenward Order attempt after completion was blocked with event text: `Greenward Order is already complete.`

## Transfer Bundle Repeatability Result

Passed. `transfer_basil` was bundled and force-finished twice in the same clean test run.

- First completion increased shared Basil storage to `1`.
- Second completion increased shared Basil storage to `2`.
- Notice Board completion count remained unchanged during Transfer Bundle processing.

## Files Touched

No source files were edited.

Created evidence/report files:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\notice-board-lifecycle-hardening-1280x720.png`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-17-glassroot-garden-notice-board-lifecycle-hardening-report.md`

Generated build output:

- `npm run build` regenerated `dist\` as part of the required build check.

## Screenshots Captured

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\notice-board-lifecycle-hardening-1280x720.png`

The screenshot shows the herbalist storage room with Transfer Bundles selected, the Greenward Notice Order already completed, shared Basil storage at `2`, and an empty finished bundle rack. The rack and board text remained readable without obvious UI overlap at 1280 x 720.

## Checks Run

- `npm run build`
  - Result: passed.
  - Note: Vite still reports the expected large chunk warning.
- Dev server reachability:
  - `http://127.0.0.1:5173/`
  - Result: HTTP `200`.
- Playwright browser lifecycle pass:
  - Reset clean local save in isolated browser context.
  - Opened the storage hut.
  - Verified `Open` -> `Awaiting completion` -> `Complete`.
  - Verified duplicate Notice Board production blocking while awaiting and after completion.
  - Verified awaiting state survived save/reload.
  - Verified completed state survived save/reload.
  - Verified Transfer Bundle repeatability by completing Basil Transfer Bundle twice.
  - Captured a 1280 x 720 screenshot.

## Cleanup Performed

- No temporary test script file was created; the Playwright check ran inline.
- The screenshot was kept intentionally as evidence.
- No source files, permanent memory files, assets, or user files were deleted.
- No staging, commits, resets, broad cleans, or permanent Obsidian memory edits were performed.

## Risks

- The lifecycle was verified through debug hooks and browser interaction, not a formal automated regression suite.
- The user's exact persistent Chrome/localStorage state was not inspected; the pass used an isolated clean browser context plus explicit save/reload checks.
- `GlassrootGardenScene.ts` remains large and high-risk for future bundled UI/state changes.
- Notice Board daily/rotating order reopening is still undesigned. Do not remove the duplicate-order guard to make repeatable daily orders.
- Vite large chunk warnings remain due to Phaser and large image assets.

## Memory-Worthy Notes

- Current Notice Board one-off lifecycle appears stable for Greenward Order on clean state and through practical save/reload checks.
- Transfer Bundles remain repeatable and separate from Notice Board completion counts.
- The current finished bundle rack visual state is readable at 1280 x 720 in the tested storage-room state.
- No source code hardening was required in this pass.

## Do Not Promote To Memory

- Do not promote the exact debug test sequence as player-facing design.
- Do not promote this clean isolated browser pass as proof that every older user save shape is migrated.
- Do not promote the current prototype bundler/packing machine art as final.
- Do not promote Vite bundle sizes or hashed build asset names as durable project facts.

## Next Recommended Gate

Proceed to a narrow visual pass only after Bob/orchestrator reviews this report. Recommended next gate: replace the prototype bundler/packing machine with a layered static body plus small rotating, sliding, particle, and glow child layers. Keep it scoped to the packing-machine presentation and avoid changing the Notice Board lifecycle unless a new bug is reproduced.
