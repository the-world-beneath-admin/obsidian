# 2026-05-16 Glassroot Garden Mobile Storage Card UI Intake

## Task

Intake the user's mobile usability correction for the herb drying room before creating more assets.

Scope: Glassroot Garden World Key.

## User Direction

The raw plant bins and dried plant bins should not remain tiny slot grids. They should become scrollable, clickable card-summary lists so they are usable on a cell phone.

Raw plant cards should add plants to the drying rack.

Dried plant cards should add dried plants to the bundling/packing machine.

## Result

Updated:

`C:\Users\yrred\Desktop\Unity\TWB-Farming\Herbalist_Drying_Room_Asset_Measurements_And_Creation_Plan.md`

Added:

`Raw And Dried Plant Storage - Mobile-First Card Revision`

The old `5 x 3` small slot grid is now marked as legacy measurement reference, not the preferred target for new assets.

## New Measured Layout

The revised storage UI still fits inside the existing lower-left module footprint:

- Overall storage module: `x=57 y=367 w=472 h=230`.
- Raw plant list panel: `x=67 y=384 w=220 h=202`.
- Dried plant list panel: `x=299 y=384 w=220 h=202`.
- Scroll viewport: `x=panelX+12 y=panelY+42 w=196 h=144`.
- Plant summary card: `w=196 h=44`.
- Three visible cards per list, with `6 px` vertical gap.
- Card icon well: `32 x 32`.
- Card action/count chip: `44 x 26`.

## Interaction Rule

- Tap raw plant card: add one item to the first available drying rack slot, or show no-space feedback.
- Tap dried plant card: add one item to the current bundling-machine input, or show no-recipe/no-space feedback.
- Compost/discard should be a deliberate secondary control, not the whole-card action.
- The card list should support wheel/drag on desktop and vertical swipe on mobile.

## Asset Plan Change

The next candidate package should use 9 raw/dried card-list assets instead of the previous 6 grid-bin assets:

1. Raw storage card-list panel, `220 x 202`.
2. Dried storage card-list panel, `220 x 202`.
3. Plant summary card normal, `196 x 44`.
4. Plant summary card hover/focus, `196 x 44`.
5. Plant summary card pressed/selected, `196 x 44`.
6. Plant summary card disabled/empty, `196 x 44`.
7. Card action/count chip, `44 x 26`.
8. Scroll rail, `4 x 144`.
9. Scroll thumb, `4 x 36`.

## Risks

- If the old grid-bin art is installed, the room will still be awkward on phone-sized touch screens.
- The card layout needs runtime scroll behavior, not just replacement art.
- Text should remain runtime-rendered for readability; do not bake plant names/counts into card art.

## Memory-Worthy Notes

- The herb drying room storage bins should be mobile-first card summaries, not tiny slot grids.
- Raw card tap sends the plant to the drying rack.
- Dried card tap sends the plant to the bundling/packing machine.
- The current small slot-grid assets are superseded unless explicitly restored.

## Do Not Promote Yet

- Do not promote exact final art style from this note; this is a layout and interaction decision, not final visual approval.

## Mini Handoff For Orchestrator

User corrected the herb drying room storage UX before asset creation: raw and dried plant bins should be scrollable card-summary lists for mobile usability, not tiny inventory slots. The plan now fits two `220 x 202` card panels into the existing lower-left `472 x 230` storage area, with `196 x 44` cards. Raw card taps should add to the drying rack; dried card taps should add to the packing machine. Please treat the old small grid-bin assets as superseded unless the user deliberately rolls that back.
