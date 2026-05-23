# The Alchemy Lab Decisions

## Active Decisions

- Decision - TWB Alchemy is a standalone browser World Key mini-game, not a Unity implementation.
- Decision - The project lives in `C:\Users\yrred\Desktop\Unity\TWB-Alchemy`.
- Decision - The main Unity project must not be modified for this work.
- Decision - The alchemy game shares umbrella inventory and pet concepts with other World Keys, but is its own independent mini-project.
- Decision - In The Alchemy Lab, pets automate cave gathering rather than farming.
- Decision - Cave exploration should be an explorable top-down maze, not a node-and-line system.
- Decision - Player-placed torches/lights are removed from the cave loop.
- Decision - Pets release from the shed one at a time with a 30-second release interval.
- Decision - Sleep cooldown starts after the pet returns to the shed and unloads, not when energy hits zero.

## Warnings

- Warning - Do not touch `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype` for this project unless explicitly instructed later.
- Warning - Current shared inventory is browser-local prototype storage, not account-backed persistence.
- Warning - Existing localStorage state can affect observed pet release timing, pet sleep states, inventory counts, and cave run positions during testing.
- Warning - The project is not a git repository, so rollback/change tracking is limited unless external backups are used.
- Warning - Generated `dist\` assets change after every build and may not be meaningful to preserve manually.
- Warning - Phaser bundle size triggers Vite chunk-size warnings after production build.
- Warning - Cave visuals are still procedural/pixel-style placeholders, not a final imported tileset.

## Sources

- [[short-term/2026-05-12-twb-alchemy-working-window-intake]]
