# Next Phase Plan: Magitech Processing Machine, Bundles, Contracts, XP, And Storage

## Intent

The Storage Hut workbench becomes the main processing station for the farming World Key. The player grows plants, pets harvest them into raw bins, raw plants are dried, dried plants are dropped into a magitech bundling machine, and finished bundles are either sent to a Notice Board request or stored in account-level World Key storage.

This phase is larger than a visual pass. It introduces a new economy loop, level gating, contract fulfillment, and overflow handling.

## Current Understanding

### Recipe Selection And Bundle Intent

- The player chooses the bundle target before using the processing machine.
- The Notice Board can provide two kinds of targets:
  - normal Notice Board recipe bundles,
  - transfer bundles for shared/account-level World Key storage.
- Whatever target is selected on the board becomes the active machine recipe.
- The active recipe is shown beside/on the machine before the player loads materials.
- The player must drop the required dried materials into the machine in the listed order to lock the recipe in place.
- Recipe amounts must vary. Avoid `1 + 1 + 1 = 1` recipes.

### Processing Surface

- Replace the current simple processing surface with a magitech machine.
- The machine should roughly follow the green shape drawn in the screenshot:
  - wider base/body,
  - funnel or chute at the top where dried plants are dropped in,
  - central glowing/rotating magitech mechanism,
  - side button/lever.
- The player drops dried plants into the machine based on the selected recipe.
- The machine verifies the order and required amounts as materials are dropped.
- Pressing the button consumes the loaded dried plants in that same order and amount.
- The machine creates a finished bundle from the selected recipe.

### Bundle Composition

- There are two bundle categories:
  - Notice Board bundles,
  - Shared World Key transfer bundles.
- Notice Board bundles are mixed recipe bundles made from 3 plant entries.
- Notice Board bundle order matters.
- Notice Board recipes use varied material counts, for example:
  - 4 Basil
  - 3 Sage
  - 2 Yarrow
- Transfer bundles are not mixed-product bundles.
- Transfer bundles condense 10 units of one dried plant into 1 shared-storage bundle.
- Example transfer bundle:
  - 10 dried Basil -> 1 Basil Transfer Bundle.
- This creates a bundle record with:
  - recipe ID,
  - ordered plant IDs and amounts,
  - destination type,
  - plant tiers,
  - creation time,
  - destination state.

### Finished Bundles Area

- Each basket/bin in the finished bundles rack holds exactly 1 finished bundle.
- When a bundle is placed there, it starts a 2-minute processing timer.
- The choice is made before the timer starts by selecting either a Notice Board recipe or a Transfer Bundle recipe.
- When the timer completes:
  - a Notice Board bundle is consumed by its matching selected Notice Board contract,
  - a Transfer Bundle is moved into account-level World Key storage for later use by other World Keys.

### Notice Board

- Notice Board requests are generated randomly.
- Each request asks for a bundle recipe with 3 ordered plant entries.
- Each entry can require more than 1 dried plant.
- The reward is based on the selected plants.
- Requests should respect the plant tier system and the player’s level/progression.
- Sending finished bundles to Notice Board requests gives the player an extra XP reward.
- A `Transfer Bundle` button lives at the top right of the Notice Board.
- Clicking it opens a small selection window where the player chooses which single-plant transfer bundle to make.

### World Key Storage

- Finished bundles can be stored for broader account-level World Key use.
- Shared-storage transfer bundles use exactly 10 dried units of one plant.
- Sending bundles to account-level World Key storage does not grant the extra Notice Board XP.
- These bundles should eventually live in the Cloudflare/account inventory system, not only local game state.

### Plant Tiers And Leveling

- Plants will be broken into 5 tiers.
- The player must level up to plant higher-tier plants.
- XP sources:
  - harvesting plants,
  - sending finished bundles to Notice Board requests.
- Bundles sent only to account-level World Key storage do not grant the second XP batch.

### Raw Bin Limits And Overflow

- Raw bins hold a maximum of 99 per bin.
- There are intentionally not enough raw bin slots for every plant type at once.
- This creates inventory pressure:
  - if a harvested plant has an existing bin with room, it goes there,
  - if the plant does not have a bin but an empty bin slot is available, it claims a slot,
  - if no valid bin slot is available, the harvest goes to the compost heap instead.
- Compost accumulates up to 999.
- Any compost above 999 disappears.

## Proposed Data Model

### Plant Definitions

Each plant should have:

- `id`
- `name`
- `tier`
- `baseHarvestXp`
- `baseRewardValue`
- `tags`
- `dryingTimeMs`
- `bundleValue`

### Raw Bin Slot

```ts
interface PlantBinSlot {
  cropId: string | null;
  count: number;
}
```

Rules:

- 15 raw slots.
- Each occupied slot is locked to one plant type until emptied.
- Count is capped at 99.

### Dried Bin Slot

```ts
interface DriedPlantBinSlot {
  cropId: string | null;
  count: number;
}
```

Rules:

- 15 dried slots.
- Each occupied slot is locked to one plant type until emptied.
- Count is capped at 99.

### Processing Machine State

```ts
interface ProcessingMachineState {
  selectedRecipeId: string | null;
  loadedEntries: Array<{
    cropId: string;
    amount: number;
  }>;
  isProcessing: boolean;
}
```

Rules:

- The selected recipe determines the required ordered entries.
- Load order is preserved.
- Notice Board recipes use 3 ordered entries with varied counts.
- Transfer recipes use 1 entry of 10 dried units.
- Button becomes active only when the loaded entries match the selected recipe.

### Processing Recipe

```ts
interface ProcessingRecipe {
  recipeId: string;
  kind: "noticeBoard" | "worldKeyTransfer";
  requiredEntries: Array<{
    cropId: string;
    amount: number;
  }>;
  rewardTokens: number;
  rewardXp: number;
}
```

### Finished Bundle

```ts
interface FinishedBundle {
  bundleId: string;
  recipeId: string;
  kind: "noticeBoard" | "worldKeyTransfer";
  plantEntriesInOrder: Array<{
    cropId: string;
    amount: number;
  }>;
  createdAt: number;
  processingReadyAt: number;
  destination: "noticeBoard" | "worldKeyStorage";
  matchedContractId: string | null;
}
```

### Finished Bundle Slot

```ts
interface FinishedBundleSlot {
  bundle: FinishedBundle | null;
}
```

Rules:

- One bundle per slot.
- Existing visual rack currently has 9 baskets, so start with 9 slots unless changed.
- Each filled slot shows a 2-minute timer.

### Notice Board Request

```ts
interface NoticeBoardRequest {
  requestId: string;
  requiredEntriesInOrder: Array<{
    cropId: string;
    amount: number;
  }>;
  tierRange: [number, number];
  rewardTokens: number;
  rewardXp: number;
  expiresAt: number | null;
}
```

Rules:

- Requests use 3 plant entries with varied required amounts.
- Order matters unless we later decide contracts should accept unordered bundles.
- Rewards scale by plant tier and rarity/value.

### Player Progression

```ts
interface GardenProgression {
  level: number;
  xp: number;
  unlockedPlantTier: 1 | 2 | 3 | 4 | 5;
}
```

Rules:

- Harvest gives base XP.
- Notice Board fulfillment gives additional XP.
- World Key storage transfer gives no Notice Board XP bonus.

### Compost

```ts
interface CompostState {
  amount: number;
}
```

Rules:

- Cap: 999.
- Overflow above 999 disappears.
- Harvests that cannot fit in raw bins are converted into compost.

## Proposed Gameplay Flow

### Harvest To Raw Bins

1. Pet harvests a crop.
2. Game checks raw bin slots.
3. If matching crop slot has room, add harvest there.
4. If no matching slot exists but an empty slot exists, assign that slot to the crop and add harvest.
5. If matching slot is full or all slots are occupied, send harvest to compost.
6. Add harvest XP.

### Raw To Dried

This needs a design decision.

Possible MVP path:

1. Player clicks a raw bin.
2. Player sends raw plants to drying rack.
3. Drying rack runs a timer.
4. Finished dried plants move into dried bins.

### Dried To Bundle

1. Player selects a Notice Board recipe or Transfer Bundle recipe first.
2. The selected recipe appears at the machine.
3. Player drags dried plants from dried bins into the machine funnel in the required order.
4. Machine records order and required quantity for each entry.
5. Once the loaded entries match the selected recipe, the button activates.
6. Player presses button.
7. Machine consumes the required dried plant amounts.
8. Machine creates the selected finished bundle.
9. Bundle is placed into the next available finished bundle basket.
10. Basket starts a 2-minute timer.

### Bundle Resolution

1. Bundle timer completes.
2. If it was created for a Notice Board contract, consume bundle and award:
   - tokens,
   - Notice Board XP.
3. If it was created as a Transfer Bundle, move it to account-level World Key storage.
4. World Key storage transfer gives no Notice Board XP bonus.

## Implementation Phases

### Phase 1: Notes And State Foundations

- Save this plan.
- Add model definitions for:
  - raw bin slots,
  - dried bin slots,
  - processing machine state,
  - finished bundle slots,
  - notice board requests,
  - progression,
  - compost.
- Do not wire full backend yet.

### Phase 2: Raw Bin Slot Rules

- Replace current map-style raw storage with 15 explicit raw bin slots.
- Add 99-per-bin cap.
- Add overflow-to-compost behavior.
- Update harvest delivery text to report:
  - stored in raw bin,
  - assigned to new raw bin,
  - sent to compost.

### Phase 3: Dried Bin And Drying Flow

- Add 15 dried bin slots.
- Decide and implement how raw plants become dried plants.
- Likely MVP:
  - click raw bin,
  - click `Send to Drying Rack`,
  - timer completes,
  - dried bin receives plant.

### Phase 4: Magitech Machine UI

- Replace processing surface placeholder with a machine matching the green sketch:
  - funnel,
  - central alchemical chamber,
  - glowing mechanism,
  - side button.
- Add selected recipe display.
- Add visible load queue that adapts to:
  - 3-entry Notice Board recipes,
  - 1-entry Transfer recipes.
- Add drag/drop from dried bins into funnel.

### Phase 5: Bundle Creation

- Pressing the machine button consumes the selected recipe's dried plant requirements in order.
- Create either a Notice Board bundle or Transfer Bundle based on the selected target.
- Place it into a finished bundle rack slot if available.
- If no finished bundle slot is available, block the action with a message.

### Phase 6: Finished Bundle Timers

- Each finished bundle slot holds one bundle.
- Each filled slot shows a 2-minute timer.
- Timer completion changes bundle state to ready for:
  - Notice Board fulfillment,
  - or World Key storage transfer.

### Phase 7: Notice Board Contracts

- Generate random 3-plant requests.
- Add `Transfer Bundle` selector button.
- Select active request.
- Match completed bundles by ordered plant IDs and amounts.
- Award tokens and Notice Board XP.

### Phase 8: Player Leveling And Tiers

- Assign all plants to 5 tiers.
- Add XP and level thresholds.
- Gate planting by unlocked tier.
- Show locked higher-tier seeds in the seed bag.

### Phase 9: Account-Level World Key Storage

- Define local placeholder first.
- Later connect to Cloudflare/platform inventory:
  - bundle records,
  - account ownership,
  - world-key storage namespace.

## Clarifying Questions

1. Should the 3-plant bundle order matter for Notice Board contracts, or should the same 3 plants count regardless of order?

2. Should raw plants dry automatically over time once placed on the drying rack, or should pets perform the drying step?

3. Should raw-to-dried conversion be 1:1, or should some plants lose quantity during drying?

4. Do finished bundle slots stay at 9 baskets, matching the current rack, or should we support more later?

5. When a finished bundle timer completes and no Notice Board request is selected, should it automatically go to World Key storage, or wait for the player to choose?

6. Should overflow compost from failed bin storage give any small XP/token consolation, or no reward beyond compost?

7. Do we want tiers assigned by real-world/commonness/folklore danger, or by gameplay pacing only?

8. Should the raw bin slot stay assigned to a plant when it reaches 0, or should it become empty and reusable immediately?

## Recommended Answers For MVP

- Bundle order should matter because you specifically called it out.
- Raw-to-dried should start as a simple click/timer flow, pets can be added later.
- Raw-to-dried should be 1:1 for MVP.
- Keep 9 finished bundle baskets for now.
- Completed bundles should wait for player choice unless a contract is selected and matches.
- Overflow compost should not grant tokens, but harvest XP should still be granted because the plant was successfully harvested.
- Tiering should be gameplay-first, with lore used to justify placement.
- Raw bin slots should clear when they reach 0 so the inventory pressure stays understandable.
