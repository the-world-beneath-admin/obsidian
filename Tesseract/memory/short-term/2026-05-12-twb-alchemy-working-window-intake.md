# Working Window Intake - 2026-05-12 - TWB Alchemy

## Project Identity
- Project/window name: TWB Alchemy / World Key: Alchemy Lab
- Main goal: Build a standalone browser-based alchemy World Key mini-game that shares inventory and pets with the other website World Keys.
- Scope: Web mini-game prototype only; not the main Unity game. Includes alchemy lab, herb bundle import/breakdown, crafting, finished product rack, autonomous pet cave exploration, and shared inventory export bundles.
- Code/project directory: C:\Users\yrred\Desktop\Unity\TWB-Alchemy
- Related Obsidian lane, if known: World Keys / The World Beneath website mini-games
- Suggested future worker role name: alchemy-lab-worldkey-worker

## Current State
The TWB Alchemy project is a standalone Vite + Phaser + TypeScript web mini-game in C:\Users\yrred\Desktop\Unity\TWB-Alchemy. It is explicitly separate from the main Unity project and should remain so.

Implemented so far: a brick-walled city basement alchemy lab UI, shared inventory localStorage handling, import/breakdown of herb bundles, lab storage, alchemy table crafting, finished rack, crafting XP and unlocks, regular outputs, essence bundle outputs, trapdoor to a cave view, tiled cave maze art pass, autonomous pet exploration, energy drain, return-home behavior, sleep cooldown, resource harvesting, node despawn/respawn, and staggered pet release from the shed.

Currently in progress: cave feel and pet movement tuning. Recent work widened cave paths, separated wall-frame tiles from pet-travel tiles, added direct walkable return paths to the shed, enforced the sleep timer only after pets reach the shed, smoothed cave redraws, and increased pet movement speed.

Not yet started or not production-ready: permanent account-backed shared inventory service, real website integration/routing, final pixel-art tileset/assets, production save migrations, full UX polish, mobile layout pass, and deeper cross-World-Key contract tests.

## Files And Areas Touched
- C:\Users\yrred\Desktop\Unity\TWB-Alchemy\src\scenes\AlchemyLabScene.ts
- C:\Users\yrred\Desktop\Unity\TWB-Alchemy\ALCHEMY_WIREFRAME_IMPLEMENTATION_PLAN.md
- C:\Users\yrred\Desktop\Unity\TWB-Alchemy\package.json
- C:\Users\yrred\Desktop\Unity\TWB-Alchemy\package-lock.json
- C:\Users\yrred\Desktop\Unity\TWB-Alchemy\vite.config.ts
- C:\Users\yrred\Desktop\Unity\TWB-Alchemy\tsconfig.json
- C:\Users\yrred\Desktop\Unity\TWB-Alchemy\dist\
- C:\Users\yrred\Desktop\Unity\TWB-Alchemy\dev-server.log
- C:\Users\yrred\Desktop\Unity\TWB-Alchemy\dev-server.err.log

## Decisions Made
- Decision - TWB Alchemy is a standalone browser World Key mini-game, not a Unity implementation.
- Source - User explicitly corrected that the World Keys are web games for the website and that the main Unity game should not be touched.

- Decision - The project lives in C:\Users\yrred\Desktop\Unity\TWB-Alchemy.
- Source - User explicitly requested the new mini-game be put in that directory.

- Decision - The alchemy game shares the umbrella inventory and pet concepts with other World Keys, but is its own independent mini-project.
- Source - User clarified that all three games use the same inventory system and pets, but each is its own game under the shared pet/inventory umbrella.

- Decision - In this game, pets automate cave gathering rather than farming.
- Source - User clarified that farming pets automate farming, while alchemy pets go down into the cave and retrieve cave materials.

- Decision - Cave exploration should be an explorable top-down maze, not a node-and-line system.
- Source - User requested replacing the node/line cave with a dark maze where pets explore randomly.

- Decision - Player-placed torches/lights were removed from the cave loop.
- Source - User requested removing player placed lights and torches because they are not needed for the pet exploration system.

- Decision - Pets should release from the shed one at a time with a 30-second release interval.
- Source - User requested pets should never release at the same time and asked for a 30-second release timer after each shed release.

- Decision - Sleep cooldown starts after the pet returns to the shed and unloads, not when energy hits zero.
- Source - User explicitly requested pathing pets back to the shed and starting sleep timer after they hit the shed.

## Memory-Worthy Facts
- Fact - Main Unity project should not be modified for this work.
- Source - User explicitly said not to build in Unity and to remove anything touched in the main game.

- Fact - TWB Alchemy uses local browser storage as the current prototype shared inventory and alchemy state backend.
- Source - Existing implementation in AlchemyLabScene.ts uses localStorage keys for shared inventory and alchemy state.

- Fact - Essence outputs are intended to become shared inventory bundles for another World Key to use.
- Source - User requested 15 essence outputs that go back into shared inventory for another World Key.

- Fact - Cave art direction is top-down orthographic / 2.5D tiled-map pixel-art RPG style.
- Source - User provided reference images and described the desired tiled-map top-down 2.5D style.

- Fact - Alchemy lab visual direction is a brick-walled city basement.
- Source - User requested the alchemy lab look like it is in a brick-walled city basement.

## Risks / Warnings
- Warning - Do not touch C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype for this project unless explicitly instructed later.
- Warning - Current shared inventory is browser-local prototype storage, not account-backed persistence.
- Warning - Existing saved localStorage state can affect observed pet release timing, pet sleep states, inventory counts, and cave run positions during testing.
- Warning - The project is not a git repository, so rollback/change tracking is limited unless external backups are used.
- Warning - Generated dist assets change after every build and may not be meaningful to preserve manually.
- Warning - Phaser bundle size triggers Vite chunk-size warnings after production build.
- Warning - Cave visuals are still procedural wireframe/pixel-style placeholders, not a final imported tileset.

## Open Questions
- What exact website route or World Key launcher entry should TWB Alchemy use when integrated?
- What is the final shared inventory schema across Glassroot Garden, Alchemy Lab, and future World Keys?
- Should pet identities, levels, and cooldowns be shared globally across World Keys or per mini-game?
- What account/service backend will replace localStorage for shared inventory and saved game state?
- Should essence bundles have fixed recipes/economy values before broader integration?
- What final tileset/art pipeline should be used for the cave and lab?
- Should there be an explicit save reset/debug panel for development builds?

## Do Not Promote
- Do not promote any prior Unity implementation direction for this project.
- Do not promote temporary cave path coordinates as final map design.
- Do not promote procedural placeholder art as final art direction beyond the broad tiled top-down style.
- Do not promote current localStorage keys as final production API contracts.
- Do not promote current recipe balance, XP numbers, material yields, or pet speeds as final economy tuning.
- Do not promote dist asset filenames; they are build artifacts.

## Current Blockers
No hard blocker is preventing prototype progress. The main gating issue is design/integration clarity around the shared World Key ecosystem, persistent account storage, and final art/tileset direction.

## Checks Run
- npm.cmd run build
- Browser smoke checks at http://127.0.0.1:5174/
- Browser cave view checks for console errors after movement/pathing changes
- Manual visual checks from screenshots/user feedback for cave wall traversal, pet release timing, and movement smoothness

## Cleanup Needed
- C:\Users\yrred\Desktop\Unity\TWB-Alchemy\dist\ may contain generated build output.
- C:\Users\yrred\Desktop\Unity\TWB-Alchemy\dev-server.log and dev-server.err.log may contain temporary local dev output.
- Browser localStorage may contain test inventory, pet run, and cave state that can affect manual QA.
- Old zip backups in the TWB-Alchemy folder should be reviewed before any cleanup; do not delete without explicit permission.

## Recommended Obsidian Tree
- memory/wiki/world-keys/overview.md
- memory/wiki/world-keys/alchemy-lab.md
- memory/wiki/world-keys/shared-inventory.md
- memory/wiki/world-keys/pets.md
- memory/wiki/world-keys/decisions.md
- memory/wiki/world-keys/open-questions.md
- memory/reports/world-keys/
- memory/short-term/

## Recommended Worker Agent
- Agent name: alchemy-lab-worldkey-worker
- Purpose: Continue the TWB Alchemy browser mini-game while preserving separation from the main Unity project and maintaining compatibility with the shared World Key inventory/pet ecosystem.
- Read-first files: C:\Users\yrred\Desktop\Unity\TWB-Alchemy\ALCHEMY_WIREFRAME_IMPLEMENTATION_PLAN.md; C:\Users\yrred\Desktop\Unity\TWB-Alchemy\src\scenes\AlchemyLabScene.ts; C:\Users\yrred\Desktop\Unity\TWB-Alchemy\package.json
- Allowed write paths: C:\Users\yrred\Desktop\Unity\TWB-Alchemy\; C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\ when explicitly asked for short-term reports
- Forbidden write paths: C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\; C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\; C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md; C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md; C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\log.md
- Done criteria: Changes stay inside TWB-Alchemy unless explicitly authorized; build passes; browser smoke test has no console errors; cave/pet behavior matches current user direction; handoff notes go to memory/short-term/ when requested.
- Report destination: memory/short-term/

## Next Recommended Gate
Bob/orchestrator should review this intake and decide which durable facts and decisions become permanent World Key memory before further implementation continues.
