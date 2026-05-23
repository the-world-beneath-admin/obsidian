# Browser Archaeology Game Implementation Plan

This plan describes the first browser-based mini game for the TWB multi-game network: a semi-idle archaeology mission game that shares companions, inventory, crafting inputs, Will, and companion lock state with the main Unity game.

The important framing is that this is not "a side web game with a save file." It is the first browser client for the shared TWB platform backend. The browser game should be fun on its own, but every important state change must be owned by the server so the main game, future mini games, and the economy all agree.

## Working Assumptions

- The shared resource is called `Will` in code. If the player-facing spelling should be `wil`, that can be a UI/content decision later.
- Existing Unity saves are currently local-first. The browser game requires a networked account backend before it can truly share inventory and pets.
- Existing useful local foundations include:
  - `PlayerData.WorldMap` with starter home/current location state.
  - `MaterialInventoryState` and `CardInventoryState` as split inventory containers.
  - `SoftCurrency`, with `InventoryService` already treating `CurrencyType.Soft` and `CurrencyType.Will` as wallet-style rewards.
  - `WorldMapInfluencePointGeneratedCatalog`, currently a baked POI catalog.
  - `WorldMapDungeons` domain/service work that already models map-spawned timed activity instances.
- The first browser game should use the same architectural shape as world-map dungeons, but with archaeology-specific nodes, tools, staged timers, and check-in mini games.
- Browser clients are untrusted. They can request actions and submit mini-game results, but the backend decides rewards, companion locks, node progression, and item grants.
- Version 1 content resolution is `country`, not county and not state/province. The player may enter a city to choose a starting country, but the archaeology map and content package should be country-based.
- Version 1 content target is 50 reusable archaeology events per country.
- Using the Natural Earth Admin-0 country/admin map baseline of 258 records, the full worldwide v1 package is 12,900 events and 258 high-resolution country map images. If the launch list is reduced to roughly 195 widely recognized countries, the package is 9,750 events and 195 country map images.

## Clarifying Questions

These do not block the first plan. Items marked as locked are covered by [Archaeology_V1_Product_Lock.md](C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Documentation/Archaeology_V1_Product_Lock.md).

1. Locked for v1: backend/shared API uses `WILL`; Unity `SoftCurrency` is a compatibility bridge.
2. Locked for v1: internal package uses the full Natural Earth Admin-0 baseline, with public UI suppression allowed for sensitive records.
3. How precise should player home location be? City-level only is safer for privacy; exact coordinates create more design and privacy burden.
4. Do you want the browser mini game to require the same account login as the main game immediately, or can the MVP support guest accounts that later link?
5. Locked for v1: archaeology assignment and cross-game locks use a new global `companion_id` that links to Unity/card identifiers.
6. Can players cancel archaeology missions early? If yes, should the pet unlock immediately with no reward, partial reward, or a Will fee?
7. Locked for v1: real-history events use the safety/tone rules in the product lock, with manual review for high-risk flags.
8. Locked for v1: every event separates `real_history_summary` from `twb_lore_layer`.
9. Partially locked for v1: higher-tier events require durable sources; low-risk lower-tier events can use curated source entries/templates.
10. Locked for v1: archaeology Companion Cards are tradeable by default, but trade/auction access exists only in the main game.
11. Locked for v1: archaeology tools are account-bound, durable, breakable, not repairable, and not auctionable/tradeable.
12. Is OpenAI acceptable as the initial AI provider, with the generation layer abstracted so providers can be swapped later?

## V1 Product Lock

The first five Series 0 decisions are implemented in:

- [Archaeology_V1_Product_Lock.md](C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Documentation/Archaeology_V1_Product_Lock.md)

Locked defaults:

- Story-facing term is `Companion`; `pet` remains a legacy/internal bridge.
- Shared backend currency is `WILL`.
- Country package uses Natural Earth Admin-0 baseline, 258 records, 50 events each.
- Cross-game locks use global `companion_id`.
- Real history and TWB fiction are stored separately with safety flags and manual review rules.
- Archaeology drops components and rare Companion Cards; final usable products are crafted.
- Archaeology tools are account-bound durable breakables with no v1 repair path.
- Every material grant records provenance.

## V1 Content Seed Spec

Series 0 content seeds are implemented in:

- [Archaeology_V1_Content_Seed_Spec.md](C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Documentation/Archaeology_V1_Content_Seed_Spec.md)

Locked seed defaults:

- 20 archaeology material item IDs.
- 10 archaeology tool item IDs.
- 2 check-in mini-game specs.
- 10 country event templates.
- 4 prompt templates for slot building, fact extraction, event writing, and safety/canon review.

## Product Goal

Build a browser-accessible archaeology mini game where a player:

1. Logs into the shared TWB account.
2. Uses their main-game pets.
3. Starts from their main-game home location, or enters a nearby city if they have never played the main game.
4. Views a detailed, stylized map of their country with 50 archaeology/investigation events available through progression.
5. Sends pets on timed archaeology missions.
6. Checks in every 5 minutes to 1 hour to play small archaeology-themed mini games.
7. Advances staged node progress and reveals more story.
8. Earns mini rewards at each stage.
9. Claims a final reward whose quality can degrade from failed check-ins, but never below 50%.
10. Has a small chance at a Companion Card drop from final node completion.
11. Sends all resources, Companion Cards, tools, and Will into the shared account inventory.
12. Cannot use the main-game auction from the mini game, but can sell unwanted items for a deliberately poor Will return.

Starter companion:

- The archaeology game starter companion should be Hazel/the squirrel from Book 1.
- The main game starter companion can still be Nova.
- Other Book 1 characters are not game cast.

Story scope:

- The archaeology game is anthology exploration, not a central campaign.
- There is no main enemy throughput, no required global villain, and no single overarching story arc.
- Country events can form small arcs only when the real-world source material naturally supports them.
- Book characters do not appear as game NPCs or quest givers.
- Hazel/the squirrel is the archaeology game's starter companion from Book 1.
- The player is called an `Initiate`.
- The archaeology game assumes the player is already awakened and already has their `World Key`.
- The inventory/information action should be labeled `Open Field Kit`.
- Faction war and player faction mechanics belong to the main game, not this mini-game.
- Archaeology events may mention historical, extinct, made-up, or background factions, but should not use current player/NPC faction systems.

## Non-Negotiable Rules

- The server is authoritative for inventory, companions, companion locks, rewards, node generation, timers, and final quality.
- The browser never grants itself items.
- The AI never grants rewards and never mutates player inventory.
- Generated nodes are cached permanently by stable node id. The same node returns the same quest unless a new content version is intentionally published.
- Real history and TWB lore should be stored separately, even if the UI presents them together.
- Player location should default to city/home-region precision unless the player explicitly gives a more precise location.
- Auction access stays in the main game only.
- Quick-sell/salvage in browser pays a poor exchange rate so the browser game does not replace the main economy.
- Do not use Carl, Sara, Randy, Granny B, or other Book 1 characters as archaeology game cast. Book 1 is source canon and tone reference, not the game's NPC roster.
- Do not impose a central story arc on the archaeology game.
- Do not add player faction gameplay, faction war, territory influence competition, or current-faction membership to archaeology v1.

## Recommended Stack

### Browser Client

- TypeScript.
- Vite.
- Phaser for check-in mini games and lightweight 2D interactions.
- MapLibre GL JS for the map surface, markers, clustering, country-level view, and future vector tile support.
- Responsive PWA shell for desktop and mobile browsers.

MapLibre is a good fit because it renders interactive vector maps in the browser with WebGL and supports markers, popups, sources, and layers. Leaflet is a simpler fallback if the first prototype only needs raster tiles and basic markers.

### Backend

Recommended first choice:

- ASP.NET Core API in C#.
- PostgreSQL with PostGIS.
- Redis or a managed queue for AI generation jobs.
- Object storage for generated content artifacts, source snapshots, and audit payloads.

Reason: the main game already has a large C# domain model. A C# backend lets us share or port rules for items, rewards, pets, and deterministic systems without rewriting everything in TypeScript.

Acceptable faster prototype:

- Supabase Postgres/Auth plus Edge Functions.
- Browser client in TypeScript.
- A later C# service can replace the edge functions once the domain contracts stabilize.

### AI Generation

Use the OpenAI Responses API with structured outputs.

Recommended model routing as of the current official OpenAI docs:

- `gpt-5.4-nano` for cheap structured extraction, classification, source summarization, node tagging, and low-tier quest drafting.
- `gpt-5.4-mini` for higher quality story shaping, richer tier 2-4 quest text, and review/rewrite passes.
- `gpt-5.4` only for manually approved high-tier world quests, major historical events, and complex canon work.
- Batch API for non-urgent pre-generation because OpenAI documents a 50% cost discount and 24-hour turnaround for batch jobs.

Approximate generation cost target:

- Low-tier cached node with `gpt-5.4-nano`: usually fractions of a cent if prompts stay compact.
- Higher-tier node with `gpt-5.4-mini`: still low enough for one-time generation if every node is cached and reused.
- Do not generate on every player visit. Generate once, store forever, reuse many times.

### V1 Content Scale

The first global content package should be pre-generated, web-hosted, and pulled by the browser as needed. It should not be generated during normal player traffic, and it should not require the whole package to be downloaded locally.

Country baseline options:

| Country list basis | Country/map records | Events at 50 each |
|---|---:|---:|
| Reduced recognized-country list | ~195 | 9,750 |
| ISO-style countries/territories | ~249 | 12,450 |
| Natural Earth Admin-0 map baseline | 258 | 12,900 |

Recommended v1 target: use the Natural Earth Admin-0 baseline unless we later decide to hide disputed or sensitive units from the public UI. That gives us one complete global map/content pack with predictable IDs.

Map image package:

| Image type | Count with 258 countries | Estimated storage |
|---|---:|---:|
| High-res country map, 2 MB WebP/AVIF avg | 258 | ~516 MB |
| High-res country map, 5 MB avg | 258 | ~1.29 GB |
| High-res country map, 10 MB avg | 258 | ~2.58 GB |

Event data package:

| Event JSON size | 12,900 events |
|---|---:|
| 10 KB avg | ~129 MB |
| 25 KB avg | ~323 MB |
| 50 KB avg | ~645 MB |
| 100 KB avg | ~1.29 GB |

Practical v1 storage target: 2-5 GB total for country map images, event JSON, indexes, thumbnails, and metadata. This is small enough to host cheaply in object storage and cache aggressively through a CDN.

Content package naming:

```text
archaeology_world_v1_admin0_50
```

The package should contain:

- `countries/index.json`
- `countries/{country_code}/manifest.json`
- `countries/{country_code}/map.webp`
- `countries/{country_code}/events/{event_id}.json`
- `countries/{country_code}/events/index.json`
- `schemas/archaeology_event.schema.json`
- `credits/source_manifest.json`

Normal gameplay should request only the needed country manifest, country map image/tiles, visible event summaries, and selected event JSON from the web-hosted package. The browser can use normal HTTP/browser caching, but the game should not download the full world package locally. The database should store only player progress, active missions, reward claims, companion locks, and event-version references.

## System Shape

```text
Unity Main Game
Browser Archaeology Game
Future Browser Fishing/Farming/Alchemy Games
        |
        v
Shared Account/Auth API
Shared Player Profile API
Shared Inventory API
Shared Pet API
Shared Pet Lock API
Shared Economy/Crafting API
Shared Map/POI API
Shared AI Content Generation Worker
Shared Ledger/Audit Store
```

## Data Model

The database should be designed for the whole multi-game network now, even if archaeology is the first browser game to use it.

### Accounts And Profiles

`accounts`

- `account_id`
- `created_at`
- `primary_auth_provider`
- `status`

`player_profiles`

- `player_id`
- `account_id`
- `display_name`
- `callsign`
- `age`
- `gender`
- `privacy_mode`
- `public_name_mode`
- `created_at`
- `last_seen_at`

Profile rules:

- `callsign` is the preferred public-facing mini-game identity.
- `display_name`, `age`, and `gender` can be hidden from other players.
- The archaeology game calls the player an `Initiate`.
- Keep the mini-game profile lightweight; faction identity belongs to the main game.

`player_home_locations`

- `player_id`
- `source_game`
- `country_code`
- `admin1`
- `city_name`
- `lat_e7`
- `lon_e7`
- `precision`
- `created_at`
- `updated_at`

Location precision values:

- `main_game_home`
- `city_centroid`
- `manual_city`
- `coarse_region`

Archaeology home rules:

- The archaeology home city creates a home base, home map node, and map origin.
- Home country/city cannot be changed from inside archaeology v1.
- The home node should open inventory and information systems while the player is viewing their home country.
- Outside home territory, `Open Field Kit` should remain accessible through a fixed UI icon.
- Traveling to another country costs `WILL`, even when the cost is minor, to discourage endless territory scrolling.

The browser game should first read the main-game home location. If absent, ask for a city and geocode it to a city centroid. Do not require exact GPS.

### Shared Inventory

`item_definitions`

- `item_id`
- `display_name`
- `item_type`
- `tier`
- `rarity`
- `stackable`
- `tradeable`
- `account_bound`
- `quick_sell_will_value`
- `metadata_json`

`player_inventory_stacks`

- `player_id`
- `item_id`
- `quantity`
- `updated_at`

`item_instances`

- `item_instance_id`
- `player_id`
- `item_id`
- `quantity`
- `durability_bps`
- `bound_state`
- `metadata_json`
- `created_at`
- `updated_at`

Use stacks for generic normal materials only when provenance can live entirely in the ledger. Use instances or provenance batches for archaeology materials if the player needs to inspect, sell, export, or craft from a specific source. Use instances for Companion Cards, tools, and any item with durability or per-instance state.

`inventory_ledger`

- `ledger_id`
- `player_id`
- `change_type`
- `source_game`
- `source_activity_id`
- `item_id`
- `item_instance_id`
- `quantity_delta`
- `currency_delta`
- `created_at`
- `server_seed`
- `metadata_json`

Every reward, salvage sale, craft, item consume, Companion Card drop, and admin correction must write a ledger row.

Material reward rule:

- Shared material item IDs stay broad and reusable.
- Every archaeology material grant must store provenance in `inventory_ledger.metadata_json` or instance metadata: `content_package_id`, `country_key`, `event_id`, `event_tier`, `source_fact_ids`, `mission_id`, `stage_id`, and `quality_bps`.
- Archaeology reward tables grant components, not finished usable products, except for rare Companion Cards at final completion.

### Currency

`wallet_balances`

- `player_id`
- `currency_code`
- `balance`
- `updated_at`

V1 currency rule:

- Use `currency_code = WILL` for the shared browser/main-game base currency.
- Treat existing Unity `SoftCurrency` as a compatibility bridge into `WILL` until the Unity UI/data model is migrated.
- Ledger rows should record `WILL`, not `SoftCurrency`.

### Companions

`companions`

- `companion_id`
- `player_id`
- `source_game`
- `creature_definition_id`
- `current_card_item_instance_id`
- `unity_creature_instance_id`
- `bond_state`
- `role`
- `tier`
- `rarity`
- `base_attack`
- `base_defense`
- `base_utility`
- `created_at`
- `updated_at`
- `metadata_json`

`companion_cards`

- `item_instance_id`
- `companion_id`
- `player_id`
- `card_state`
- `source_type`
- `bond_state`
- `trade_policy`
- `drop_line`
- `safe_once_earned`
- `provenance_note`
- `created_at`

V1 identity rule:

- `companion_id` is the authoritative cross-game identity.
- Unity `CreatureInstance.InstanceId` and card `ItemInstanceId` are linked references, not the permanent network identity.
- A Companion Card is a device readout for a bond record, summon pattern, contract, command structure, capture state, construct schema, or recorded being. Store provenance and bond state so trade/reward rules can vary by source.
- Archaeology Companion Cards default to `trade_policy = tradeable`, but archaeology does not expose trade/auction UI.
- Archaeology Companion Cards are safe once earned and should include a source-specific `drop_line`.

### Global Companion Locks

`companion_locks`

- `lock_id`
- `companion_id`
- `player_id`
- `source_game`
- `activity_type`
- `activity_id`
- `started_at`
- `expires_at`
- `released_at`
- `state`

Database rule:

- Only one active lock per `companion_id`.

Start mission transaction:

1. Verify the player has access to every selected companion.
2. Verify every companion has no active lock.
3. Verify required tool/item costs.
4. Create archaeology mission.
5. Insert companion locks.
6. Consume costs.
7. Commit.

If any step fails, nothing changes.

### Tools And Crafting

`recipe_definitions`

- `recipe_id`
- `output_item_id`
- `output_quantity`
- `category`
- `tier`
- `source_game`
- `is_shared`
- `metadata_json`

`recipe_inputs`

- `recipe_id`
- `input_item_id`
- `quantity`

Archaeology can use a simpler archaeology-specific recipe slice in v1, but it should share the same item definitions, ledger patterns, and mental model as the main game. The database should be ready to merge into the larger shared recipe system later.

Tool rules:

- Tools can be mundane, World Key-enhanced, magical artifacts, tech gadgets, or hybrids.
- Tools are account-bound.
- Tools are not tradeable or auctionable.
- Tools are durable and breakable.
- Tools are not repairable in v1.
- Broken tools must be replaced or crafted again.
- Tool ownership, damage, and breakage are server-authoritative.

Tool categories:

- `survey`
- `excavation`
- `screening`
- `recording`
- `conservation`
- `analysis`

Initial real-world-inspired tool set:

- Field notebook.
- Measuring tape.
- Hand trowel.
- Soft brush.
- Sieve/screen.
- Line level/plumb bob.
- Hand lens.
- Sample bags.
- Conservation wrap.
- GPS/field mapper.
- Total station.
- Magnetometer.
- Ground-penetrating radar.
- Flotation kit.

Early tools can be simple stat modifiers. Later tools can unlock specific node stages or mini-game advantages. Tools are final usable products, so they should come from crafting rather than normal random drops.

### Archaeology Nodes

`archaeology_nodes`

- `node_id`
- `country_code`
- `country_slug`
- `event_index`
- `display_name`
- `tier`
- `node_type`
- `map_x_bps`
- `map_y_bps`
- `lat_e7`
- `lon_e7`
- `source_region_label`
- `source_status`
- `content_status`
- `active_content_version`
- `created_at`
- `updated_at`

Country-centric notes:

- `event_index` should run 1-50 inside each country content package.
- `map_x_bps` and `map_y_bps` place the marker on the custom country map image without requiring precise geodata for every event.
- `lat_e7` and `lon_e7` can be optional or approximate. They are useful for later map upgrades, but v1 does not need county/state precision.
- `source_region_label` can hold a human-readable region like "northern coast", "old capital district", "western rail corridor", or "Andes foothills" without forcing a global state/province schema.

Stable node id pattern:

```text
arch_{country}_{event_index}_{tier}_{source_hash}_{canon_version}
```

`archaeology_node_content_versions`

- `node_content_id`
- `node_id`
- `content_version`
- `title`
- `real_history_summary`
- `twb_lore_layer`
- `mission_brief`
- `stage_json`
- `reward_table_id`
- `model_id`
- `prompt_version`
- `schema_version`
- `created_at`
- `approved_at`
- `approved_by`

`archaeology_node_sources`

- `source_id`
- `node_id`
- `source_url`
- `source_title`
- `source_type`
- `publisher`
- `retrieved_at`
- `source_hash`
- `fact_extract_json`

`archaeology_generation_jobs`

- `job_id`
- `node_id`
- `job_type`
- `status`
- `model_id`
- `attempt_count`
- `error`
- `created_at`
- `finished_at`

### Player Missions

`archaeology_missions`

- `mission_id`
- `player_id`
- `node_id`
- `node_content_id`
- `state`
- `tier`
- `current_stage_index`
- `quality_bps`
- `started_at`
- `next_checkin_at`
- `completes_at`
- `claimed_at`
- `server_seed`
- `metadata_json`

`archaeology_mission_companions`

- `mission_id`
- `companion_id`
- `role_projection_json`

`archaeology_mission_tools`

- `mission_id`
- `item_instance_id`
- `tool_effect_json`
- `durability_cost_bps`

`archaeology_stage_attempts`

- `attempt_id`
- `mission_id`
- `stage_index`
- `mini_game_type`
- `server_seed`
- `client_result_json`
- `validated_result`
- `quality_delta_bps`
- `mini_reward_ledger_id`
- `created_at`

### World Projects

`archaeology_world_projects`

- `project_id`
- `display_name`
- `historical_event_key`
- `country_code`
- `scope`
- `tier`
- `state`
- `progress_required`
- `progress_current`
- `starts_at`
- `ends_at`
- `content_version`
- `metadata_json`

`archaeology_world_project_contributions`

- `contribution_id`
- `project_id`
- `player_id`
- `companion_id`
- `mission_id`
- `progress_delta`
- `reward_claimed`
- `created_at`

World projects are for major historical events, famous archaeological campaigns, and shared server-wide mysteries. They should use stricter source requirements and probably manual approval before publication. They must remain optional anthology-scale events, not a central story arc.

No v1 archaeology player-faction tables:

- Player-created factions are a main-game system.
- Archaeology can reference historical/background factions in event content, but should not store faction membership, faction territory, faction war state, or faction influence scores.

## Map And Node Discovery

### Home Location Flow

1. Browser game loads player profile.
2. API checks for `player_home_locations` from the main game.
3. If present, center the game on the home country and show the home-base node.
4. If absent, ask for nearest city.
5. Geocode city to coarse lat/lon and country.
6. Store city-level home location as the archaeology home base/map origin.
7. Fetch the country content manifest and visible archaeology events for that country.

Travel rules:

- Players may travel to any country if they can pay the `WILL` travel cost.
- Travel cost should be a nuisance fee, not a strategic blocker, but should not be zero.
- Home city/country cannot be changed from within archaeology v1.

Development can use public geocoding cautiously. Production should use a paid geocoding service, a self-hosted Nominatim instance, or a managed provider. The public OpenStreetMap Nominatim service has usage policy limits and is not a production autocomplete backend.

### Country Map

The country map should be a custom, high-resolution, TWB-styled image or tiled image for that country. It should show:

- Available archaeology events.
- Locked/high-tier events.
- In-progress missions.
- Completed/claimable missions.
- World projects.
- A home-country marker or starting area label.
- A clickable home-base node in the home country for `Open Field Kit` access.

Recommended map behavior:

- Start at country zoom.
- Render markers from the static country manifest.
- Reveal tier 0 and tier 1 events immediately.
- Reveal higher-tier events through level progression, completed event chains, tools, and world project unlocks.
- Avoid state/province/county drilldown in v1.
- Show a fixed `Open Field Kit` icon when the player is outside their home country.

### Country Content Package

Each country should have exactly 50 archaeology events in v1.

Suggested per-country distribution:

| Tier | Count | Purpose |
|---|---:|---|
| Tier 0 - Local Leads | 15 | Short, accessible entries that teach the loop. |
| Tier 1 - Regional Patterns | 12 | More connected local/history patterns. |
| Tier 2 - National Threads | 10 | Recognizable national routes, events, institutions, or archives. |
| Tier 3 - Landmark Cases | 7 | Larger famous sites/events with stronger reward tables. |
| Tier 4 - Deep History | 4 | Ancient/canon-heavy or research-frontier entries requiring review. |
| Tier 5 - World Project Hooks | 2 | Country-linked entries that can connect into group world quests. |

This distribution keeps every country playable while preventing low-population or low-source countries from needing county-level detail. Sensitive countries or source-poor countries can use broader cultural, geographic, archival, or route-based events instead of recent local crime. V1 should prefer pre-1900 events and avoid living-memory material.

### Node Sources

Start with these source layers:

- Curated country seed list.
- Natural Earth country geometry and metadata.
- Existing TWB `WorldMapInfluencePointGeneratedCatalog` as optional inspiration for the United States/local tests.
- Wikidata/Wikipedia for notable historical sites and events.
- Library/archive/public-domain sources for higher-tier history.
- Curated internal seed list for major world projects.

The first production content package should not try to research every town dynamically. It should pre-generate and review 50 stable events per country, then serve those events by country manifest.

## Node Tier Design

Tier 0: Local Leads

- Local banks, old roads, cemeteries, courthouses, mills, schools, rail depots, civic buildings, industrial remnants.
- Story scale: "something odd happened here."
- Example: an old bank robbery, lost county ledger, strange survey marker, missing cargo record.
- Timer range: 5-15 minutes per stage.
- Stages: 2-3.
- Rewards: low archaeology materials, small Will, very rare Companion Card chance.

Tier 1: Regional Patterns

- Historical societies, heritage markers, abandoned sites, graveyards, regional infrastructure, old routes, local archives, and culturally specific local patterns.
- Story scale: "the local lead ties into a hidden pattern."
- Timer range: 15-30 minutes per stage.
- Stages: 3-4.
- Rewards: better materials, first useful tool components.

Tier 2: National Threads

- National routes, trade corridors, early settlements, famous archives, museums, courts, ports, rail systems, river systems, and battlefield-adjacent records where appropriate.
- Story scale: "the secret-world connection becomes clear."
- Timer range: 30-60 minutes per stage.
- Stages: 4-5.
- Rewards: tier 2 materials, tool upgrades, moderate Companion Card chance.

Tier 3: Landmark Cases

- Major national historical events, large museums/archives, famous landmarks, known archaeological sites.
- Story scale: "the node affects the national hidden map."
- Timer range: 1-4 hours per stage.
- Stages: 5-7.
- Rewards: high materials, rare research artifacts, Companion Cards.

Tier 4: Ancient Civilizations And Research Frontiers

- Ancient sites, archaeological research, contested interpretations, old-world/canon-heavy nodes.
- Story scale: "deep history intersects the TWB cosmology."
- Timer range: 4-12 hours per stage.
- Stages: 6-8.
- Rewards: high-tier archaeology materials, rare Companion Cards, world project access hooks.

Tier 5: Group World Quests

- Major historical events or global archaeology projects.
- Story scale: "many players commit pets to uncover a server-wide secret."
- Timer range: 6-24 hours per contribution, with multi-day project windows.
- Rewards: contribution-tier rewards, shared unlocks, cosmetics, rare Companion Cards.

## AI Content Generation

### Principle

AI should turn sourced real-world material into structured TWB quest content. It should not invent real facts. It can invent the TWB secret-world interpretation.

V1 history boundary:

- Prefer pre-1900 events by default.
- Avoid living-memory events.
- Do not use living people.
- Ugly history is allowed when handled carefully: sacred sites, burial sites, indigenous history, slavery, genocide, colonial violence, war, and religious trauma should be flagged and treated seriously, not avoided by default.
- Low-tier events should still be meaningful local/regional history, not trivial one-off incidents unless the TWB layer gives them strong significance.
- High-tier events may use aliens, ancient gods, secret labs, fairy courts, Atlantis-style material, major conspiracies, and hidden civilizations when separated clearly from real history.

### Generation Pipeline

1. `NodeCandidateBuilder`
   - Input: country, event index, tier distribution, country source pack, canon rules.
   - Output: country event candidate with stable id.

2. `SourceCollector`
   - Fetches available public facts and source references.
   - For low-tier MVP, this can start with country-level curated seeds, public encyclopedic sources, and safe local-history templates.
   - For higher tiers, require at least one durable source URL or curated source entry.

3. `FactExtractor`
   - Model: `gpt-5.4-nano`.
   - Output: structured facts, dates, people/places, confidence, sensitive-topic flags.

4. `CanonTwistWriter`
   - Model: `gpt-5.4-nano` for tier 0-1.
   - Model: `gpt-5.4-mini` for tier 2-4.
   - Model: `gpt-5.4` for manually approved major world quests if needed.
   - Output: strict JSON matching the node content schema.

5. `SafetyAndToneReview`
   - Flags sensitive real tragedies, sacred sites, recent events, hate/extremism, living people, and legal risk.
   - Low-risk nodes auto-publish.
   - High-risk nodes require manual review.

6. `ContentPersistor`
   - Stores source facts, prompt version, model id, output JSON, content version, and approval state.

7. `NodeServe`
   - Returns stored content only.
   - Never regenerates during a normal player request.

### Pre-Generation And Web Hosting Strategy

For v1, run generation as a pre-generation/admin pipeline, then publish the reviewed output to object storage/CDN:

1. Build the country list.
2. Create 50 candidate event slots per country using the tier distribution.
3. Collect or attach source references for each slot.
4. Generate structured event JSON in batch.
5. Run automated safety/tone/canon checks.
6. Manually review high-risk or high-tier entries.
7. Publish the approved package as `archaeology_world_v1_admin0_50`.
8. Freeze package IDs so player progress can reference stable event versions.

Normal player traffic should never call the model. Player clients pull reviewed content from the web-hosted package. New events arrive through new package versions or season packs.

### Structured Output Schema

Generated node content should include:

- `title`
- `real_history_summary`
- `twb_lore_layer`
- `mission_brief`
- `sensitive_topic_flags`
- `source_fact_ids`
- `stages`
- `mini_game_mix`
- `reward_tags`
- `tool_affinity_tags`
- `pet_affinity_tags`
- `content_rating`

Each stage should include:

- `stage_index`
- `stage_title`
- `stage_brief`
- `timer_seconds`
- `mini_game_type`
- `success_reveal`
- `failure_reveal`
- `mini_reward_table_id`
- `quality_penalty_bps`

## Gameplay Loop

### Start Mission

1. Player selects an available node.
2. Player selects 1-3 available pets.
3. Player optionally equips tools.
4. Server projects pet stats into archaeology stats.
5. Server checks active companion locks.
6. Server checks `WILL` mission cost, tool ownership, and optional tool costs.
7. Server creates mission, charges `WILL`, and locks companions in one transaction.
8. Browser shows timer until first check-in.

Mission cost rule:

- Starting an archaeology mission costs `WILL`.
- The base cost should be affordable.
- Expensive buy-ins are reserved for major world events or high-tier optional content.

### Pet Stat Projection

No pet skills are used in this game. Pet base stats and identity project into archaeology stats.

Example projection:

- Attack -> Dig Power.
- Defense -> Preservation.
- Utility -> Survey Insight.
- Might -> excavation strength bonus.
- Cunning -> clue/cipher bonus.
- Mind -> archive/research bonus.
- Magic -> anomaly interpretation bonus.
- Faith -> burial/ritual site caution bonus.
- Robotics -> survey equipment bonus.
- Cybernetics -> precision tool bonus.
- ArcaneEngineering -> strange mechanism bonus.
- ArcaneFighting -> hazard control bonus.

Pet role still matters, but only as a stat profile. A pet's main-game attack/defense/utility skill does not activate here.

### Stage Check-In

Each mission stage has:

- A minimum wait timer.
- A check-in window.
- A small mini game.
- A mini reward.
- A story reveal.
- A quality adjustment.

Check-in interval targets:

- Tier 0: 5-15 minutes.
- Tier 1: 15-30 minutes.
- Tier 2: 30-60 minutes.
- Tier 3+: 1 hour or longer.

Missing a check-in can either auto-resolve as a weak success or wait indefinitely. Recommended first implementation: wait indefinitely, because it is less punishing and simpler to explain.

### Quality Degradation

Mission quality starts at 100%.

- Perfect check-in: no degradation, possible small bonus roll.
- Minor failure: -5%, possible small `WILL` penalty.
- Major failure: -10%, possible larger `WILL` penalty and tool durability damage.
- Missed optional objective: -2% to -5%.
- Tool/pet mitigation can reduce a limited number of penalties.
- Final quality is clamped between 50% and 100%.

Formula:

```text
final_quality = clamp(10000 - total_penalty_bps + mitigation_bps, 5000, 10000)
```

The final reward table scales quantity and rare-roll weight by final quality. Progress should never fail completely.

### Mini Game Ideas

Grid Brushing

- Player brushes dirt from a grid without over-scrubbing fragile tiles.
- Good for excavation and preservation.

Stratigraphy Sort

- Player orders soil layers or artifact layers correctly.
- Good for reasoning and chronology.

Sieve Sorting

- Player separates relevant finds from debris under time pressure.
- Good for fieldwork and tool bonuses.

Context Mapping

- Player places finds on a site grid from clues.
- Good for survey and recording tools.

Archive Link

- Player links names, dates, places, and symbols from source cards.
- Good for local history nodes.

Inscription Rubbing

- Player traces or reveals marks without crossing damage thresholds.
- Good for ancient/higher-tier nodes.

First MVP should implement only two:

- Grid Brushing.
- Archive Link.

## Rewards

### Reward Types

- Will.
- Common archaeology component materials.
- Tool components.
- Lore fragments.
- Research notes.
- Rare artifact materials.
- Very rare Companion Card drop on final completion.

Reward philosophy:

- Normal rewards are components, not finished usable products.
- Final usable archaeology tools, archaeology-themed skills, and archaeology-themed modifiers are crafted by the player.
- Rare Companion Cards are the exception and can drop at final node completion.
- Archaeology Companion Cards are tradeable by default, but the archaeology client does not expose trade or auction UI.
- Companion Card rewards are safe once earned.
- Companion Card drop text must be source-specific.
- Every material reward records where it came from.
- World Keys, control-node parts, unique companions, named artifacts, and living beings never appear in normal random reward tables.

### Initial Archaeology Materials

Common:

- Pottery sherd.
- Rusted buckle.
- Glass fragment.
- Charcoal sample.
- Field note.
- Map scrap.

Uncommon:

- Stratified sample.
- Maker mark rubbing.
- Survey pin.
- Archive seal.
- Preserved textile.
- Fossilized resin.

Rare:

- Inscribed shard.
- Relic core.
- Anomaly dust.
- Sealed correspondence.
- Old-world mechanism.

These should be normal shared item definitions so future crafting can use them across the main game and other mini games. Country/event specificity belongs in provenance metadata, not in one-off item IDs.

### Companion Card Drops

Companion Card drops should only happen at final node completion.

Rules:

- Low base chance.
- Scales modestly by node tier and final quality.
- Can be weighted by node affinity/type.
- No pet crafting in the archaeology game.
- Dropped Companion Cards enter the shared card inventory.
- Main game can use these Companion Cards after import/sync.
- Companion Cards are tradeable by default.
- Trade/auction actions are only available in the main game.
- All source types are open, including willing bonds, reciprocal bonds, contracts, command-bound records, captured patterns, construct schemas, summon patterns, ritual instructions, recovered records, alien/cryptid/folklore/spirit/monster/animal/construct sources, and stranger event-specific sources.
- Claimed Companion Card rewards are safe once earned.
- Every Companion Card drop must expose `companion_card_source_type`, `companion_card_bond_state`, and a type-specific player-facing drop line.
- Companion Cards should connect to a real potential companion, recorded being, constructable being, summonable being, or entity pattern; avoid empty blueprint rewards with no being attached.

Type-specific drop line examples:

- `bond_record`: "Your World Key resolves a Companion Card from the recovered bond record."
- `summon_pattern`: "Your World Key stabilizes the summon pattern into a Companion Card."
- `captured_pattern`: "Your World Key contains the captured pattern and resolves it into a Companion Card."
- `construct_schema`: "Your World Key compiles the construct schema into a Companion Card."
- `ritual_instruction`: "Your World Key indexes the rite and records a Companion Card from its instructions."

Example initial chance:

```text
Tier 0: 0.05% to 0.10%
Tier 1: 0.10% to 0.25%
Tier 2: 0.25% to 0.50%
Tier 3: 0.50% to 1.00%
Tier 4: 1.00% to 2.00%
World project: contribution-tier based
```

Tune later. The important thing is that Companion Card drops feel exciting but do not make the archaeology game the dominant companion source unless that is intentional.

### Quick Sell

Browser quick sell should be called something like `Field Office Salvage`.

Rules:

- Only sell owned items from the shared inventory.
- No auction access.
- Pay a poor Will rate, such as 10-20% of expected player-market value.
- The Will is paid by a dealer, knowledge broker, trader, or trading house.
- In-world, the player is selling artifacts, field notes, research value, or knowledge.
- Account-bound and special items may be unsellable.
- Every sale writes an inventory ledger row.

## World Projects

World projects are group quests for major historical events and major archaeology themes.

Examples:

- A national archive unlock.
- A famous lost expedition.
- Ancient trade route reconstruction.
- A server-wide dig season.
- A major historical event reinterpreted through TWB canon.

Rule: world projects are optional shared events. They should not introduce a permanent main villain, required campaign track, or single overarching plot for the archaeology game.

Flow:

1. Project appears on the country/world map.
2. Players commit one or more pets for a timed contribution.
3. Committed pets are globally locked.
4. Contributions add progress.
5. Individual rewards are based on contribution tier.
6. Group completion unlocks lore, future nodes, cosmetics, recipes, or new regions.

World projects should have:

- Hard start/end dates.
- Per-player contribution caps.
- Per-companion lock windows.
- Anti-whale reward caps.
- Manual content review.
- Server-wide progress ledger.

## Main Game Integration

The main Unity game and browser game should both use the same backend APIs eventually.

Minimum integration path:

1. Add account login/linking to the Unity game.
2. Upload or migrate local player inventory/pets to shared backend.
3. Main game reads shared inventory and pets on login.
4. Main game respects `companion_locks`.
5. Browser game reads the same inventory and pets.
6. Browser game writes rewards through the shared API.
7. Unity refreshes inventory after browser activity.

Important migration issue:

- The local Unity code has both `CreatureInstance` and creature-card `ItemInstance` concepts. Before browser implementation, define one global pet identity and a stable mapping to current Unity data.

## API Surface

Initial APIs:

`GET /me`

- Returns account/player profile and feature flags.

`GET /me/home-location`

- Returns main-game home location if available.

`POST /me/home-location`

- Stores city-level fallback location.

`GET /inventory`

- Returns shared materials, cards, tools, and wallet.

`POST /inventory/quick-sell`

- Converts allowed items to Will at poor rate.

`GET /pets`

- Returns pets and current lock status.

`GET /archaeology/countries`

- Returns the supported country list and map/content package metadata.

`GET /archaeology/map?country=US`

- Returns visible country events, in-progress missions, claimable missions, world projects, and the map image/tile URL.

`POST /archaeology/content-packs/{packId}/publish`

- Admin/worker call to publish a reviewed web-hosted content pack to object storage/CDN. Not used by normal player traffic.

`POST /archaeology/missions/start`

- Starts mission and locks pets.

`GET /archaeology/missions/{missionId}`

- Returns mission state and next check-in.

`POST /archaeology/missions/{missionId}/attempt`

- Submits mini-game attempt result for validation.

`POST /archaeology/missions/{missionId}/claim`

- Claims final reward and releases pets.

`GET /archaeology/world-projects`

- Lists active group projects.

`POST /archaeology/world-projects/{projectId}/contribute`

- Commits pet/time/resources to a group project.

## Implementation Series

### Series -1 - World Canon Mastersheet And Author Interview

Goal: turn the existing Book 1 material and the author's unwritten rules into a reusable canon source before AI starts generating archaeology content at scale.

Source document:

- `Documentation/TWB_World_Canon_Mastersheet.md`

Tasks:

1. Treat Book 1 release prose as primary canon and marketing/audiobook files as tone and positioning sources.
2. Extract confirmed rules for companions, lockwatch panes, storage, archive, activities, marks, routes, pressure, etiquette, control nodes, and local stewardship.
3. Mark every uncertain system as an open question instead of letting AI invent permanent answers.
4. Interview the author in short sessions for cosmology, companion bonds, lockwatch rules, marks/routes/territory, factions, Will, crafting, archaeology ethics, and content boundaries.
5. Convert answered questions into canon rules with dates and source notes.
6. Use the mastersheet as a required input for all archaeology node prompts and manual review checklists.

Acceptance:

- The mastersheet exists and separates `Confirmed`, `Strong inference`, `Open question`, and `Game-only placeholder` material.
- The first interview pass answers the highest-risk browser game questions: companion terminology, companion card meaning, Will definition, AI canon limits, and low-tier archaeology content rules.
- AI-generated nodes are blocked from inventing global cosmology, ancient civilizations, lockwatch origin, or companion origin until those topics are confirmed.

### Series 0 - Product And Canon Lock

Goal: define enough product truth and canon vocabulary to avoid rebuilding the core later.

Tasks:

1. Done for v1 in `Documentation/Archaeology_V1_Product_Lock.md`: decide story-facing vocabulary for `pet`, `companion`, `companion card`, and lockwatch ownership/permission language.
2. Done for v1 in `Documentation/Archaeology_V1_Product_Lock.md`: decide `Will` vs `SoftCurrency` naming and data shape.
3. Done for v1 in `Documentation/Archaeology_V1_Product_Lock.md`: decide final country list basis.
4. Done for v1 in `Documentation/Archaeology_V1_Product_Lock.md`: decide companion identity mapping and cross-game lock language.
5. Done for v1 in `Documentation/Archaeology_V1_Product_Lock.md`: write content safety/tone rules for real history using the canon mastersheet.
6. Done for v1 in `Documentation/Archaeology_V1_Content_Seed_Spec.md`: define first 20 archaeology item ids.
7. Done for v1 in `Documentation/Archaeology_V1_Content_Seed_Spec.md`: define first 10 tool item ids.
8. Done for v1 in `Documentation/Archaeology_V1_Content_Seed_Spec.md`: define first two mini-game specs.
9. Done for v1 in `Documentation/Archaeology_V1_Content_Seed_Spec.md`: define first 10 country event templates.
10. Done for v1 in `Documentation/Archaeology_V1_Content_Seed_Spec.md`: create the first prompt templates with canon guardrails pulled from the mastersheet.

Acceptance:

- The canon mastersheet is linked and referenced by generation prompts.
- The v1 product lock exists and covers the first five product/canon decisions.
- Shared item ids are stable.
- V1 item/tool IDs, mini-game IDs, event template IDs, and prompt version IDs are stable.
- Companion identity strategy is chosen.
- Low-tier archaeology event rules are approved.
- V1 content package target is fixed at 50 events per country.

### Series 1 - Shared Backend Foundation

Goal: create the platform that all mini games and the main game will use.

Tasks:

1. Create backend service project.
2. Add auth.
3. Add PostgreSQL schema migrations.
4. Add account/profile tables.
5. Add shared wallet/inventory/pet tables.
6. Add inventory ledger.
7. Add companion lock transaction logic.
8. Add API tests for lock conflicts and inventory ledger writes.

Acceptance:

- A player can log in.
- A player can own items and pets.
- A companion can be globally locked.
- A second activity cannot lock the same pet.

### Series 2 - Main Game Sync Contract

Goal: connect existing Unity concepts to backend concepts without building the whole sync UI yet.

Tasks:

1. Done in Series 2: export current Unity item definitions into backend seed data.
2. Done in Series 2: export/map current Companion Card definitions.
3. Done in Series 2: define migration/import endpoint for a local save.
4. Done in Series 2: add read-only API client proof of concept in Unity.
5. Done in Series 2: add lock status read proof of concept in Unity.

Implementation report:

- `Documentation/Backend_Phase2_Implementation_Report.md`

Acceptance:

- Done in Series 2: backend can represent current materials, cards, companions, and Will.
- Done in Series 2: Unity can read lock status for a known companion.

### Series 3 - Browser Shell And Map

Goal: create the playable web app shell.

Tasks:

1. Done in Series 3: create TypeScript/Vite app.
2. Done in Series 3: add login flow.
3. Done in Series 3: add responsive layout.
4. Done in Series 3: add MapLibre map.
5. Done in Series 3: add home-location flow.
6. Done in Series 3: add country map image/tile view.
7. Done in Series 3: add event marker rendering from the country manifest.
8. Done in Series 3: add mission list and inventory/pet summary panels.

Implementation report:

- `Documentation/Backend_Phase3_Browser_Shell_Report.md`

Acceptance:

- Done in Series 3: player can open the browser game on desktop/mobile.
- Done in Series 3: player sees their country map.
- Done in Series 3: player sees available events from the country content manifest.

### Series 4 - Country Content Package And Event Database

Goal: serve stable cached country events from a versioned package before AI automation.

Tasks:

1. Done in Series 4: add archaeology event/node tables using country-centric IDs.
2. Done in Series 4: add event content version tables.
3. Done in Series 4: add event source tables.
4. Done in Series 4: add content-pack manifest tables.
5. Done in Series 4: create a local seed script for one country with 50 hand-authored or placeholder events.
6. Done in Series 4: add web-hosted object-storage/CDN layout for `archaeology_world_v1_admin0_50`.
7. Done in Series 4: add `GET /archaeology/countries`.
8. Done in Series 4: add `GET /archaeology/map`.
9. Done in Series 4: add deterministic visibility rules by player level/progress.

Implementation report:

- `Documentation/Backend_Phase4_Country_Content_Report.md`

Acceptance:

- Done in Series 4: same event id returns same quest content for every player.
- Done in Series 4: events can be versioned without breaking active missions.
- Done in Series 4: country manifests can be fetched on demand and cached by CDN/browser HTTP cache.

### Series 5 - Pre-Generated Web-Hosted Content Package

Goal: generate reusable country event content once, review it, and publish it as a web-hosted package that the game pulls from on demand.

Author update after Series 5:

- Default generation should be Codex-authored static JSON in the repo.
- Do not spend API credits for normal content generation.
- Keep OpenAI provider code optional/parked only.
- Validate Codex-authored packages with `tools/backend/validate-archaeology-package.py`.

Tasks:

1. Done in Series 5: add AI provider abstraction.
2. Done in Series 5: add OpenAI Responses API client.
3. Done in Series 5: add structured output schema.
4. Done in Series 5: add prompt versions.
5. Done in Series 5: add batch pre-generation job runner.
6. Done in Series 5: add country event slot builder for 50 events per country.
7. Done in Series 5: add `gpt-5.4-nano` low-tier generation path.
8. Done in Series 5: add `gpt-5.4-mini` high-tier rewrite path.
9. Done in Series 5: add source/fact extraction persistence.
10. Done in Series 5: add safety/tone review flags.
11. Done in Series 5: add admin review state for high-risk events.
12. Done in Series 5: add content-pack exporter that writes manifests, event JSON, and source manifests to object storage/CDN.

Implementation report:

- `Documentation/Backend_Phase5_PreGeneration_Report.md`

Acceptance:

- Done in Series 5: a country event candidate can generate structured content.
- Done in Series 5: generated content is web-hosted and reused.
- Done in Series 5: normal player requests do not call the model.
- Done in Series 5: failed generation does not block the game; it returns existing published package events.

### Series 6 - Mission Timers And Pet Locks

Goal: make archaeology missions work as semi-idle activities.

Implementation note after the full world package pass:

- Done as a browser-local Series 6 prototype slice: selected nodes can start missions, spend `WILL`, lock the starter companion, show a timer, and claim after the timer resolves.
- Still pending for production Series 6: authoritative backend mission tables/endpoints, server-side companion lock transaction, and claim/release persistence.

Tasks:

1. Add archaeology mission tables.
2. Add mission start endpoint.
3. Add pet selection validation.
4. Add tool selection validation.
5. Create companion lock rows in the same transaction as mission start.
6. Add mission state endpoint.
7. Add claim endpoint.
8. Release companion locks on claim.
9. Add abandoned/expired mission cleanup policy.

Acceptance:

- Player can start a mission with pets.
- Pets become unavailable globally.
- Player can claim after final stage.
- Pets unlock reliably.

### Series 7 - Check-In Mini Games

Goal: add the active browser gameplay layer.

Implementation note, April 26, 2026:

- Done as a browser-local Series 7 prototype slice: active missions now expose staged check-ins from hosted content `miniGameId` values, use deterministic per-stage choices, advance on success or failure, reduce quality only to a 50% floor, grant local stage rewards, and write local ledger rows.
- The prototype supports the 12 generated archaeology mini-game IDs through one reusable browser interaction shell.
- Still pending for production Series 7: Phaser/canvas presentation pass if desired, backend-generated per-stage seed, backend result submission, server-side timing validation, authoritative ledger writes, and authoritative mission stage advancement.

Tasks:

1. Implement Grid Brushing in Phaser.
2. Implement Archive Link in Phaser.
3. Generate server seed per stage.
4. Send mini-game setup from backend.
5. Submit result to backend.
6. Validate score ranges and timing server-side.
7. Apply mini reward.
8. Apply quality penalty or mitigation.
9. Advance stage.

Acceptance:

- Completing a check-in advances the mission.
- Failing a check-in still advances the mission.
- Final quality never drops below 50%.
- Mini rewards write ledger rows.

### Series 8 - Tools And Crafting

Goal: make archaeology rely on craftable tools instead of pet skills.

Implementation note, April 26, 2026:

- Done as a browser-local Series 8 prototype slice: archaeology material definitions, starter field stock, three craftable tool definitions, local recipes, account-bound tool instances, equipment selection, mission start tool requirement, check-in score/quality effects, durability damage, and broken-tool status are now implemented.
- Repair is intentionally absent in v1, and tool cards display the no-trade/no-auction/account-bound policy.
- Still pending for production Series 8: backend crafting endpoint, authoritative tool ownership, authoritative durability and breakage, shared inventory recipe consumption, server-side equipment validation, and server-enforced trade/auction blocking.

Tasks:

1. Seed tool definitions.
2. Seed archaeology material definitions.
3. Seed tool recipes.
4. Add crafting endpoint or reuse shared crafting API.
5. Add tool equipment to mission start.
6. Add tool stat effects.
7. Add tool durability damage and breakage.
8. Block tool repair in v1.
9. Enforce account-bound, no-trade, no-auction tool policy.

Acceptance:

- Player can craft a basic tool.
- Tool affects mission/check-in results.
- Tool can be damaged and eventually broken by mission failure/cost rules.
- Broken tools cannot be repaired in v1.
- Tools cannot be traded or auctioned.
- Tool ownership and durability are server-authoritative.

### Series 9 - Rewards, Companion Cards, And Salvage

Goal: finish the economy loop.

Implementation note, April 26, 2026:

- Done as a browser-local Series 9 prototype slice: final mission claim now grants quality-scaled component rewards by node tier, can roll rare companion card drops into local card inventory, writes final reward/card ledger rows with provenance metadata, and exposes poor-rate component quick-sell for `WILL`.
- Companion cards are marked tradeable only through the main game, while tools/protected items are blocked from browser quick-sell.
- Normal reward tables grant components only, not finished usable products.
- Still pending for production Series 9: backend reward tables, authoritative final-claim transaction, authoritative companion-card inventory, server-side quick-sell endpoint, ledger audit tests, and protected-drop enforcement on the backend.

Tasks:

1. Add reward tables by node tier/type.
2. Add quality scaling.
3. Add Companion Card drop table.
4. Add final claim reward calculation.
5. Add browser quick-sell.
6. Add item binding/trade flags.
7. Add ledger audit tests.
8. Add material provenance metadata to every archaeology grant.
9. Block protected random drops.

Acceptance:

- Stage rewards and final rewards enter shared inventory.
- Pet card drops enter shared card inventory.
- Companion Card drops are tradeable by default, but only through the main game.
- Quick-sell grants poor-rate Will and cannot touch protected items.
- Normal rewards grant components, not finished usable products.

### Series 10 - Group World Projects

Goal: add online shared archaeology projects.

Implementation note, April 26, 2026:

- Done as a browser-local Series 10 prototype slice: seeded world project definitions, project map markers, project detail UI, timed companion contributions, companion/project lock conflict rules, local progress state, progress ledger rows, and local contribution/completion rewards are now implemented.
- Local project progress starts from a simulated baseline so the feature reads like a shared world effort in the prototype.
- Still pending for production Series 10: backend world project tables, shared progress endpoint, multi-player contribution transaction, server-side companion lock logic, admin approval workflow, and authoritative project completion rewards/content unlocks.

Tasks:

1. Add world project tables.
2. Add project map markers.
3. Add contribution endpoint.
4. Add pet commitment/lock logic.
5. Add progress ledger.
6. Add project completion rewards.
7. Add admin content approval.

Acceptance:

- Multiple players can contribute to one project.
- Pets are locked during contribution.
- Completion unlocks shared rewards/content.

### Series 11 - Main Game Full Integration

Goal: make the archaeology browser game and Unity main game feel like one account.

Implementation note, April 26, 2026:

- Done as a browser-local Series 11 integration-contract slice: the Field Kit can link a local Unity player id and generate a versioned `twb.browser.sync.v1` snapshot containing wallet, shared component inventory, companion cards, tools, active companion locks, completed node ids, ledger count, offline revision, and snapshot hash.
- The snapshot is designed as the browser-side counterpart to the existing backend/Unity local-save import and companion-lock status concepts.
- Still pending for production Series 11: real Unity/backend account authentication, backend shared inventory pull, backend shared pet/card pull, Unity-side application of archaeology rewards, server-authoritative companion lock display, inventory refresh endpoint, and merge/conflict resolution for offline browser state.

Tasks:

1. Add Unity login/account link.
2. Add shared inventory pull.
3. Add shared pet pull.
4. Add companion lock display in Unity.
5. Add inventory refresh after browser activity.
6. Add conflict handling for local/offline saves.
7. Add migration tooling for existing players.

Acceptance:

- A companion sent on browser archaeology is unavailable in Unity.
- A reward earned in browser appears in Unity inventory.
- A Companion Card dropped in browser can be used in Unity.

### Series 12 - Hardening And Launch

Goal: make it safe enough for real players.

Implementation note, April 26, 2026:

- Done as a browser-local Series 12 hardening prototype slice: high-impact action rate limits, local telemetry events, local abuse flags, backup snapshot creation, state hashing, privacy notes, and AI-spend status are now visible in the Field Kit audit surface.
- Telemetry is recorded for mission starts, check-ins, claims, quick-sell, tool craft/equip, project contribution, project claim, sync snapshot export, and backup creation.
- Still pending for production Series 12: server-side rate limiting, real bot detection, abuse dashboards, durable telemetry storage, backup/restore drills, backend reward audit queries, formal location privacy/legal review, and content review queue operations.

Tasks:

1. Add rate limiting.
2. Add bot/automation detection for check-ins.
3. Add abuse dashboards.
4. Add pre-generation spend caps.
5. Add event-generation review queue.
6. Add backups and restore drills.
7. Add telemetry for mission starts, completions, failures, rewards, and companion locks.
8. Add legal/privacy review for location data and historical content.

Acceptance:

- AI costs are capped.
- Economy changes are auditable.
- Location data has clear precision and retention rules.
- Reward exploits can be investigated from ledger data.

### Series 13 - Backend Browser Sync Intake

Goal: begin converting the browser prototype into production-shaped backend authority.

Implementation note, April 26, 2026:

- Done as a backend foundation slice: added a `twb.browser.sync.v1` import model, `ImportBrowserSyncSnapshot` store contract, in-memory intake implementation, wallet/inventory/card/tool import, browser companion lock import, completed-event passthrough, snapshot metadata preservation, and duplicate snapshot idempotency.
- Backend tests now verify that browser sync imports wallet, inventory, card rows, tool rows, active locks, ledger metadata, completed event ids, and that replaying the same snapshot hash does not duplicate rewards.
- Still pending for production Series 13: HTTP endpoint, authentication, request signing, server-side snapshot hash verification, delta/absolute reconciliation policy, persistent database tables, companion id mapping table, and real conflict resolution against Unity/main-game state.

Tasks:

1. Add browser sync import DTOs.
2. Add platform-store sync import contract.
3. Import browser wallet and shared inventory rows.
4. Import companion-card and tool inventory rows.
5. Import browser companion locks.
6. Preserve browser provenance metadata in ledger rows.
7. Reject or no-op duplicate snapshot hashes.
8. Add backend tests.

Acceptance:

- Browser sync snapshots can be ingested by backend foundation code.
- Duplicate snapshot imports do not duplicate rewards.
- Active browser companion locks become backend lock rows.
- Imported browser rewards are auditable from ledger metadata.

## MVP Scope Recommendation

Build the smallest version that proves the architecture:

1. One country vertical slice: United States.
2. One custom country map image or temporary styled map placeholder.
3. 50 country events in the final v1 format.
4. 3 event tiers for the first playable country package.
5. 2 mini games.
6. 10 archaeology materials.
7. 5 tools.
8. 1-3 pet mission assignment.
9. Global companion locks.
10. Stage rewards, final rewards, and rare Companion Card drop.
11. No auction.
12. Quick-sell only.
13. AI generation behind an admin/dev pipeline, not live player traffic.
14. Content package manifest shaped like the future worldwide package.

This proves the shared backend, companion locks, inventory write path, country map/event path, and web-hosted content package path without trying to build the whole world package at once.

World v1 production target after the slice:

- 50 events per country.
- 258 Natural Earth Admin-0 records if using the full map baseline.
- 12,900 total events.
- 258 high-resolution country maps.
- Package name: `archaeology_world_v1_admin0_50`.

## Key Risks

### Scope Explosion

The idea can grow forever. Keep the first slice to one country map, 50 events, three tiers, two mini games, and web-hosted package serving.

### Economy Exploits

Browser games are easier to automate and tamper with. All rewards must be calculated server-side.

Archaeology should be net-positive in `WILL` over time, but equivalent time spent in archaeology must not exceed the main game's home defense/idle economy. Mini-games should feel meaningful inside archaeology without becoming mandatory for main-game competition.

### Pet Identity Confusion

Current Unity systems include creature instances and creature-card item instances. Pick one global pet id before the browser game goes too far.

### AI Cost Growth

Never generate on every play. Pre-generate through the admin pipeline, review, publish a web-hosted package, and serve event JSON during gameplay.

### Historical Content Tone

Real events can involve victims, sacred places, war, race, religion, colonial violence, and living communities. The content policy needs to exist before broad generation.

### Location Privacy

City-level location is enough. Avoid asking for exact GPS unless a future feature truly needs it.

## First Development Milestone

Milestone: "Archaeology Vertical Slice"

Deliverables:

1. Backend account with one test player.
2. Shared Will wallet.
3. Shared inventory with archaeology materials.
4. Shared pet list with three test pets.
5. Pet lock table and transaction.
6. Browser map centered on city/country.
7. Five seeded archaeology events from the country manifest.
8. Start mission with one pet.
9. One 5-minute timer.
10. One Grid Brushing check-in.
11. Mini reward grant.
12. Final reward claim.
13. Pet unlock.
14. Ledger entries for every inventory/currency change.

Once this works, every other mini game can copy the same spine.

## Source Notes

- OpenAI model and pricing guidance checked against official OpenAI API docs on 2026-04-25.
- OpenAI structured outputs should be used for event JSON so generated content matches the backend schema.
- OpenAI Batch API is appropriate for non-urgent pre-generation because it provides lower-cost asynchronous processing.
- MapLibre GL JS is suitable for a browser country map with vector tiles, markers, sources, and layers.
- Public Nominatim should not be treated as a production geocoding/autocomplete service; use it only within its policy limits or self-host/use a provider.
