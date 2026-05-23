# Magitech Farming Work Stages Implementation Plan

## Design Rule

The required loop is automated by Companions:

1. Player chooses a seed and target plot.
2. Companion tills the soil.
3. Companion fetches the seed from the tool shed.
4. Companion plants the crop.
5. Crop grows on a timer.
6. Companion harvests the ready crop and carries it to storage.

The optional loop is player-timed:

1. During crop growth, optional work windows appear.
2. Player clicks the crop during an open window.
3. A Companion queues the matching work.
4. Success adds yield bonus.
5. Failure adds yield penalty.

## Plot States

- `untilled`: Empty plot, cannot accept a crop yet.
- `tilling`: Companion is preparing soil.
- `tilled`: Plot is prepared and can be planted.
- `planting`: Companion is fetching/planting seed.
- `growing`: Crop is growing and optional windows may appear.
- `ready`: Crop is mature and waiting for automated harvest.
- `harvesting`: Companion is collecting and carrying the crop to storage.

## Step-By-Step Build Plan

1. [x] Add plot work-stage fields and queued crop metadata.
2. [x] Change seed drop so it queues required Companion work instead of planting instantly.
3. [x] Implement automated required sequence: till soil -> fetch seed -> plant crop.
4. [x] Add automatic ready-crop harvesting by available Companions.
5. [x] Add yield tracking fields: base yield, bonus count, penalty count, final quality.
6. [x] Add optional work-window definitions during the growth timer.
7. [x] Let player click a growing crop during an open optional window to queue Companion work.
8. [x] Resolve optional task success/failure from Companion focus/stats later; use simple chance for wireframe.
9. [x] Show optional window state visually on the plot.
10. [x] Resolve final harvest rewards from yield score and quality.

Current progress: 10/10 completed. Core magitech farming work-stage loop is complete.

## Current Implementation Target

Steps 1-10 are complete. The core work-stage loop is now implemented:

- Required loop is automated.
- Seed drop still starts the process.
- Pets perform visible tilling, tool-shed pickup, planting, and harvesting.
- Yield scoring exists and harvest rewards resolve through quality.
- Optional windows are computed from crop growth progress and shown in plot info.
- Clicking a crop during an open optional window queues a Companion to fetch the right material/tool and perform placeholder work at the plot.
- Optional work resolves as success or failure using a simple Companion chance roll.
- Success adds yield bonus; failure adds yield penalty.
- Plot badges now show upcoming, open, queued, missed, and scored optional work states.
- Final harvest rewards resolve from base crop value, yield score, and quality multiplier.
- Next build direction: tune timings/odds, improve visible feedback, and connect this loop to real backend persistence.
