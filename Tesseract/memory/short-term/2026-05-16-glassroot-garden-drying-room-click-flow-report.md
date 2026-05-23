# 2026-05-16 Glassroot Garden Drying Room Click Flow Report

## Task
Make the herbalist drying room support direct click flow: raw plants click into an empty drying rack slot, and ready dried rack bundles click into the dried plant bin if storage space is available.

## Result
Complete. Raw bin stacks already routed through the rack path; this pass confirmed and preserved that path, added clickable occupied rack slots, and changed drying-rack auto collection so ready herbs remain manually collectable while the storage room is open.

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`

## Checks Run
- `npm run build` passed.
- Browser-flow test passed with seeded Basil:
  - clicked raw Basil stack into drying rack slot 0;
  - forced drying ready for test;
  - clicked ready rack bundle into dried bin slot 0;
  - no page errors reported.

## Cleanup Performed
No temporary files were created.

## Risks
- Drying rack auto-collection still runs when the storage room is closed, so away-from-room automation continues. While the room is open, collection is player-click driven.

## Memory-Worthy Notes
- Ready drying rack bundles are now manually collectable in the storage room.
- Plant bin storage now fills across compatible/empty slots instead of stopping after a single partially full slot.

## Next Recommended Gate
Live browser review: open the herbalist room, click a raw stack onto the rack, wait or force-ready during testing, then click the dried bundle into the dried bin.
