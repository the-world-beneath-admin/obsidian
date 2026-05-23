# The Garden Testing

## Current Test Commands

Run from `C:\Users\yrred\Desktop\Unity\TWB-Farming`.

- Start dev server: `npm run dev`
- Browser URL: `http://127.0.0.1:5173/`
- Required build check after code changes: `npm run build`

## Confirmed Checks From Intake

- `npm run build` passed after recent code changes. The Vite large Phaser chunk warning appeared and is expected for now.
- 2026-05-16 tool shed door animation check confirmed the installed sheet opens during fetch actions and closes after departure.
- Headless browser smoke testing verified Comfreygrass planting from the seed bag.
- Comfreygrass selection text showed it is free, grows for 2 minutes, and harvests into 5 curing compost.
- Planting Comfreygrass kept ready compost at 0 and queued/planted normally.
- Forced-ready Comfreygrass harvest produced 5 curing compost, kept raw total at 0, and put the plot into harvest lockdown.
- Dev server rebooted with `npm run dev`, and `http://127.0.0.1:5173/` returned HTTP 200.
- Earlier debug/browser audit covered planting, raw-to-drying-to-dried, Notice Board XP/tokens, transfer storage without XP, failed harvest compost, compost conversion, tier unlock, save/reload, and Comfreygrass compost routing.
- 2026-05-12 fresh full-loop playtest (worker report): normal basil planting, optional work, harvest, raw storage, drying to dried bins, bundling, Notice Board contract, transfer bundle, bin clean-out, Comfreygrass compost, and ready compost conversion. Notice Board produced `tokens +18`, `board completion +1`, `Notice Board XP +2.25`, and transfer bundle added shared storage with no token/XP delta. 
- 2026-05-16 checks confirmed starter-pet walk-sheet wiring, slower roaming with plot-work-only labels, and the retimed herbalist door plus right-side plaque placement.
- 2026-05-16 checks confirmed all 5 well tiers and all 5 compost tiers are wired, tiered compost-fill mounds exist, the cyan-matte seed bag UI source set is generated but not yet installed, drying-room raw-to-rack and rack-to-bin click flow works, the 21 crop plant folders are wired with seed carry/drop planting, and the storage card lineup/refit passes kept the raw/dried cards compact and readable.

## Current Validation Status

- 2026-05-15 checks confirmed the corrected 12-plot `4 x 3` layout, the installed tier 1 well and compost assets, the lantern-free store entry swap, and the cleanup of utility-area mockup blotches.
- 2026-05-16 decommission report says `npm run build` passed after rolling back the interrupted pet selector board install.
- Local dev server was reachable at `http://127.0.0.1:5173/` during plaque verification.
- Clean Playwright verification after rollback showed the tool shed and herbalist hut plaques visible again.
- User browser state showed a separate plant/bar artifact over all 12 plots; clean Playwright did not reproduce it, so the next validation must account for local save/browser state.
- 2026-05-16 checks confirmed starter-pet walk-sheet wiring, slower roaming with plot-work-only labels, the retimed herbalist door plus right-side plaque placement, the image-backed seed bag UI, real seed markers, plot timer relocation into the info panel, tier tabs, and drying-room click flow.
- 2026-05-17 checks confirmed Notice Board quest bundles block duplicates after the first completion while Transfer Bundles remain repeatable into shared storage.
- 2026-05-17 final decommission confirms the local dev server returned HTTP `200`, `npm run build` passed after the Notice Board duplicate-order guard, and the focused Playwright check verified Greenward Order duplicate blocking while `transfer_basil` remained repeatable.
- 2026-05-17 Notice Board lifecycle hardening passed with no source changes. Clean/browser checks confirmed `Open` -> `Awaiting completion` -> `Complete`, duplicate Notice Board production blocked while awaiting and completed, Transfer Bundles remained repeatable, save/reload checks passed, dev server returned HTTP `200`, and the finished rack was readable at `1280 x 720`.
- 2026-05-18 Herbalist Workbench / Storage Hut presentation pass: `npm run build` passed with the known Vite large chunk warning. Node audits over `src/data/bundleCatalog.ts` found 500 generated notice orders with 0 failures, and each order had 3 inputs, 3 distinct plants, and 3 distinct quantities. Legacy scene notice recipes also passed the same distinct-input audit. Manual Playwright/Chromium visual checks covered `1280 x 720` workbench composition, Notice Board fit/card text, storage-bin card/button/icon fit, and populated bin/Notice Board views.
- 2026-05-19 Garden worker decommission: focused mobile/touch review found portrait-phone Scale.FIT makes the image-backed Herbalist Workbench too small; current direction is landscape support/requirement rather than another squeeze pass. `npm run build` passed with the known Vite large chunk warning, browser smoke at `http://127.0.0.1:5173/` loaded, and the Workbench could be entered.
- 2026-05-19 bundling-machine visual QA failed after v6 runtime sheet processing/wiring. The moving press/clamp detached from the arms/base because the pieces did not share stable anchors or one compositional contract. This should be treated as an asset-pipeline failure, not a simple scale/position bug.

## Next Gate
- Current gate: bundling-machine-only restart. Inspect whether the failed v6 runtime machine is visible in-app; hide/revert that presentation path if needed; then produce a stricter modular asset/prompt contract informed by the SLYNYRD and external pixel-art resources before more code or art iteration. Keep Notice Board lifecycle unchanged unless a reproducible bug appears, and keep Transfer Bundle repeatability intact.

## Production Risks

- `window.__glassrootDebug` helpers are useful for testing but should be gated or removed before production.
- There is no formal automated regression suite yet.
- Player comprehension is not validated; tutorial/onboarding is still missing.

## Sources

- [[short-term/2026-05-12-glassroot-garden-working-window-intake]]
- [[short-term/2026-05-16-garden-worker-final-decommission-report]]
- [[short-term/2026-05-16-glassroot-garden-tier-check-seed-bag-ui-report]]
- [[short-term/2026-05-16-glassroot-garden-drying-room-click-flow-report]]
- [[short-term/2026-05-16-glassroot-garden-herb-sprite-wiring-report]]
- [[short-term/2026-05-16-glassroot-garden-mobile-storage-card-ui-intake]]
- [[short-term/2026-05-16-glassroot-garden-mobile-storage-cards-assets-report]]
- [[short-term/2026-05-16-glassroot-garden-storage-card-refit-report]]
- [[short-term/2026-05-16-glassroot-garden-storage-card-lineup-pass-report]]
- [[short-term/2026-05-17-garden-worker-final-decommission-report]]
- [[short-term/2026-05-17-glassroot-garden-notice-board-lifecycle-hardening-report]]
- [[short-term/2026-05-18-glassroot-garden-worker-report]]
- [[short-term/2026-05-19-glassroot-garden-worker-final-decommission-report]]
