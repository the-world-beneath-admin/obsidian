# Storage Workbench Bin Module Refinement Plan

## Goal

Refine the storage workbench screen so the lower workbench modules fit the marked layout:

- raw/dried plant bins in the left pink target area,
- finished bundles in the right green target area,
- processing surface filling the space between them.

The screen should read as a tabletop workbench / archaic alchemical machine, not as giant shelves inside a room.

## Requirements

### Left Module: Raw And Dried Plant Bins

- Resize and reposition the left module into the pink target area.
- Make it slightly wider than the current raw-only module.
- Split it into two labeled sections:
  - `RAW PLANT BINS`
  - `DRIED PLANT BINS`
- Each section should have 15 visible slots.
- Slots should look like old milk-bottle crate compartments:
  - small square/cubby openings,
  - rigid grid dividers,
  - product appears inside the slot when present,
  - not shelves holding baskets.
- Raw counts still come from existing harvest storage.
- Dried counts are placeholder-zero for now until processing is built.

### Right Module: Finished Bundles

- Resize and reposition into the green target area.
- Keep it visually related to the left module but narrower.
- Make it feel like compact finished-output cubbies/trays, not a standing shelf.
- Keep placeholder finished bundles for now.

### Center Module: Processing Surface

- Expand the processing surface to fill the remaining workbench space between left and right modules.
- Keep it as a placeholder alchemical processing surface / work area.
- It should feel centered between intake bins and output bundles.

## Implementation Steps

1. Add a small helper for drawing slotted crate grids.
2. Replace the raw shelf drawing with a two-section slotted crate:
   - 15 raw slots,
   - 15 dried slots.
3. Replace the finished bundle shelf with a compact slotted output crate in the right target area.
4. Resize and reposition the processing surface so it fills the center workbench area between those modules.
5. Run `npm run build`.
6. Refresh the browser and verify:
   - left bins sit in the pink target area,
   - right bundles sit in the green target area,
   - center processing surface fills the gap,
   - no console errors.

## Notes

This is a layout and visual-metaphor pass. It does not add real drying or bundling gameplay yet. The raw inventory cap and harvest-to-bin behavior must remain intact.
