# Game Dev Quickref

## Current Direction

- Fact - The parent project is **The World Beneath**.
- Fact - The main Unity prototype source is `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`.
- Fact - The current seeded garden prototype should be marketed publicly as **The Garden**; **Glassroot Garden** is now an internal or historical prototype label.
- Fact - The first two planned free public World Keys are **The Garden** and **The Alchemy Lab**.
- Fact - Players name their own garden or lab when first opening those World Keys.
- Fact - Confirmed local build/test commands are recorded in [[build-test-commands]].
- Decision - Treat The World Beneath as the parent design authority and Glassroot Garden as a World Key subgame/module.
- Warning - Do not let Glassroot mechanics, SEO, or constraints overwrite main-game design decisions.
- Source: [[memory/raw/game-design/main-game/MASTER_BOOTSTRAP_STAGE_1_DOCS_v8]]
- Source: [[project-hierarchy]]
- Source: [[main-game-overview]]
- Source: [[memory/raw/game-design/glassroot/TWB_Glassroot_Garden_GPT_Pro_Research_Plan]]
- Source: [[memory/raw/game-design/glassroot/Full_Loop_Test_And_Implementation_Plan]]

## Important Constraints

- Decision - Main game memory and World Key memory must be kept distinct.
- Decision - Main-game tasks must state whether they touch main Unity systems, Glassroot, another World Key, or shared platform/account systems.
- Decision - MVP should stay focused. Do not start with a giant crafting economy, marketplace, generated story system, full NPC economy, weather simulation, open-world exploration, or direct main-game item rewards.
- Decision - The browser client must not be the reward authority. Planting, growth, harvest validation, Companion assignment, and token rewards need dedicated server-owned routes before live/public reward use.
- Warning - Companion Cards are not yet populated in the live platform database according to the research plan, so real Companion slotting depends on platform/import work.
- Warning - SaveVersion v9 is active for the main game and must not change without explicit authority.
- Source: [[memory/raw/game-design/main-game/TWB_SYSTEM_ARCHITECTURE_MAP]]
- Source: [[memory/raw/game-design/glassroot/TWB_Glassroot_Garden_GPT_Pro_Research_Plan]]

## Recent Decisions

- Decision - Main game is the parent project; Glassroot is a subgame.
- Decision - Use Phaser 3.90, TypeScript, and Vite for the browser prototype.
- Decision - Use Stardew-like angled top-down 2D rather than true 3D or full isometric for the first playable.
- Decision - Use Companions as the required automation layer for tilling, seed fetch, planting, and harvesting.
- Decision - World Key shared storage is separate from main-game inventory.
- Source: [[memory/wiki/decisions/design-decisions]]
- Source: `memory/raw/game-design/glassroot/package.json`
- Source: [[memory/raw/game-design/glassroot/Magitech_Farming_Work_Stages_Implementation_Plan]]
- Source: [[memory/raw/game-design/glassroot/Full_Loop_Test_And_Implementation_Plan]]

## Warnings

- Warning - Do not let client-side timers or generic inventory events mint harvest rewards.
- Warning - Do not make failures punishing in the MVP. Failure should delay, reduce bonus, or create mild mess, not destroy crops or permanently harm Companions.
- Warning - Keep plant references fictional and non-instructional; avoid real-world medical, poison, dosage, harvesting, or occult instructions.
- Source: [[memory/raw/game-design/glassroot/TWB_Glassroot_Garden_GPT_Pro_Research_Plan]]

## Open Questions

- Open Question - Which main-game Phase 3 start area is the current priority: content pool expansion, dungeon content expansion, or progression/economy expansion?
- Open Question - Should Companions assigned to Glassroot Garden be fully unavailable for all other active activities, or only unavailable for other automation systems?
- Open Question - Should Glassroot Scrip remain game-specific forever or later clear into a broader World Key token?
- Open Question - Should Notice Board bundle order always matter in production?
- Source: [[wiki/game-dev/open-questions]]

## Deeper Notes

- [[game-dev-task-workflow]]
- [[project-hierarchy]]
- [[build-test-commands]]
- [[main-game-overview]]
- [[main-game-systems]]
- [[world-keys]]
- [[player-fantasy]]
- [[primary-verbs]]
- [[current-mechanics]]
- [[core-loop]]
- [[wiki/game-dev/systems]]
- [[controls]]
- [[enemies]]
- [[level-design]]
- [[design-constraints]]
- [[technical-constraints]]
- [[wiki/game-dev/open-questions]]
