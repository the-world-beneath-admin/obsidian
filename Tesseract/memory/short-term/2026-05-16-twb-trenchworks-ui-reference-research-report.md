# TWB Trenchworks UI Reference Research Report

Date: 2026-05-16
Worker scope: Standalone TWB-tagged game / TWB Trenchworks
Project target: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

## Sources / Links

- Captain of Industry Steam page: https://store.steampowered.com/app/1594320/
- Captain of Industry SteamDB screenshots/metadata: https://steamdb.info/app/1594320/screenshots/
- Captain of Industry Update 3 UI notes: https://www.captain-of-industry.com/post/update3-is-out
- Captain of Industry Wiki - Selection Tools: https://wiki.coigame.com/Selection_Tools
- Captain of Industry Wiki - Settlement UI reference: https://wiki.coigame.com/Settlement
- Captain of Industry Wiki - UI images category: https://wiki.coigame.com/Category%3AUI_images
- Captain of Industry Reddit feedback on Update 3 UI: https://www.reddit.com/r/captain_of_industry/comments/1kmqqpv/feedbackthread_to_update3/
- Captain of Industry Reddit thread on missing naval/ship build category: https://www.reddit.com/r/captain_of_industry/comments/1kq39ix/i_miss_having_a_navalship_building_category_in/
- Captain of Industry Reddit QoL/UI thread: https://www.reddit.com/r/captain_of_industry/comments/1de934u/quality_of_life_features_youd_like_to_see/
- Factorio Wiki - Quickbar: https://wiki.factorio.com/Quickbar
- Factorio Wiki - Shortcut bar: https://wiki.factorio.com/Shortcut_bar
- Satisfactory Wiki - Build Gun / build menu and hotbar binding: https://satisfactory.wiki.gg/wiki/Build_Gun
- Satisfactory Wiki - Settings / hotbar and build menu options: https://satisfactory.wiki.gg/wiki/Settings
- Anno 1800 interface guide: https://www.gamepressure.com/anno-1800/interface/z4b4f8

Notes: Only public web pages, public screenshots/metadata, public wiki pages, and public discussion threads were used. No game files, proprietary assets, code, or extracted UI resources were accessed.

## Observed UI Patterns

### Captain of Industry

- HUD structure uses a simulation-builder pattern: high-level settlement/resource status at the top, build/actions along the bottom, contextual details and resource/material tracking at the right, notifications/warnings at screen edges.
- Public Update 3 notes confirm a broad UI overhaul covering entity detail windows, statistics, codex, HUD, blueprints, and construction responsiveness. This suggests the game treats UI speed as part of factory-building ergonomics, not merely decoration.
- Selection tools include planning mode, pause/unpause, and instant-build/boost style actions. The key pattern is separating "lay out intent" from "commit resources/workers now."
- Public settlement documentation references top-left population access and a right-side population overview pane. This supports the pattern of making global status clickable into deeper detail instead of showing every number permanently.
- Public feedback after Update 3 flags several risks: too many extra clicks, reduced readability from transparent/alternating panels, small or stylized fonts, and category recall problems when buildings are placed in unexpected build tabs.
- Category feedback is especially relevant: players wanted functionally obvious groupings, search, and sometimes duplicate placement in more than one category when an item logically belongs in multiple contexts.

### Comparable Factory / Builder Patterns

- Factorio separates the always-visible quickbar from the shortcut/action bar. The quickbar is a customizable set of links, not inventory storage, and supports multiple bars with keyboard access.
- Factorio shortcut tools expose recurrent actions such as alt-info, undo/redo, copy/paste, blueprints, deconstruction, and upgrade planning. The lesson for Trenchworks is to keep high-frequency map/build actions visible and hotkeyable.
- Satisfactory supports build-menu-to-hotbar binding by hovering a buildable and pressing 0-9. Its pattern is good for player-defined favorites without forcing every buildable into a crowded permanent bar.
- Anno 1800 uses a traditional management layout: top global economy/population/status, bottom construction categories, right selected-object detail, minimap/resource context, and edge warnings. It is a useful older-city-builder confirmation that this layout remains legible when the game has many parallel systems.

## What To Adapt For Trenchworks

- Use the proven management-game screen geography:
  - Top bar: global war/factory state.
  - Bottom bar: build categories and hotbar/favorites.
  - Right tracker: selected structure, active build plan, logistics bottleneck, or combat/frontline detail.
  - Map overlay controls: grid, ghost plan, logistics flow, threat/frontline, repair, demolish, pause.
- Separate planning from commitment. Trenchworks should let players sketch belts, trenches, bunkers, depots, and production chains as ghosts before spending materials or assigning crews.
- Include search or quick-find for buildables once the category list grows. CoI feedback makes clear that category memory becomes brittle.
- Allow some duplicate buildables in multiple logical categories where useful. Example: a Field Depot could appear under Logistics and Frontline; a Repair Post under Defense and Maintenance. This is less offensive than hiding core items in "technically correct" tabs.
- Keep resource/status labels readable over aesthetic styling. Trenchworks can have a military-industrial tone, but not at the cost of small text, low opacity, or excessive panel transparency.
- Provide player-customizable favorites/hotbar slots separate from the main build category bar.

## What Not To Copy

- Do not copy Captain of Industry icon art, panel shapes, category names, visual styling, screenshots, or asset language. Treat CoI as a public UX reference only.
- Do not reproduce CoI's exact bottom bar grouping. Public feedback suggests some groupings after Update 3 were controversial, especially when "ship" style functions were split across categories.
- Do not lean on translucent alternating right-side resource rows. Public feedback specifically complains that such panels can become hard to scan.
- Do not use narrow seven-segment or novelty fonts for important status data. Factory games ask players to read numbers constantly; legibility wins.
- Do not bury common actions behind two or three clicks. The research signal is blunt: players notice click inflation.

## Concrete Recommendations: Bottom Build Categories

Recommended first-pass bottom build layout for Trenchworks:

1. Logistics
   - roads/paths, conveyors, pipes, haulers, depots, storage yards, distribution posts
2. Production
   - extractors, refineries, workshops, ammo/parts fabrication, power-processing buildings
3. Frontline
   - trenches, bunkers, emplacements, command posts, observation posts, field depots
4. Utilities
   - power, water/fuel lines, maintenance, repair, worker/support infrastructure
5. Terrain
   - dig, fill, flatten, ramp, reinforce ground, remove obstacle
6. Planning
   - ghost plan mode, blueprint/save layout, copy, paste, rotate, mirror, upgrade, deconstruct
7. Emergency
   - pause area, priority repair, ration/shortage response, evacuate/disable, alert filters
8. Favorites
   - 0-9 player-bound buildables/tools, with visible hotkeys and drag/rebind support

Category principles:

- Keep categories based on player intent, not internal simulation taxonomy.
- Put "findability" above purity. If a building serves two strong player intents, duplicate it.
- Show locked future categories as subdued only when they teach progression; hide deep future clutter if it becomes noise.
- Every bottom category should open a compact tray, not a giant modal that covers the map.
- Category tray should show: icon, name, cost, required inputs, unavailable reason, and a short warning if placement would fail.

## Top Info Bar Recommendation

- Left: game clock/speed/pause, alert count, current objective or milestone.
- Center: critical stockpile strip with only the resources that matter now: steel/scrap, concrete, fuel, power, workers/crew, ammunition/supplies.
- Right: war/frontline health, logistics congestion, research/progression, settings/map modes.
- Clicking any metric should open the relevant detailed view in the right tracker.
- Support pinning resources to the top bar so players can choose what to monitor.

## Right Detailed Tracker Recommendation

- Use one right-side panel with mode tabs rather than several competing panels:
  - Selected
  - Build Queue
  - Logistics
  - Frontline
  - Alerts
- Default behavior should follow context: selecting a building shows selected details; opening build mode shows cost/placement/queue details; selecting frontline overlay shows threat/supply/repair state.
- Rows should have stable opaque backgrounds and strong contrast. Avoid alternating transparency.
- The panel should collapse to icon-only or a narrow summary when building large layouts.

## Map / Build Ergonomics

- Always provide clear ghost placement with valid/invalid color states, footprint, rotation indicator, connector hints, and projected route/flow direction.
- Add "planning pause": players can queue a large trench/factory layout without instantly consuming stockpiles.
- Include rectangular drag tools for roads, trenches, barriers, demolish, upgrade, and priority zones.
- Add copy/paste and undo/redo early. Public factory-builder expectations strongly favor this, especially for repeated layouts.
- Provide overlays for logistics flow, power/fuel coverage, frontline danger, worker access, blocked routes, and terrain height.
- Keep the map interactable while trays are open; the UI should frame building work, not seize the screen.

## Risks

- CoI is a strong reference but too close a visual imitation would be legally and creatively weak. Adapt principles, not expression.
- A bottom bar with too many tabs will become a filing cabinet. Start with fewer intent-based categories and use search/favorites to absorb growth.
- If the right tracker tries to show every resource permanently, it will become wallpaper. Let the player pin important items and surface only bottlenecks by default.
- A stylized trench-war UI could easily become muddy. Test readability at 1080p and smaller laptop/Steam Deck-like scales before polishing the theme.
- Transparent panels may look modern in screenshots and fail during real play. Use opacity and contrast first; flourish after the numbers are readable.
- Public Reddit feedback is useful signal, not a statistically reliable survey. Treat it as warning signs to test in Trenchworks playtests.

## Memory-Worthy Notes

- For Trenchworks, use a bottom intent-based build bar plus player favorites/hotbar rather than a single exhaustive build catalog.
- Keep planning/ghost placement separate from resource commitment.
- Prioritize category recall, search, duplicate placement for cross-functional buildings, and readable right-panel tracking.
- Avoid copying Captain of Industry visuals, icons, exact category scheme, or proprietary assets.
