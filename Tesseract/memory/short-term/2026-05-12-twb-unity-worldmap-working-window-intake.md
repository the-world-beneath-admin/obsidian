# Working Window Intake - 2026-05-12 - TWB Unity Worldmap

## Project Identity
- Project/window name: TWB Phase 1 Idle Prototype - Unity world map, territory overlay, UI conversion, and starter guardian pets
- Main goal: Convert core TWB UI/world map systems to the new HoloGlyph/field-tablet style while replacing heatmap-style dungeon/territory presentation with clustered territory nodes, routes/lanes, and node dungeon interaction.
- Scope: Unity UI builders, world map territory overlay, node dungeon/inspect dungeon windows, crafting/activity/home-defense UI surfaces, starter guardian creature/card/skill content validation.
- Code/project directory: C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype
- Related Obsidian lane, if known: TWB Unity / world map / UI / starter pets
- Suggested future worker role name: twb-unity-starter-pet-and-worldmap-steward

## Current State
The project has undergone a large interactive Unity UI pass. Several crafting, activities, home-defense, world-map navigation, and dungeon-related screens were moved toward the new HoloGlyph/field-tablet visual language. The world map territory overlay has been substantially reworked away from heatmap-style spawning toward clustered display-owner nodes, influence fields/rims, routes/lanes, and node-level dungeon interaction.

The world map overlay is functional but still not final. Clusters now appear to collapse more properly into town/display-owner summaries, and node dungeon interaction has a first functional movable subwindow. Remaining world map concerns include route/lane completeness, line readability, hiding collapsed town markers, and polishing the node dungeon and inspect dungeon windows.

Starter guardian pets Peggy and Stanly were partially wired by another Codex window and caused catalog validation failures. The immediate validation blockers were fixed locally: cards now resolve to known creatures, Peggy/Stanly are high-end Tier 1 Legendary creatures within tier bounds, and their skills declare valid A-Series affinities. Build passed after the latest fix.

Implementation is now intentionally paused for Bob/orchestrator review.

## Files And Areas Touched
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/UnityBridge/UI/Builders/WorldMapSurfaceBuilder.cs
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/UnityBridge/UI/WorldMapTownPresentationPlan.cs
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/UnityBridge/UI/Widgets/
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/UnityBridge/UI/UiCommon/FieldTabletWindowTemplate.cs
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Services/WorldMapService.cs
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/UIBoundary/WorldMapUiSnapshot.cs
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/WorldMap/
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/WorldMapDungeons/
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Services/WorldMapDungeons/
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/Creatures/Catalog/CreatureCatalogAuthority.cs
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/Taxonomy/FamilyMetadataRules.cs
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/Creatures/Definitions/C_Special_EphemrialSpirit_Peggy.cs
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/Creatures/Definitions/C_Special_EphemrialSpirit_Stanly.cs
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/Creatures/StarterPets/StarterPetCatalog.cs
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/Domain/Items/Definitions/PetCreatureCardDefinitionBase.cs
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/Domain/Items/Definitions/CARD_Companion_Special_EphemrialSpirit_Peggy.cs
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/Domain/Items/Definitions/CARD_Companion_Special_EphemrialSpirit_Stanly.cs
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/Skills/Catalog/Definitions/SkillDef_PeggyThresholdWard.cs
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/Skills/Catalog/Definitions/SkillDef_StanlyPrancingBite.cs
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/Skills/UtilitySkillCatalog.cs
- C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/Skills/Attack/Catalog/AttackSkillCatalog.cs
- C:/Users/yrred/Desktop/HOLO_GLYPH_WINDOW_CONVERSION_HYDRATION.md
- Territory planning/user reference markdowns: TERRITORY_OVERLAY_IMPLEMENTATION_PLAN_2026-05-07.md, TERRITORY_SYSTEM_FUTURE_WORK_PLAN_2026-05-07.md, territory_overlay_visual_direction.md, UI_ROADMAP_MASTER_v7.md

## Decisions Made
- Decision - Do not add `special_ephemrial_spirit` to the global biome registry just to satisfy starter pets.
- Source - Starter pet validation fixes; special starter identity is kept in starter metadata while regular biome/family taxonomy remains canonical.

- Decision - Do not weaken tier/stat/skill validators to make Peggy or Stanly pass.
- Source - Starter pet fixes were made by correcting creature/card/skill data and catalog initialization behavior.

- Decision - Special protected starter creatures may skip regular biome/family slice validation, but still must pass creature envelope, tier, and skill affinity contracts.
- Source - `CreatureCatalogAuthority` and `FamilyMetadataRules` changes.

- Decision - Peggy is a Faith utility starter; Stanly is a Might attack starter.
- Source - Peggy Threshold Ward and Stanly Prancing Bite affinity fixes.

- Decision - Starter guardians should be high-end Tier 1 Legendary creatures, not over-tier stat outliers.
- Source - User instruction and subsequent creature envelope/card rarity fixes.

- Decision - World map territory display should collapse raw anchors into display-owner/town summaries.
- Source - World map clustering work and user confirmation that clusters finally collapsed properly.

- Decision - Folded child anchors should become owner badges/intensity instead of independent map clutter.
- Source - World map visual policy/owner presentation work.

- Decision - Territory connections should attach to display owners, not raw/folded child anchors.
- Source - Route/lane diagnosis and clustering fixes.

## Memory-Worthy Facts
- Fact - The new UI visual language uses cyan outlines/title/dropdown/info areas, orange slot outlines, and reduced/faded cyan fills for slot backgrounds.
- Source - Repeated UI conversion directives across crafting, activities, and node dungeon windows.

- Fact - The project uses a HoloGlyph/field-tablet visual style with large sci-fi frames, cyan glow, orange accents, and functional dense tool panels rather than landing-page style UI.
- Source - User UI feedback and converted window passes.

- Fact - World map region/area modes should show owner summaries rather than every folded dungeon/anchor as a standalone object.
- Source - World map visual stack/presentation policy request.

- Fact - Visible town label should act as the display owner; standalone owner node/marker should be suppressed when it duplicates a visible label.
- Source - User-provided implementation direction for owner presentation plan.

- Fact - Node dungeon interaction should open a movable subwindow summarizing available dungeons at the clicked node.
- Source - User design direction after clustering appeared functional.

- Fact - Peggy and Stanly are "guardian angel" starter pets, despite file ids currently spelling the family as `ephemrial`.
- Source - User clarification and starter pet fixes.

- Fact - The misspelling `ephemrial` exists in ids and file names; do not casually rename it without a migration.
- Source - Existing starter pet ids/files and validation errors.

## Risks / Warnings
- Warning - The Unity git worktree is heavily dirty with many unrelated or generated changes. Do not blindly revert, reset, or stage everything.
- Warning - Several files appear untracked while still being important to compile/runtime behavior. Review carefully before committing.
- Warning - World map route/lane presentation is still not final; further changes need focused diagnosis rather than more vague "lever pulling."
- Warning - Unity static initialization can leave stale catalog state after validation exceptions until a domain reload/play-mode restart.
- Warning - Node dungeon and inspect dungeon windows are functional but not visually finished.
- Warning - Starter pet "special affinity" and combat A-Series affinity are separate concepts; skills still need exactly one A-Series `PrimaryAffinity`.
- Warning - `TWB.Domain.csproj` and generated content folders may include broad churn from other workers.

## Open Questions
- How many guardian angel starter pets are planned, and what are their intended A-Series affinities and combat roles?
- Should Legendary starter companion cards receive a bespoke UI badge/treatment beyond `ItemRarity.Legendary`?
- Should guardian starters continue using regular Tier 1 envelopes or eventually get a named special Tier 1 legendary template?
- What is the final rule for world map long-range route connectivity between display-owner nodes?
- Should collapsed towns hide all town text/markers or keep labels only for major named owners?
- What is the final visual target for the node dungeon and inspect dungeon subwindows?

## Do Not Promote
- Do not promote the many failed UI "lever" attempts as design doctrine.
- Do not promote GPT Pro handoff prompts or analysis drafts as canonical unless Bob reviews them first.
- Do not promote temporary debug colors, layer toggles, visual attribution names, or diagnostic counters as permanent product language.
- Do not promote screenshots as final UI specs unless Bob explicitly curates them.
- Do not promote angry/frustrated wording from live debugging into permanent memory.

## Current Blockers
- Active implementation is paused for this Obsidian short-term intake.
- Bob/orchestrator needs to review this report before permanent memory or next worker assignment.
- Unity should be reloaded/retested after the latest Peggy/Stanly affinity fixes to confirm the world map opens cleanly in-editor.

## Checks Run
- Ran `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` multiple times during starter pet fixes.
- Latest known build after Peggy/Stanly affinity fixes succeeded with 0 errors and 4 warnings.
- Remaining warnings included existing unreachable code and unused/unassigned fields in UI/config areas.
- Used search checks for Peggy/Stanly special starter references and Unknown affinities during fixes.
- Used manual Unity editor screenshots/error output from the user as visual/runtime verification.

## Cleanup Needed
- Review the dirty Unity worktree and separate intentional changes from unrelated/generated churn.
- Review untracked UI/world-map/starter-pet files before any commit.
- Inspect diagnostic/output/tmp folders later if cleanup is requested; do not delete now.
- Node dungeon window frame/list sizing and inspect dungeon styling need another focused polish pass.
- Route/lane graph and presentation should get a focused verification pass after memory migration.

## Recommended Obsidian Tree
- memory/wiki/twb-unity/overview.md
- memory/wiki/twb-unity/world-map-territory-overlay.md
- memory/wiki/twb-unity/starter-pets-guardian-angels.md
- memory/wiki/twb-unity/ui-hologlyph-style.md
- memory/wiki/twb-unity/decisions.md
- memory/wiki/twb-unity/open-questions.md
- memory/reports/twb-unity/
- memory/short-term/

## Recommended Worker Agent
- Agent name: twb-unity-starter-pet-and-worldmap-steward
- Purpose: Continue TWB Unity world map/UI work while guarding content validation contracts for starter guardian pets.
- Read-first files: C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/UnityBridge/UI/Builders/WorldMapSurfaceBuilder.cs; C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Services/WorldMapService.cs; C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/UIBoundary/WorldMapUiSnapshot.cs; C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/Creatures/Catalog/CreatureCatalogAuthority.cs; C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/Creatures/StarterPets/StarterPetCatalog.cs; C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/Creatures/Definitions/C_Special_EphemrialSpirit_Peggy.cs; C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/Domain/Creatures/Definitions/C_Special_EphemrialSpirit_Stanly.cs; territory/UI roadmap markdowns listed above.
- Allowed write paths: C:/Users/yrred/Desktop/Unity/TWB_Phase1_IdlePrototype/Assets/_TWB/Scripts/; relevant Unity UI assets only after review; C:/Users/yrred/Desktop/Obsidian/Tesseract/memory/short-term/ for reports.
- Forbidden write paths: C:/Users/yrred/Desktop/Obsidian/Tesseract/memory/wiki/; C:/Users/yrred/Desktop/Obsidian/Tesseract/memory/index.md; C:/Users/yrred/Desktop/Obsidian/Tesseract/memory/hot.md; C:/Users/yrred/Desktop/Obsidian/Tesseract/memory/log.md; unrelated generated creature/enemy/card bulk files unless explicitly assigned; destructive git operations.
- Done criteria: Build passes; Unity world map opens without validation errors; starter pets remain high-end Tier 1 Legendary guardian angels; no validator bypasses; next visual change is isolated and verified.
- Report destination: memory/short-term/

## Next Recommended Gate
Bob/orchestrator should review this intake, decide what becomes permanent memory, then choose one next work lane: either harden/test starter guardian pet creation contracts or resume focused world-map route/lane and node-dungeon UI cleanup.
