# 2026-05-16 Glassroot Garden Worker Break Portal Door Layered Animation Report

## Task

Cut out the user-provided worker-break / pet-door sprite sheets and wire them as two separate runtime layers: an independently looping portal sheet behind a separate opening/closing door foreground sheet. Preserve the cyan-background cutout process, including removal of cyan and near-cyan border tones, and keep the door interior transparent so the portal shows through.

## Result

Complete. The worker-break doorway now uses two disconnected Phaser sprite sheets:

- Portal background layer: loops independently behind the doorway.
- Door foreground layer: opens and closes over the portal.

When companions return to the worker-break/pet door, the foreground door opens, the portal remains visible and looping behind it, the companion is hidden into the doorway, and the door closes afterward. The composite preview is QA-only; no combined portal+door runtime sprite sheet was installed.

## Whether The Plant/Bar Artifact Was Reproduced

Not retested in this subpass. This task was a follow-on door-animation asset and wiring pass after the earlier pet selector and door work. Earlier clean Playwright passes did not reproduce the user's all-plots mature-plant/blue-bar artifact; this report does not supersede that unresolved browser-state note.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\worker-break-portal-door-open-close-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\worker-break-portal-loop-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\worker-break-portal-door-01\source\worker-break-portal-door-source.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\worker-break-portal-door-01\source\worker-break-portal-loop-source.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\worker-break-portal-door-01\crops\worker-break-portal-door-open-close-cleaned.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\worker-break-portal-door-01\crops\worker-break-portal-loop-cleaned-normalized.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\worker-break-portal-door-01\qa\`

## Assets Converted Or Explicitly Not Converted

Converted from user-provided cyan-background sources:

- `C:\Users\yrred\Desktop\ChatGPT Image May 16, 2026, 12_31_54 AM (2).png`
- `C:\Users\yrred\Desktop\ChatGPT Image May 16, 2026, 01_11_24 AM.png`

Installed assets:

- `worker-break-portal-door-open-close-sheet.png`: 6 frames, 362 x 361 per frame.
- `worker-break-portal-loop-sheet.png`: 8 frames, 362 x 361 per frame, portal scaled into the doorway's usable interior rectangle.

No new art was generated in Codex. No single combined runtime sprite sheet was installed.

## Screenshots Captured

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-worker-break-two-layer-door-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-worker-break-portal-open-or-best-2026-05-16.png`

QA images were also captured under:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\worker-break-portal-door-01\qa\`

## Checks Run

- `npm run build` from `C:\Users\yrred\Desktop\Unity\TWB-Farming` passed.
- Local dev server at `http://127.0.0.1:5173/` returned HTTP 200.
- Playwright screenshot captured the closed two-layer door in scene.
- Timed Playwright probe captured the portal visible while the worker-break door was open.
- Dark/light QA images reviewed after two-step cyan and near-cyan edge cleanup.

## Cleanup Performed

Removed disposable Playwright probe frames after copying the best portal-open capture. Kept source images, cleaned crops, QA images, processing report, and final screenshots as evidence.

## Risks

- The portal and door currently share the existing worker-break display dimensions. It looks functional in the 1280 x 720 check, but the user may still want art-scale or anchor tweaks after live viewing.
- The doorway animation is event-driven by companion returns; overlapping companion entries are serial-gated, but a high-traffic later companion system may need a small queue rather than last-entry timing.
- The all-plots mature-plant/blue-bar artifact remains a separate local-browser-state issue and was not advanced by this door pass.

## Memory-Worthy Notes

- For layered doors, keep the portal/background and door/foreground as separate Phaser sprites, not a baked composite sheet.
- Portal should be scaled to the usable doorway interior so it does not bleed outside transparent foreground areas.
- Cyan cleanup needed both exact/near-cyan removal and a second darker cyan-edge contour pass on the door foreground.

## Do Not Promote To Memory

Do not promote raw QA counts, temporary probe timing, or frame-by-frame screenshot filenames unless this becomes a recurring asset-pipeline rule.

## Next Recommended Gate

Have the user refresh/watch `http://127.0.0.1:5173/` and approve the worker-break door scale, anchor, and timing. If accepted, proceed to the next door/layer polish gate; if not, tune worker-break display width/height and entry timing before broad expansion.

## Addendum - Companion Depth Fix

After live review, the user reported pets were drawing behind the new door sprites. Fixed by adding an explicit `COMPANION_TOKEN_DEPTH = 20` in `GlassrootGardenScene.ts` and applying it to each companion token container, placing pets above door/fixture layers while still below modal/UI panels.

Additional check run:

- `npm run build` passed after the depth fix.

Additional screenshot captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-pets-front-depth-worker-break-open-2026-05-16.png`

Cleanup:

- Removed temporary `garden-pets-front-depth-probe-*.png` Playwright probe frames after preserving the best evidence screenshot.

## Addendum - Tool Shed Pre-Open Timing

After live review, the user reported the tool shed door opened too late. Added a `TOOL_SHED_DOOR_PREOPEN_LEAD_MS = 1000` timing pass so movement to the tool shed schedules the door to begin opening about one second before the companion arrives. The arrival-side tool-shed use now avoids restarting the open animation if the door is already open or opening.

Additional check run:

- `npm run build` passed after the tool-shed timing change.

## Addendum - Herbalist Door Early Open And Staged Deposit

After live review, the user requested the herbalist/herb-shack door open 2.5 seconds sooner and suggested a more realistic deposit beat. Added:

- `HERBALIST_DOOR_PREOPEN_LEAD_MS = 2500`, scheduled from the companion's estimated path duration to the storage drop point.
- A one-second arrival wait at the door before depositing.
- A direct step into the herbalist threshold, deposit processing inside the doorway, a short hold, a step back out, then door close before the companion walks away.

Additional check run:

- `npm run build` passed after the herbalist staging change.

Additional screenshots captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-herbalist-door-staged-open-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-herbalist-door-step-in-out-2026-05-16.png`

Cleanup:

- Removed temporary `garden-herbalist-door-staged-probe-*.png` and `garden-herbalist-door-step-probe-*.png` Playwright probe frames after preserving evidence screenshots.

## Addendum - Tool Shed Stop Point Lowered

After live review, the user reported pets were stepping too far into the tool shed. Moved `TOOL_SHED_SEED_POINT` from `{ x: 785, y: 156 }` to `{ x: 785, y: 186 }`, so tool-shed fetches end 30 pixels lower in front of the doorway.

Additional check run:

- `npm run build` passed after the tool-shed stop-point change.

## Addendum - Door Preopen Holds And Endpoint Tuning

After live review, the user reported the worker-break / pet-shed door waited until companions were on top of it, the herbalist green door opened too early, and multiple companions should not restart door animations while sharing a doorway. Updated `GlassrootGardenScene.ts` so:

- Worker-break / pet-shed returns schedule a pre-open with `WORKER_BREAK_DOOR_PREOPEN_LEAD_MS = 1000`.
- Herbalist pre-open was retuned down to `HERBALIST_DOOR_PREOPEN_LEAD_MS = 1000`.
- Worker-break home/entry endpoint was lowered with `WORKER_BREAK_COMPANION_HOME_Y_OFFSET = 56`.
- Herbalist storage endpoint was lowered to `storageDropY = 177`.
- Tool shed, herbalist, and worker-break doors now use per-companion door holds and door hold counts, so repeated approaches do not restart an already-open/opening door and each door waits until the last held companion releases before closing.

Additional screenshots captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-door-hold-herbalist-held-open-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-door-hold-worker-break-preopen-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-door-hold-worker-break-held-open-2026-05-16.png`

Additional checks run:

- `npm run build` passed after the door hold and endpoint tuning changes.
- A clean Playwright multi-pet probe seeded three ready Basil plots; all three companions harvested and delivered successfully, raw storage reached 6, and screenshots showed the herbalist door held open during overlapping deliveries and the worker-break portal/door opening before companion entry.

Cleanup:

- Removed temporary `garden-door-hold-timing-probe-*.png`, `garden-door-hold-multipet-probe-*.png`, and the temporary contact sheet after preserving the three evidence screenshots above.

Risk:

- Door hold tracking is per companion slot and door kind. It handles the current starter-pet flow, but if later systems interrupt a pet mid-door-use or teleport companions between doors, the hold map should be revisited so delayed releases cannot affect a new task.

## Addendum - Worker-Break Door Opens Before Pet Emergence

After live review, the user reported pets were emerging through the pet-shed door before the door opened. Updated `GlassrootGardenScene.ts` so hidden companions leaving the worker-break/pet shed now:

- Begin a worker-break door hold before becoming visible.
- Open the worker-break door and portal first.
- Wait for the door-open readiness plus a short `WORKER_BREAK_DOOR_EXIT_REVEAL_PAUSE_MS = 180` beat.
- Appear at the doorway, step down to the top walk lane, release the door hold, then continue to the requested task or roam point.

Also added `workerBreakDoorOpenReadyAt` so overlapping enter/exit calls wait for the actual open animation readiness instead of assuming an already-opening door is ready after a flat 100ms.

Additional screenshots captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-worker-break-door-open-before-emerge-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-worker-break-pet-emerge-after-open-2026-05-16.png`

Additional check run:

- `npm run build` passed after the pet-emergence timing change.

Cleanup:

- Removed temporary `garden-worker-break-emerge-probe-*.png` frames and the temporary contact sheet after preserving the two evidence screenshots above.

## Addendum - Worker-Break Entry Sparkle/Twist Effect

After live review, the user asked whether a particle-style pet disappearance was possible in this web game. It is feasible in Phaser and was added without new art assets:

- Generated a tiny in-scene sparkle texture at runtime with Phaser graphics.
- Added a disposable particle burst when a companion enters the worker-break/pet shed.
- Added a short squash/pop, spin, shrink, and fade tween so the pet appears to twist inward before it is hidden.
- Added a final sparkle burst at the door after the twist completes.
- Reset companion token scale, alpha, and angle on show/hide so the effect does not leak into later movement.

During verification, the first particle pass revealed a Phaser coordinate issue: creating the emitter at world coordinates and also exploding at world coordinates doubled the offset. Fixed by keeping the emitter at origin and exploding at the companion's world position.

Additional screenshots captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-worker-break-entry-sparkle-twist-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-worker-break-entry-pop-before-hide-2026-05-16.png`

Additional check run:

- `npm run build` passed after the sparkle/twist effect and the particle offset fix.

Cleanup:

- Removed temporary `garden-worker-break-entry-fx-probe-*.png` frames and the temporary contact sheet after preserving the two evidence screenshots above.

Risk:

- The effect is intentionally brief and low-cost. If the user wants a stronger magical read, the next tuning pass should adjust particle size/count and twist duration rather than adding a new asset pipeline.

## Addendum - Well Water Sparkle Particles

After live review, the user requested particle sparkles on the well water. Added a separate runtime-generated `WELL_WATER_SPARKLE_TEXTURE_KEY` glint texture and a restrained continuous particle emitter over the visible water surface in `drawGardenWell`.

Implementation notes:

- The emitter is layered above the well PNG but below companion sprites and UI text.
- The emitter is constrained to the water-surface ellipse using offsets measured from `garden-well-tier-1.png`.
- No new art assets were generated or installed; the glint texture is generated with Phaser graphics at scene startup.

Additional screenshot captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-well-water-sparkle-2026-05-16.png`

Additional check run:

- `npm run build` passed after the well sparkle effect.

Cleanup:

- Removed temporary `garden-well-water-sparkle-probe-*.png` frames after preserving the best evidence screenshot.

Risk:

- The sparkle is subtle by design. If the user wants a stronger magical-water read, increase emitter frequency/count or glint scale before adding another asset.

## Addendum - Well and Compost Inventory Signposts

After live review, the user requested the ground signpost crop be used beside the well and compost heap, with inventory text moved onto the signs.

Changes made:

- Installed `095-cutout.png` as `src\assets\glassroot\garden\inventory-sign-post.png`.
- Added a reusable signpost render helper in `GlassrootGardenScene.ts`.
- Replaced the well label with a signpost that only shows `0/99`; removed the visible `Water` word.
- Replaced the compost label with a signpost that only shows `0/99`; removed `Ready Compost` and `Curing` text from the main view.
- Changed the compost inventory cap from `999` to `99`.
- Set both signpost counters to blue `#6fd7ff` with a dark stroke for readability on the brown boards.

Additional screenshot captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-inventory-signposts-2026-05-16.png`

Additional check run:

- `npm run build` passed after the signpost install and compost-cap change.

Cleanup:

- No temporary probe images or scratch scripts were left from this pass. The source crop was preserved in `output\asset-conversion\garden-main-screen\ground-progression-sheet-01\crops\`.

Risk:

- Existing saves with compost above `99` will now clamp down to the requested cap. Compost feedstock also respects the reduced remaining capacity.

Memory-worthy notes:

- The shared inventory signpost asset is now installed under `src\assets\glassroot\garden\inventory-sign-post.png` and can be reused for future small in-world counters.

Do not promote to memory:

- Exact signpost coordinates should stay provisional until the user accepts the layout after live viewing.

## Addendum - Door Plaque Glyph Shrink

After live review, the user reported the printed icons inside the herbalist-room and tool-shed door plaques were too large and overhanging the plaques.

Changes made:

- Added a shared `GARDEN_DOOR_MARKER_GLYPH_SCALE = 0.8`.
- Scaled only the printed tool and herbalist glyph measurements around each plaque center.
- Left the plaque board size, plaque positions, pet selector board, and pet selector icons unchanged.

Additional screenshot captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-door-plaque-glyph-shrink-2026-05-16.png`

Additional check run:

- `npm run build` passed after the plaque-glyph shrink.

Cleanup:

- No temporary files were created for this pass.

Risk:

- The glyphs are still drawn procedurally. If final art replaces them later, this scale constant should either be removed or applied only to the fallback glyph path.

## Addendum - Worker-Break Portal Step-In Before Disappear

After live review, the user requested pets walk forward into the portal before triggering the sparkle/twist disappearance.

Changes made:

- Added `WORKER_BREAK_DOOR_ENTRY_STEP_IN_DISTANCE = 30`.
- Added `WORKER_BREAK_DOOR_ENTRY_STEP_DURATION_MS = 360`.
- Updated `dismissCompanionIntoWorkerBreak` so, after the worker-break door is open, the pet steps 30 pixels upward into the portal before the sparkle/twist effect starts.
- Added move-serial and door-hold checks around the delayed entry step so interrupted companions do not finish an obsolete portal entry.

Additional screenshot captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-worker-break-entry-step-in-2026-05-16.png`

Additional check run:

- `npm run build` passed after the portal step-in change.

Cleanup:

- No temporary files were created for this pass.

Risk:

- The screenshot verifies clean boot, not the precise animation timing. The live browser should be used to judge whether the 30-pixel step feels deep enough once a pet returns to the portal.

## Addendum - Compost Heap and Short Sign Fit

After live review, the user requested more room around the compost inventory sign.

Changes made:

- Moved `COMPOST_SOURCE_POINT` from `{ x: 1116, y: 552 }` to `{ x: 1088, y: 526 }`, shifting the compost heap up and left.
- Moved the compost sign left by 5 pixels from its prior absolute x-position, now landing at x `1189`.
- Added `src\assets\glassroot\garden\inventory-sign-post-short.png` as a compost-only sign variant.
- Shortened the compost sign shaft by clearing the bottom 12 source pixels, roughly 10 rendered pixels at current display scale.
- Left the well sign using the original full-height signpost.

Additional screenshot captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-compost-heap-sign-fit-2026-05-16.png`

Additional check run:

- `npm run build` passed after the compost/sign layout adjustment.

Cleanup:

- No temporary files were left from this pass.

Risk:

- The compost service point moved with the heap. Pet pathing and resource ticks now target the shifted heap position, which should be checked during live compost deposit flow.

## Addendum - Plot Hover/Active Highlights and Seed Bag Auto-Close

After live review, the user requested visible plot mouseover and active states, plus automatic seed-bag closure after planting or committing a seed.

Changes made:

- Added a dedicated highlight rectangle to each plot model.
- Added per-plot `isHovered` state.
- Added hover styling with a lighter gold frame/fill.
- Added selected/active styling with a stronger gold frame/fill.
- Updated plot refresh so selected-active state persists after click and after plot state changes.
- Closed the seed bag after successful seed queue/commit.
- Also closed the seed bag when the queued seed is actually planted into a plot, so delayed companion planting cannot leave a stale seed panel open.

Additional screenshots captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-plot-hover-highlight-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-plot-active-seedbag-closed-2026-05-16.png`

Additional checks run:

- `npm run build` passed after the plot-highlight and seed-bag closure change.
- Playwright interaction pass hovered a plot, clicked it, selected a seed packet, clicked `Plant Selected`, and captured the post-commit closed-panel state.

Cleanup:

- No temporary files were left from this pass.

Risk:

- The active/hover highlight is intentionally drawn above the plot art. It is low-alpha, but if later plant art becomes denser, the highlight alpha or depth may need a small tuning pass.

## Addendum - Shaped Plot Highlight and Worker-Break Door Hold Tune

After live review, the user reported the plot highlight looked like a square frame instead of following the actual bed, and that the worker-break portal door was staying open too long.

Changes made:

- Replaced the rectangular plot highlight with a graphics-drawn eight-point bed silhouette.
- Kept hover and active/selected states, but now they follow the raised-bed shape rather than a square.
- Reduced worker-break door pre-open lead from `1000ms` to `550ms`.
- Reduced worker-break entry hold from `520ms` to `240ms`.
- Reduced worker-break exit close delay from `450ms` to `260ms`.
- Fixed a stale door-hold path: if a companion is redirected from a held door state to ordinary plot work, its old door hold is now released immediately instead of leaving the portal thinking it is still in use.

Additional screenshots captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-plot-shaped-active-highlight-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-worker-break-door-tuned-after-plant-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-worker-break-door-tuned-later-2026-05-16.png`

Additional checks run:

- `npm run build` passed after the shaped-highlight and door-hold tune.
- Playwright interaction pass clicked a plot, opened the seed bag, committed a seed, and captured both an early worker-break door state and a later closed-door state.

Cleanup:

- No temporary files were left from this pass.

Risk:

- The plot silhouette is hand-tuned to the current Tier 1 plot PNG. If plot art changes shape, the highlight points should be retuned with it.

## Addendum - Real Plot Outline Guide and Panel-Safe Portal Idle

After live review, the user requested the plot hover/active guide be pinned to the real plot shape, with a complete 1-2 pixel outline instead of a square or hand-tuned approximation.

Changes made:

- Generated `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-plot-tier-1-outline.png` from the current Tier 1 plot PNG alpha/render envelope.
- Replaced the hand-tuned Phaser graphics silhouette with a loaded outline texture sized exactly to the displayed plot art.
- Kept the hover/active states, but now both use the same plot-shaped outline guide with different alpha.
- Disabled the previous selected-plot sparkle emitter so the outline remains the only active plot-selection guide.
- Paused hidden idle companion emergence while the seed bag, plot info, or storage room panels are open, preventing the worker-break portal from sitting open behind active garden UI.

Additional screenshots captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-plot-outline-no-sparkles-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-worker-break-panel-idle-paused-2026-05-16.png`

Additional checks run:

- `npm run build` passed after the real-outline asset and panel-safe portal idle change. Vite still reports the existing large chunk warning only.

Cleanup:

- Diagnostic outline preview images were retained under `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\` as visual evidence for the outline-generation pass.

Risk:

- The outline asset is derived from the current `garden-plot-tier-1.png` display dimensions. If the Tier 1 plot art or display size changes, regenerate `garden-plot-tier-1-outline.png` from the updated plot art rather than retuning points by hand.

## Addendum - Compost Heap Fill Overlay

The user requested a visible fill animation for the compost heap using `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\ground-progression-sheet-01\crops\049-cutout.png`, with the mound sliding upward and clipping below a line so it appears to grow from the middle of the heap.

Changes made:

- Installed the supplied cutout as `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\compost-fill-mound.png`.
- Added a Phaser-loaded compost fill mound texture.
- Added a masked compost fill image inside the existing heap art.
- Drove the visual fill level from `compostAmount + compostFeedstock`, so the heap shows both ready compost and curing feedstock as physical contents.
- Kept the sign text on ready compost only, preserving the existing `0/99` usable-compost meaning.
- Added a short tween so the mound slides upward/downward when total heap contents change.
- Used a hidden graphics geometry mask so the mound disappears below the compost box line and reads as rising from the middle.

Additional screenshot captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-compost-fill-mound-70-2026-05-16.png`

Additional checks run:

- `npm run build` passed after the compost fill overlay change. Vite still reports the existing large chunk warning only.

Cleanup:

- No temporary files were removed. The screenshot is retained as evidence. The installed fill asset is now a source asset.

Risk:

- The fill mask is tuned to the current compost heap art and its current screen position. If the heap image, scale, or source point moves again, the mask offsets may need a small visual tuning pass.

## Addendum - Lower Idle Pet Roaming Frequency

The user requested less frequent pet emergence when pets are only roaming.

Changes made:

- Added `COMPANION_ROAM_STEP_INTERVAL_MS`.
- Changed the idle roaming loop from every `4200ms` to every `9000ms`.
- Increased the worker-break idle emergence cooldown from `6000ms` to `22000ms`.
- Kept work-trip behavior unchanged: hidden pets can still emerge immediately when needed for planting, watering, composting, harvest, or storage work.

Additional checks run:

- `npm run build` passed after the idle roaming frequency change. Vite still reports the existing large chunk warning only.

Cleanup:

- No temporary files were created for this pass.

Risk:

- This is a behavioral feel tuning rather than a visual bug fix. If the garden now feels too quiet, reduce `COMPANION_ROAM_STEP_INTERVAL_MS` or `WORKER_BREAK_IDLE_EMERGE_COOLDOWN_MS` slightly rather than touching work-task dispatch.

## Addendum - Slower Companion Travel

The user reported the pets still looked like they were sliding because their movement speed was too fast.

Changes made:

- Slowed companion path movement by roughly 30%.
- Changed `COMPANION_MOVE_DURATION_PER_PIXEL` from `8.8` to `11.4`.
- Changed `COMPANION_MOVE_MIN_DURATION_MS` from `560` to `730`.
- Changed `COMPANION_MOVE_MAX_DURATION_MS` from `2480` to `3225`.
- Left `COMPANION_WALK_FRAME_RATE` unchanged for this pass, so this tuning addresses travel speed without altering the walk-sheet playback.

Additional checks run:

- `npm run build` passed after the companion travel speed change. Vite still reports the existing large chunk warning only.

Cleanup:

- No temporary files were created for this pass.

Risk:

- If the pets now look like their feet are churning too quickly, tune `COMPANION_WALK_FRAME_RATE` separately. This pass intentionally changed only travel timing.

## Addendum - Additional Companion Travel Slowdown

The user requested the walking speed be slowed another 20%.

Changes made:

- Increased companion travel durations by roughly 20% on top of the previous slowdown.
- Changed `COMPANION_MOVE_DURATION_PER_PIXEL` from `11.4` to `13.7`.
- Changed `COMPANION_MOVE_MIN_DURATION_MS` from `730` to `875`.
- Changed `COMPANION_MOVE_MAX_DURATION_MS` from `3225` to `3870`.
- Left `COMPANION_WALK_FRAME_RATE` unchanged again, so this remains a movement-speed-only tuning pass.

Additional checks run:

- `npm run build` passed after the additional companion travel slowdown. Vite still reports the existing large chunk warning only.

Cleanup:

- No temporary files were created for this pass.

Risk:

- If the pets still appear to slide, the next likely adjustment is the walk-sheet frame rate or per-direction frame choice rather than further travel slowdown alone.

## Addendum - Companion Queue Handoff Fix

The user reported that pets were returning to the pet shed even when more actions were queued, instead of moving directly to the next action.

Changes made:

- Added a `finishCompanionWork` handoff path for successful companion jobs.
- Added `assignNextQueuedWorkToCompanion` so a companion that just finished can immediately claim the next ready harvest or queued planting job.
- Updated successful planting, optional work, compost-harvest delivery, failed-harvest compost delivery, and herbalist storage delivery to use the handoff path.
- Kept cancellation/error paths returning home, since those are exceptional plot/resource mismatch states.
- Updated `harvestPlot` to accept an assigned companion, allowing the just-finished pet to claim a ready harvest without going through the generic picker.
- Ensured `returnCompanionHome` marks the companion busy while walking home, preventing the scheduler from grabbing a companion mid-return.

Additional screenshot captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-companion-queue-handoff-2026-05-16.png`

Additional checks run:

- `npm run build` passed after the queue handoff fix. Vite still reports the existing large chunk warning only.
- Seeded Playwright run with 8 queued plots for 50 seconds produced no page errors. Result: 3 planted/growing plots, 1 planting, 2 tilling, and 2 still queued, confirming active handoff into continued work instead of immediate shed return.

Cleanup:

- No persistent test save was written; the queued-plot test used an isolated Playwright browser context.

Risk:

- The handoff currently prioritizes ready harvests before queued planting, matching the scene's existing update order. If user expectations favor finishing manually queued planting first, that priority can be swapped later.

## Addendum - Compost Fill Fade Test

The user asked whether the compost fill animation was wired, then requested a better reveal: the pile should not show below the marked heap line, and should sit on top of the compost heap while fading/revealing from bottom toward top.

Changes made:

- Changed the compost fill mound from a sliding image to a fixed-position overlay sitting on the heap.
- Replaced the slide-up visual with a bottom-to-top reveal mask.
- Moved the clip boundary upward so the mound is invisible below the heap line.
- Added alpha fade tied to fill amount, so the mound fades in as the reveal grows.
- Added `window.__glassrootDebug.startCompostFillVisualTest(durationMs)` as a visual-only debug trigger. It animates the heap fill from empty to full without directly changing saved compost inventory.

Additional screenshots captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-compost-fixed-fade-fill-mid-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-compost-fixed-fade-fill-full-2026-05-16.png`

Additional checks run:

- `npm run build` passed after the fixed-position compost fill/fade change. Vite still reports the existing large chunk warning only.
- Playwright invoked `window.__glassrootDebug.startCompostFillVisualTest(6000)` successfully with no page errors.

Cleanup:

- No persistent test save was written by the visual test pass.

Risk:

- The reveal mask is tuned to the current compost heap image and current user-marked line. If the heap art or position changes, retune `COMPOST_FILL_CLIP_BOTTOM_Y_OFFSET`, `COMPOST_FILL_REVEAL_HEIGHT`, and `COMPOST_FILL_MOUND_Y_OFFSET`.

## Addendum - Compost Smell Wisps

The user requested progressively intense green/brown smell particles wafting off the compost pile and asked for "smell wafting animation" research before implementation.

Research notes:

- Smoke/smell effects should drift upward slowly, with negative/upward gravity or upward emission, longish lifetimes, and fade-out over particle lifetime.
- Smoke reads more naturally when particles spawn from slightly varied origins, grow as they rise, and have varied duration/size rather than uniform motion.
- Cartoon smell is commonly represented by wavy rising lines, so a small wavy wisp texture was used instead of round smoke puffs.

Changes made:

- Added runtime-generated `glassroot-compost-smell-wisp` texture.
- Added three compost smell particle emitters above the compost heap.
- Tied emitter intensity to compost heap fullness:
  - Low fill starts a sparse green wisp layer.
  - Medium fill adds denser green/brown wafts.
  - High fill adds the strongest brown/green waft layer.
- Updated the fill visual test so the smell intensity follows the visual test fill amount.
- Prevented emitters from restarting every refresh frame by tracking emitter active states.

Additional screenshot captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-compost-smell-wisps-visible-2026-05-16.png`

Additional checks run:

- `npm run build` passed after the compost smell particle implementation. Vite still reports the existing large chunk warning only.
- Playwright invoked `window.__glassrootDebug.startCompostFillVisualTest(6000)` successfully with no page errors and captured the smell-wisp state.

Cleanup:

- No temporary files were removed. Screenshots were retained as visual evidence.

Risks:

- Static screenshots under-represent the wafting effect because the wisps are meant to move and fade. Live review at `http://127.0.0.1:5173/` is the better test.
- If the smell reads too subtle or too strong in live view, tune emitter alpha/frequency first before changing heap art.

Sources consulted:

- `https://learn.unity.com/tutorial/modifying-gravity-color-size-lifetime-of-particle-systems`
- `https://www.cryengine.com/docs/static/engines/cryengine-5/categories/23756816/pages/65437722`
- `https://www.cryengine.com/docs/static/engines/cryengine-3/categories/1114113/pages/1048585`

## Addendum - Compost Fill Readability at Mid Inventory

The user reported that a half-full compost heap did not visually look filled, and clarified that `049-cutout.png` should sit on top of the bin and fade/reveal from bottom to top.

Changes made:

- Increased the compost fill mound display size from `112 x 73` to `132 x 84`.
- Increased the reveal mask width/height to cover more of the bin interior.
- Moved the fixed mound placement upward so it sits more visibly on top of the compost heap.
- Added `COMPOST_FILL_VISUAL_GAMMA = 0.55`, so mid inventory values reveal a visually appropriate amount of the mound rather than a mathematically thin lower slice.
- Kept the mound fixed in place; only its bottom-to-top mask reveal and alpha change.

Additional screenshot captured:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-compost-47-fill-readable-2026-05-16.png`

Additional checks run:

- `npm run build` passed after the mid-fill readability tuning. Vite still reports the existing large chunk warning only.
- Playwright loaded a clean context seeded with `47/99` ready compost and captured the heap state with no page errors.

Cleanup:

- No persistent test save was written; the `47/99` compost state used an isolated Playwright browser context.

Risk:

- The visual fill is intentionally non-linear now. It better communicates fullness at a glance, but the sign remains the exact inventory truth.
## Addendum: Plant Production Sprite Sheet Generation Attempt

Task:
- Generate full plant production sprite sheets for all Garden crops, with plot growth stages plus raw-bin, drying-rack undried, drying-rack dried, and dry-bin bundle states.

Result:
- Partial package created under `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\plant-production-sprite-prompts`.
- 13 of 21 plant sheets were generated, copied into the Garden output folder, cut out, previewed, and split into individual transparent cell sprites.
- The built-in image generator then refused additional jobs. No local `OPENAI_API_KEY` is currently set for CLI fallback generation.

Plant sheets generated:
- Basil, thyme, yarrow, sage, nettle, comfreygrass, rosemary, mugwort, lavender, rue, vervain, wormwood, angelica.

Plant sheets not generated:
- Wolfsbane, belladonna, foxglove, mistletoe, henbane, mandrake, rowan, elder.

Files touched:
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\plant-production-sprite-prompts\`

Assets converted:
- Source cyan sheets copied into `generated-source`.
- Transparent cutout sheets written to `cutout-sheets`.
- Eight per-plant cell sprites written under `cutout-cells`.
- Dark/light QA previews written to `previews`.

Checks run:
- Visual spot-check of basil dark preview after first and second cleanup pass.
- Count check confirmed 13 source sheets and 104 extracted cell sprites.

Cleanup performed:
- Generated image originals were left in Codex's generated image cache as required; copied project-bound versions are stored under the Garden output folder.

Risks:
- The completed sheets have not been installed into runtime code.
- Generated art still needs species-by-species visual approval before installation.
- Remaining eight plants need generation through a resumed built-in imagegen pass or a confirmed API-key-backed CLI fallback.

Memory-worthy notes:
- For plant production art, one 2x4 sheet per plant is the safer prompt shape.
- Required states per plant are seed/planted, sprout, mature, ready-harvest, raw-bin, drying-undried, drying-dried, and dry-bundle.

Do not promote to memory:
- Specific generated sprite files until the user approves the visual style.

Next recommended gate:
- Review the partial package previews, then complete the remaining eight plant sheets before wiring plant sprites into runtime rendering.

## Addendum: Plant Production Sprite Sheet Completion

Task:
- Resume the rolling-cooldown image generation pass and complete the remaining plant production sprite sheets.

Result:
- Complete 21-plant package created under `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\plant-production-sprite-prompts`.
- All 21 plant source sheets were generated, copied into the Garden output folder, cut out, previewed, and split into individual transparent cell sprites.

Additional plant sheets generated:
- Wolfsbane, belladonna, foxglove, mistletoe, henbane, mandrake, rowan, elder.

Final counts:
- Source cyan sheets: 21
- Transparent cutout sheets: 21
- Preview sheets: 42
- Extracted transparent cell sprites: 168

Files touched:
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\plant-production-sprite-prompts\`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\plant-production-sprite-prompts-complete-2026-05-16.zip`

Assets converted:
- All plant source sheets copied into `generated-source`.
- All transparent cutout sheets written to `cutout-sheets`.
- Eight per-plant cell sprites written under `cutout-cells`.
- Dark/light QA previews written to `previews`.

Checks run:
- Count check confirmed 21 source sheets, 21 cutout sheets, 42 previews, and 168 extracted sprites.
- Full cutout manifest contains 168 lines.

Cleanup performed:
- Generated image originals were left in Codex's generated image cache as required.
- Project-bound copies are stored in the Garden output folder.
- No runtime source files were changed for this completion pass.

Risks:
- Generated plant art still needs species-by-species visual approval before installation.
- The cutout process is automated; a few dense dried bundles may still need hand-tuning if QA finds small cyan edge flecks.

Memory-worthy notes:
- Complete plant production art batch exists for all 21 current crop definitions.
- The eight-stage plant production layout is now established for generated candidate sheets.

Do not promote to memory:
- Specific generated sprite choices until the user approves the visual style.

Next recommended gate:
- Review the dark/light previews, then choose whether to wire the sprites into plot growth, raw bin, drying rack, and dry bin rendering.

## Addendum: Plant Sprite Cyan QC Cleanup Pass

Task:
- Run a quality-control cleanup pass across all generated herb/plant production assets before runtime wiring.
- Specifically check for interior cyan blotches and off-cyan edge tints.

Result:
- All 21 plant sheets were rebuilt from the generated cyan sources.
- All 168 extracted transparent plant sprites were regenerated.
- Dark, light, and magenta previews were regenerated.
- QC contact sheets and metrics were written under `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\plant-production-sprite-prompts\qc`.

Cleanup process:
- Removed exact cyan and strong key cyan globally, including interior holes between leaves.
- Removed edge-connected off-cyan background tones.
- Applied an additional edge despill pass so remaining cyan-blue fringe is shifted out of sprite edges without deleting legitimate herb pigments such as rue's blue-green leaves.

Final QC metrics across all 168 extracted sprites:
- Exact cyan: 0
- Strong key cyan: 0
- Edge key cyan: 0
- Weak teal-or-cyan colour pixels: 11912, retained as legitimate plant colour rather than key background.

Files touched:
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\plant-production-sprite-prompts\cutout-sheets\`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\plant-production-sprite-prompts\cutout-cells\`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\plant-production-sprite-prompts\previews\`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\plant-production-sprite-prompts\qc\`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\plant-production-sprite-prompts-qc-clean-2026-05-16.zip`

Checks run:
- Count check confirmed 21 source sheets, 21 cutout sheets, 168 extracted sprites, and 63 preview sheets.
- QC metrics confirmed zero exact/strong/edge key cyan in the extracted sprites.
- Visual contact sheet review checked `qc/contact-magenta.png` and `qc/contact-dark.png`.

Cleanup performed:
- Temporary rue cleanup test images were removed.
- Generated image originals remain in Codex's generated image cache as required.

Risks:
- Some plant species intentionally use blue-green/teal pigments; those are retained and may still appear in broad colour metrics.
- Final art approval is still needed before runtime installation.

Memory-worthy notes:
- The QC-clean package should supersede the earlier complete package for plant runtime wiring.

Do not promote to memory:
- Specific generated sprite choices until the user approves the visual style.

Next recommended gate:
- Use the QC-clean package for the plant sprite runtime wiring pass, not the earlier complete zip.
