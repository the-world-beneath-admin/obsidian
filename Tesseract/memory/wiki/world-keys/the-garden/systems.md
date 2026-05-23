# The Garden Systems

## Current Core Loop

The local prototype loop is:

1. Plant seeds in garden plots.
2. Perform optional Companion work windows where available.
3. Harvest plants.
4. Route normal harvests into raw bins or failed harvests into compost feedstock.
5. Dry raw plants in batches of 5.
6. Move finished drying batches to dried bins when space exists.
7. Load dried plants into Bundler recipes.
8. Complete one-off Notice Board bundles for XP, rewards, and board credit.
9. Complete Transfer Bundles into World Key shared storage without XP.

## Companion Automation

Companions can till, fetch seed, plant, handle optional work windows, harvest, and deliver outputs. The current UX direction is to keep Companion terminology clear and player-facing.

## Notice Board And Bundles

Notice Board quest bundles are one-off orders: once a quest bundle is queued or completed, duplicate production should stay blocked until a future design explicitly reopens it. The visible labels should move through `Open`, `Awaiting completion`, and `Complete`.

Transfer Bundles remain repeatable and are the normal route into World Key shared storage.

The 2026-05-17 lifecycle hardening pass verified this separation on a clean browser save with practical save/reload checks. No source changes were required.

The 2026-05-18 catalog pass moved Notice Board and Transfer Bundle definitions into `src/data/bundleCatalog.ts`. Generated Notice Board orders now total 500, with 100 orders per tier. Each generated order uses exactly 3 distinct plant inputs with varied quantities. Expired Notice Board orders refill after a randomized 1-3 minute delay.

Current open risk: future daily/rotating Notice Board orders need a new order lifecycle. Do not remove the duplicate-order guard to make repeatable daily orders; design a proper rotation/reopen path instead.

## Pet Selector / Companion Area

The live scene now uses the work-board style starter-pet selector in the previously approved wall area. Chuck, Peggy, and Stanly are wired into the selector and roaming companion sprites. The older three circular slot markers are superseded.

The selector source/candidate remains preserved under:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\pet-selector-plaque-01\
```

Future selector work should tune alignment, scale, or hit areas narrowly from the installed baseline rather than resuming the old interrupted half-install.

## Storage And Workbench

The storage/workbench area now uses an image-backed Herbalist Workbench room direction: basement brick/floor backdrop, wooden work table, wall-mounted drying rack, ornate Notice Board, and image-backed raw/dried plant storage panels. Raw/dried bins are scrollable, capped at 999 units each, and no longer expose whole-bin compost controls.

The cards should preserve the source art aspect ratio, keep text readable, and avoid footer/header overlap. If larger labels are wanted later, the right fix is a taller or wider panel rather than another squeeze pass.

The 2026-05-19 mobile/touch review found portrait-phone Scale.FIT makes the image-backed Workbench too small. Current direction is to require or guide players into landscape for this room rather than forcing another cramped portrait squeeze pass.

The finished-bundles rack/package art is wired into the Storage Hut, but the v6 bundling-machine runtime art failed visual QA. The failure is a composition-contract problem: independently generated machine parts did not preserve shared anchors, sockets, stable runtime footprint, or non-overlap during motion. Treat v6 as failed reference evidence until reviewed. The next bundling-machine pass should use smaller modules with strict sockets or simpler procedural animation instead of one large brittle animated machine prompt.

## Garden Pets And Achievements

Garden achievement UI/scaffolding and Garden pet board/roster/stamina/subskill scaffolding were advanced in the 2026-05-19 worker pass. Garden pet subskills must remain World-Key-specific and separate from main-game pet stats and balance.

Platform client integration now includes Garden pet catalog/account-owned pet fallback surfaces, but authoritative website/platform ownership and production sync remain shared-platform work. Garden should keep local fallback compatibility with the existing `companionCards` shape until the platform read/purchase APIs are fully reviewed and approved.

## Seed Bag And Plot UI

The live seed bag now uses the cleaned alpha crop set as image-backed UI instead of placeholder rectangles.

Seed-stage markers now prefer the real `seed-planted` sprite, with the decorative dot only as a fallback.

Growing timers belong in the plot info panel instead of floating over the bed.

The 2-column tier-tab seed bag layout is the preferred direction over dense paging.

Plant sprites should stay anchored to the soil-centre so badges and art do not fight each other.

Drying-room occupied slots can be inspected while drying and manually collected when ready while the room is open.

## Compost

Compost has curing/feedstock and ready states. Curing compost converts into ready compost at 1 unit per 15 seconds.

Comfreygrass is the free compost filler crop. It grows for 120 seconds, costs no ready compost, and harvests into 5 curing compost.

## Progression

Normal crop growth timing increases by tier:

- T1: 60 seconds
- T2: 90 seconds
- T3: 120 seconds
- T4: 180 seconds
- T5: 240 seconds

Current unlock thresholds:

- T2: 200 T1 XP/units
- T3: 500 T2 XP/units
- T4: 1000 T3 XP/units
- T5: 10000 T4 XP/units

## Technical Warning

Most prototype logic is concentrated in `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`. This is useful for fast iteration but increases regression, merge, and readability risk.

Plot child visuals should be created hidden and shown only through `refreshPlot()`. This prevents startup errors before `refreshAllPlots()` from leaving default plant shapes and blue work bars visible on every plot.

## Sources

- [[short-term/2026-05-12-glassroot-garden-working-window-intake]]
- [[short-term/2026-05-16-garden-worker-final-decommission-report]]
- [[short-term/2026-05-16-glassroot-garden-visual-artifact-pet-selector-report]]
- [[short-term/2026-05-16-glassroot-garden-starter-pets-selector-wiring-report]]
- [[short-term/2026-05-16-glassroot-garden-mobile-storage-card-ui-intake]]
- [[short-term/2026-05-16-glassroot-garden-mobile-storage-cards-assets-report]]
- [[short-term/2026-05-16-glassroot-garden-storage-card-refit-report]]
- [[short-term/2026-05-16-glassroot-garden-storage-card-lineup-pass-report]]
- [[short-term/2026-05-17-garden-worker-final-decommission-report]]
- [[short-term/2026-05-17-glassroot-garden-notice-board-lifecycle-hardening-report]]
- [[short-term/2026-05-18-glassroot-garden-worker-report]]
- [[short-term/2026-05-19-glassroot-garden-worker-final-decommission-report]]
