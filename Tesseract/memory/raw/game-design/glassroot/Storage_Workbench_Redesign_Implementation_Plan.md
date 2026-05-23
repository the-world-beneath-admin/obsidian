# Storage Workbench Redesign Implementation Plan

## Goal

Convert the Storage Hut screen from a full-room layout into a focused 2D workbench / archaic alchemical processing station. The screen should feel like one large, functional station rather than a hut interior full of oversized shelves.

## Design Intent

- The whole screen reads as a compact herbalist/alchemical workstation.
- The lower half becomes a broad workbench or machine table.
- Raw plant bins and finished bundles become smaller tabletop modules.
- The drying rack hangs on the back wall, not floating as a giant room fixture.
- The right side of the back wall gets an empty notice board for future tasks, recipes, or processing notes.
- The layout keeps the existing functional positions readable while making the objects feel properly scaled.

## Functional Requirements

- Keep the `Back to Garden` button.
- Keep raw storage count behavior:
  - raw material total is capped at 99.
  - bins only appear when that crop has raw materials.
  - harvested crops increment the correct raw bin.
- Keep finished bundle display placeholder.
- Keep drying rack placeholder art.
- Do not change crop growth, harvesting, pet movement, seed bag, or plot UI in this pass.

## Visual Layout

### Background

- Replace the current full-room floor-heavy look with:
  - dark back wall band,
  - lower tabletop/workbench platform,
  - subtle alchemical panel lines,
  - bronze/wood trim.

### Wall Area

- Left wall:
  - hanging drying rack with herbs.
  - smaller than current rack if needed.
  - visually attached to the wall.

- Right wall:
  - empty notice board.
  - simple framed board with no content for now.
  - reserved for future processing notes/recipes.

### Workbench Area

- A large horizontal workbench runs across the lower screen.
- Raw plant bins sit on or are embedded into the left side of the bench.
- Finished bundles sit on or are embedded into the right side of the bench.
- Center workbench area remains available for future processing controls.

## Implementation Chunks

### Chunk 1: Plan And Frame

- Save this markdown plan.
- Refactor `createStorageRoomOverlay()` so the background reads as wall + workbench.
- Remove the visual room-floor emphasis.
- Keep button centered at the bottom.

### Chunk 2: Wall Details

- Restyle `drawDryingRacks()` so it sits on the left side of the wall.
- Add a new `drawNoticeBoard()` helper for the right side of the wall.

### Chunk 3: Tabletop Modules

- Restyle `drawRawPlantBins()` so it appears as a compact tabletop raw-bin tray.
- Restyle `drawFinishedBundleShelves()` so it appears as a compact finished-bundle tray.
- Keep raw bin logic and 99 cap intact.

### Chunk 4: Verification

- Run `npm run build`.
- Open the local browser view.
- Check that:
  - storage screen opens,
  - no console errors appear,
  - back button works,
  - raw storage visuals still support empty/filled states.

## Notes

This should be a layout and style pass only. The processing system itself can come later once the workbench reads correctly.
