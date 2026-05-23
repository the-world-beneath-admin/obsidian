# 2026-05-16 TWB Trenchworks Crafting Logistics Trade-Off Addendum

## Scope

Standalone Unity 2D TWB Trenchworks prototype under The World Beneath umbrella.

This is a design-only refinement to `2026-05-16-twb-trenchworks-crafting-logistics-design-report.md`. No code was implemented. No permanent memory, wiki, index, hot, or log files were edited.

Design refinement: each crafting tier should produce some goods that can be sent directly to the front and some goods that are better reserved for higher-tier crafting. The player should constantly choose between feeding the war now and withholding material to build more complex weapons, logistics, and siege capacity later.

## 1. Tier-by-tier split: frontline outputs vs upward-crafting outputs

### Tier 1 - Hand War Economy

Frontline outputs:

- Loose Cartridges: weak but immediate ammunition for scouts and rifle units.
- Basic Rations: keeps porters, scouts, and trench holders moving.
- Field Dressings: reduces early casualty loss.
- Sandbag Bundles: lets units dig shallow cover and stabilize first contact.
- Replacement Bodies: low-training manpower to keep the line populated.
- Hand Tools: slow obstacle clearing and primitive digging support.

Upward-crafting outputs:

- Black Powder Batches: reserved for Tier 2 Ammo Crates and later shell chains.
- Planks and Crate Boards: reserved for conveyors, crate packaging, depots, and Tier 2 construction flow.
- Sterile Cloth Rolls: reserved for Medical Crates and later hospital chains.
- Meal Tins: reserved for Ration Crates and organized replacement pipelines.
- Recruit Rolls: reserved for trained squads instead of raw replacement bodies.
- Sorted Scrap: reserved for presses, wire, boilers, and machine parts.

Tier 1 rule: early goods should always have an ugly but useful frontline version and a cleaner reserve version. The player can survive by shipping hand goods, but cannot industrialize if every plank, ration, and powder batch is thrown into the mud.

### Tier 2 - Belted Workshop Line

Frontline outputs:

- Ammo Crates: reliable rifle and machine-gun supply.
- Ration Crates: front endurance and morale support.
- Medical Crates: better casualty recovery than field dressings.
- Trench Material Crates: wire, planks, sandbags, duckboards, and brace kits.
- Boiler Fuel: keeps local front equipment and support stations operating.
- Wire Coils: immediate defensive obstacle and trench-holding value.

Upward-crafting outputs:

- Powder Kegs: reserved for Tier 3 Shell Forge and explosives.
- Pressed Casings: reserved for shell and fuse chains.
- Steam Fittings: reserved for Tier 3 engine houses and powered loaders.
- Cable Spools: reserved for signal benches, relays, and later command systems.
- Treated Timber Frames: reserved for concrete forms, bulk docks, and heavy works.
- Packed Medical Stock: reserved for Field Hospital Kits.

Tier 2 rule: conveyors make volume possible, but volume creates temptation. The player should feel clever for reserving material, and nervous because the front is asking for those exact goods.

### Tier 3 - Steam Yard And Chemical Works

Frontline outputs:

- Shell Crates: direct artillery support and suppression.
- Replacement Squads: trained infantry, engineers, medics, or sappers.
- Field Hospital Kits: wounded-return capacity and morale stabilization.
- Concrete Revetment Packs: stronger trench and base-cell durability.
- Signal Kits: better reinforcement routing and local unit coordination.
- Repair Kits: keeps machines, depots, support tools, and war equipment active.

Upward-crafting outputs:

- Fuse Assemblies: reserved for Tier 4 heavy shells and Tier 5 siege goods.
- Chemical Reagents: reserved for advanced explosives, medicine, and binding works.
- Steam Cells: reserved for Tier 4 bulk transport and robotics support.
- Uniform Kits: reserved for trained replacements and command-ready squads.
- Precision Gears: reserved for automata, rangefinders, and relay systems.
- Reinforced Frames: reserved for bulk hauler docks, siege presses, and vault machinery.

Tier 3 rule: this is the first major strategic fork. Shipping shells and squads now wins local fights; reserving fuses, steam, and precision parts builds the machine that can eventually destroy the enemy base.

### Tier 4 - Arcane Industrial Works

Frontline outputs:

- Heavy Shell Crates: strong bombardment and fortified-position damage.
- Engineer Automata Packs: faster obstacle clearing, repair, and trench work.
- Obstacle-Clearing Charges: breaks wire, rubble, and bunker obstructions.
- Command Relay Kits: better scout response, reinforcement timing, and coordinated assaults.
- Aether Batteries: front energy for searchlights, relays, and support machines.
- Stabilized Energy Canisters: safer late-war energy supply.

Upward-crafting outputs:

- Siege-Grade Casings: reserved for Tier 5 Siege Shells.
- Bound Charge Cores: reserved for Base-Breach Charges.
- Targeting Lenses: reserved for Harmonic Rangefinders.
- Ward Plates: reserved for safe volatile storage and bombardment stabilization.
- Heavy Servo Frames: reserved for advanced automata and siege support.
- Command Authority Seals: reserved for War Choir, final bombardment control, and high-tier coordination.

Tier 4 rule: the TWB twist becomes a real choice here. Aether and robotics can save the front immediately, but the same parts are required for the victory machinery. Magic should not be a free answer; it should be a terrible budget meeting with sparks.

### Tier 5 - Siege Engine And Binding Works

Frontline outputs:

- Siege Shells: heavy front bombardment and defensive breakthrough.
- Heavy Automata Service Packs: keeps late robotics and obstacle teams working.
- Strategic Ration Reserves: supports long offensives and collapse prevention.
- War Choir Pulses: temporary coordination boost across active sectors.
- Emergency Stabilized Energy: prevents late front machinery from stalling.
- Base Repair Vault Loads: protects the player's 10x10 base area from enemy pressure.

Final-annihilation reserve outputs:

- Base-Breach Charges: direct enemy-base destruction package.
- Stabilized Bombardment Cores: required to damage enemy base integrity reliably.
- Harmonic Targeting Kits: reduces wasted bombardment and seeded miss variance.
- Sealed Siege Lots: bundled shells, charges, energy, and targeting for planned bombardment windows.
- Commanded Offensive Stockpiles: food, ammo, medical, energy, and bodies reserved for a major push.
- Binding-Safe Victory Stores: warded late goods that prevent final-chain instability.

Tier 5 rule: there is no Tier 6, so the upward-crafting equivalent is final annihilation assembly. The player chooses between spending Tier 5 output to keep the front from buckling and reserving it for a coordinated base-kill window.

## 2. Decision pressure at each tier

Tier 1 pressure:

- Send now: scouts live longer, early contacts are less punishing, and porters keep moving.
- Reserve: belts, crates, depots, ammo crates, and stable recipe chains arrive sooner.
- Failure mode: over-shipping to front creates a brave, hungry mess with no industrial future; over-reserving makes the opening war feel abandoned.

Tier 2 pressure:

- Send now: the front gets reliable ammo, food, medical, and trench supplies.
- Reserve: Tier 3 shells, hospitals, steam power, and trained squads unlock sooner.
- Failure mode: conveyors can make the player believe throughput is solved while the actual problem is allocation.

Tier 3 pressure:

- Send now: local fights improve, wounded return, trenches harden, and enemy pressure slows.
- Reserve: Tier 4 robotics, bulk transport, command relays, and heavy bombardment come online.
- Failure mode: Tier 3 can become the comfort tier unless the enemy eventually demands heavier tools.

Tier 4 pressure:

- Send now: the front gains powerful support and can clear obstacles or hold captured cells.
- Reserve: Tier 5 siege systems, final base-breach packages, and late command control become possible.
- Failure mode: aether must not become universal soup. If it solves everything, the rest of the economy becomes decorative.

Tier 5 pressure:

- Send now: prevent late collapse, support grand offensives, and keep advanced systems alive.
- Reserve: assemble a reliable bombardment window that can actually annihilate the enemy base.
- Failure mode: if final assembly is too slow, the player hoards forever; if it is too cheap, the war ends like a damp firework.

## 3. Example trade-off chains

Ammo-to-siege chain:

```text
Scrap + Niter + Sulfur
  -> Loose Cartridges sent to front
      Immediate: scouts fight and retreat less often.
      Cost: fewer powder batches for higher production.
  -> Black Powder reserved
      Tier 2: Ammo Crates
      Tier 3: Shell Crates
      Tier 4: Heavy Shell Crates
      Tier 5: Siege Shells / Base-Breach Charges
```

Food-to-manpower chain:

```text
Grain + Water
  -> Basic Rations sent to front
      Immediate: lower fatigue, better scouting range, fewer morale breaks.
      Cost: fewer organized rations for trained replacements.
  -> Meal Tins reserved
      Tier 2: Ration Crates
      Tier 3: Replacement Squads / Field Hospital support
      Tier 5: Strategic Ration Reserves for major offensives
```

Construction-to-entrenchment chain:

```text
Timber + Cloth + Stone
  -> Sandbags and hand tools sent to front
      Immediate: units dig shallow cover after contact and hold cells longer.
      Cost: fewer planks, forms, and frames for factory expansion.
  -> Planks / Treated Timber Frames reserved
      Tier 2: Belts, depots, trench material crates
      Tier 3: Concrete forms and revetment packs
      Tier 4: Bulk hauler docks
      Tier 5: Siege press infrastructure
```

Medical-to-recovery chain:

```text
Cloth + Medicinal Fungus + Water
  -> Field Dressings sent to front
      Immediate: early casualties are less final.
      Cost: fewer sterile rolls for better medical systems.
  -> Sterile Cloth Rolls reserved
      Tier 2: Medical Crates
      Tier 3: Field Hospital Kits
      Tier 5: Offensive stockpile casualty buffer
```

Command-to-bombardment chain:

```text
Copper + Aether + Clockwork Salvage
  -> Signal Kits / Aether Batteries sent to front
      Immediate: better response to contact and powered support.
      Cost: fewer relays and targeting parts for base destruction.
  -> Cable Spools / Aether Batteries / Targeting Lenses reserved
      Tier 3: Signal Kits
      Tier 4: Command Relay Kits
      Tier 5: Harmonic Targeting Kits and controlled bombardment
```

Bodies-to-specialists chain:

```text
Mustered Recruits + Food + Cloth
  -> Replacement Bodies sent to front
      Immediate: empty cells refill and losses hurt less.
      Cost: replacements are weak, hungry, and poorly coordinated.
  -> Recruit Rolls / Uniform Kits reserved
      Tier 3: Rifle Squads, Engineer Squads, Medics, Sappers
      Tier 4: Automata-supported engineers
      Tier 5: Commanded offensive stockpiles
```

## 4. Suggested UI indicators for "send to front" vs "reserve for crafting"

Recommended item/depot controls:

- Every dual-use output should show two destinations: `Front` and `Craft Reserve`.
- Depots should support simple allocation buttons first: `Front`, `Reserve`, `Split`.
- Later depots can support percentage allocation, reserve floors, and emergency overrides.
- Storage should show "reserved amount" separately from "available to ship" so the player does not think goods vanished.

Recommended visual language:

- Front icon: helmet, bayonet, shell burst, or forward arrow.
- Craft reserve icon: gear, crate stack, upward arrow, or locked-tier badge.
- Contested item icon: split arrow showing that the item has both immediate and future value.
- Warning color: red for front starvation, amber for contested allocation, blue/steel for crafting reserve.

Recommended tracker fields:

- War need now: current requested goods by category.
- Reserved for next tier: goods withheld for higher recipes.
- Shortage consequence: what happens if the front does not receive the item.
- Upgrade consequence: what unlocks if the item remains reserved.
- Time to front trouble: rough countdown before starvation/fatigue/ammo shortage matters.
- Time to craft target: rough countdown before the next machine, recipe, or siege package is ready.

Example UI text:

- "Ammo Crates: 72 front / 40 reserved for Shell Forge."
- "Rations starving front in 38 ticks. Reserve unlocks Replacement Squad in 55 ticks."
- "Aether Battery contested: Command Relay needs 3; front searchlights need 2."
- "Emergency front shipment will delay Heavy Shell chain."

## 5. Balancing risks

- If front shipment is always correct, the crafting tiers become fancy decoration.
- If reserve crafting is always correct, the war becomes a background timer the player ignores.
- If withholding goods causes sudden catastrophic collapse, the player will feel ambushed rather than strategically punished.
- If every item is dual-use, the UI becomes tax paperwork with bayonets. Limit the most painful decisions to a few key goods per tier.
- If aether substitutes for too many resources, the WW1 logistics identity dissolves.
- If bodies are cheap, the war becomes spam. If bodies are too costly, recovery feels impossible. Bodies should require food, kit, and command capacity.
- If bulk transport arrives too early or without category limits, it trivializes the 250x250 factory layout.
- If Tier 5 final assembly requires too many invisible prerequisites, the player will not understand why victory is stalled.
- If the NPC enemy pressure does not escalate, players will comfortably hoard upward goods and never feel the war-now half of the decision.
- If diagnostics do not explain shortages, players will blame randomness instead of their logistics choices.

## 6. Recommended first implementation slice

Do not build the entire five-tier economy at once. The first slice should prove the allocation decision, not the whole cathedral. Very noble restraint, naturally.

Recommended slice:

1. Add the concept of dual-use outputs to the design data: each key output can have a frontline use and an upward-crafting use.
2. Start with six contested goods:
   - Loose Cartridges: front ammo now or Black Powder reserve.
   - Basic Rations: front stamina now or Ration Crate / manpower reserve.
   - Field Dressings: front casualty reduction now or Medical Crate reserve.
   - Sandbag Bundles / Planks: front cover now or factory/conveyor construction reserve.
   - Ammo Crates: front firepower now or Shell Forge reserve.
   - Aether Batteries: front energy now or Command Relay / siege reserve.
3. Add a depot allocation mode for each contested category: `Front`, `Reserve`, or `Split`.
4. Add a right-panel diagnostic showing:
   - amount sent to front,
   - amount reserved,
   - current front consequence,
   - next crafting consequence.
5. Keep conveyors as Tier 2 and preserve the current working prototype loop while progression is still being shaped.
6. Make the war consume the immediate side of the split before adding new late-tier machines:
   - low ammo reduces contact performance,
   - low food increases fatigue,
   - low medical increases permanent casualty loss,
   - low construction slows digging and weakens trenches.
7. Add only one upward chain at first:
   - Loose Cartridges / Black Powder -> Ammo Crates -> Shell Crates.
8. Once that is readable, add one non-ammo chain:
   - Basic Rations -> Ration Crates -> Replacement Squads.
9. Only after those two chains feel understandable should Tier 4 aether and Tier 5 bombardment reserves be added.

First pass success criteria:

- The player can see why sending goods to the front helps immediately.
- The player can see what future craft is delayed by sending those goods.
- The front can suffer from under-supply without instantly ending the run.
- At least one stronger output requires the player to reserve goods instead of always shipping everything.
- The UI makes the trade-off visible without opening a spreadsheet outside the game, because we do have standards.

## Context sources read

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-crafting-logistics-design-report.md`

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-crafting-logistics-tradeoff-addendum.md`

## Checks run

- Read the existing crafting/logistics report and required project memory context.
- Confirmed this pass is design-only and did not edit Unity source or permanent memory.

## Cleanup performed

No temporary files, screenshots, logs, or throwaway artifacts were created.

## Anything blocked

Nothing blocked.
