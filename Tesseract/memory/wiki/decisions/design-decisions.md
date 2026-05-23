# Design Decisions

## Workflow

- [[design-decision-workflow]]

## Record Format

Each decision should use:

```text
### YYYY-MM-DD - Short Decision Name

- Status:
- Decision:
- Reason:
- Source:
- Affected Areas:
- Risks:
- Review Trigger:
- Superseded By:
```

## Active Decisions

### 2026-05-11 - Use The World Beneath As Parent Project

- Status: Active
- Decision: Treat **The World Beneath** as the parent/main game and treat **World Key: Glassroot Garden** as a subgame/module inside that larger project.
- Reason: User clarified that the gardening game is a subgame, and local main-game source docs identify The World Beneath as the parent project.
- Source: User clarification - 2026-05-11.
- Source: [[memory/wiki/game-dev/project-hierarchy]]
- Source: [[memory/raw/game-design/main-game/MASTER_BOOTSTRAP_STAGE_1_DOCS_v8]]
- Affected Areas: Game design, memory, task briefs, playtesting, SEO marketing, decisions.
- Risks: If subgame-specific memory is used as parent-game authority, main-game strategy and marketing will drift.
- Review Trigger: When adding a new game, World Key, or main-game Phase 3 task.
- Superseded By: None.

### 2026-05-11 - Use Phaser, TypeScript, And Vite For First Playable

- Status: Active
- Decision: Use Phaser 3.90, TypeScript, and Vite for the first playable browser prototype.
- Reason: The local prototype package already uses this stack and the Glassroot plan recommends Phaser 3.90 + TypeScript + Vite.
- Source: `memory/raw/game-design/glassroot/package.json`
- Affected Areas: Technical implementation, game-dev task briefs, build/test commands.
- Risks: If the project moves to a different engine or production deployment shape, this decision must be superseded.
- Review Trigger: Before production hardening or engine migration.
- Superseded By: None.

### 2026-05-11 - Keep MVP Focused On The Visible Farm-To-Bundle Loop

- Status: Active
- Decision: Keep MVP scope focused on visible planting, growth, Companion help, harvest, processing, bundles, contracts, and World Key shared storage.
- Reason: The strongest first playable proves the core loop before adding a larger economy, generated narrative, or broad feature set.
- Source: [[memory/raw/game-design/glassroot/Full_Loop_Test_And_Implementation_Plan]]
- Affected Areas: Core loop, production scope, playtesting, feature prioritization.
- Risks: Scope may creep into marketplace, giant crafting, full NPC economy, or direct main-game reward systems before the basic loop is validated.
- Review Trigger: After the first successful external playtest set.
- Superseded By: None.

### 2026-05-11 - Use Angled Top-Down 2D For MVP

- Status: Active
- Decision: Use Stardew-like angled top-down 2D rather than true 3D or full isometric for MVP.
- Reason: The design needs readable tiles, simple input, clear mobile/desktop interaction, and manageable art scope.
- Source: [[memory/raw/game-design/glassroot/TWB_Glassroot_Garden_GPT_Pro_Research_Plan]]
- Affected Areas: Level design, controls, art, camera, mobile interaction.
- Risks: Visual richness must come from layout, animation, lighting, and UI polish rather than 3D spectacle.
- Review Trigger: After visual prototype and playtest feedback.
- Superseded By: None.

### 2026-05-11 - Keep World Key Storage Separate From Main-Game Inventory

- Status: Active
- Decision: Treat World Key shared storage as separate from directly usable main-game inventory.
- Reason: The current plan says World Key bundle outputs should not become direct main-game items in the MVP.
- Source: [[memory/raw/game-design/glassroot/Full_Loop_Test_And_Implementation_Plan]]
- Affected Areas: Rewards, economy, storage, contracts, platform integration.
- Risks: Players may expect harvested or bundled outputs to appear in main-game inventory unless the UI explains the separation clearly.
- Review Trigger: Before platform economy integration or public reward-bearing launch.
- Superseded By: None.

## Superseded Decisions

### 2026-05-11 - Use Glassroot Garden As Active Game Reference

- Status: Superseded
- Decision: Treat **World Key: Glassroot Garden** as the active game-design reference for this memory system.
- Reason: Local TWB-Farming docs were the first complete design source found, but user clarified Glassroot is a subgame rather than the main game.
- Source: [[memory/raw/game-design/glassroot/TWB_Glassroot_Garden_GPT_Pro_Research_Plan]]
- Affected Areas: Game design, memory, task briefs, playtesting, SEO marketing.
- Risks: This would over-centre the subgame and cause the memory system to ignore the main game.
- Review Trigger: Superseded immediately after user clarification.
- Superseded By: [[design-decisions#2026-05-11 - Use The World Beneath As Parent Project]]
