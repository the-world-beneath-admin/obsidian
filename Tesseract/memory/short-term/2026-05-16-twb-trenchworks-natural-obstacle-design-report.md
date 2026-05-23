# TWB Trenchworks Natural Obstacle Design Report

Date: 2026-05-16

Superseded note: this report is superseded for implementation direction by `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-simplified-cover-map-props-report.md`. The revised direction uses a simpler posture, cover, concealment, and movement model and removes ricochet/deflection-style terrain effects.

Scope: standalone TWB Trenchworks Unity 2D prototype at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

This is a design-only worker report. No Unity source code was edited.

## Design Intent

The war map is a 600 x 1000 semi-2D tactical grid where squads scout, shoot at range, dig in, and connect trenches over time. Natural placements should make the front feel discovered rather than drawn: sightlines break, squads find small footholds, engineers value certain ground, and large features bend the eventual trench network.

Important implementation pushback: the current prototype has only broad obstacle buckets such as rubble, wire, crater, and ruin. The 40 placements below should be data-driven definitions that output cell effects. The first implementation can bucket them into existing cover/movement behavior, but the long-term shape should not be 40 hard-coded enum cases.

## Cover And Effect Scale

- Negative cover: `-0.05` to `0.00`, exposed or hazardous ground.
- Light cover: `0.08`, concealment or tiny firing posture advantage.
- Half cover: `0.18` to `0.26`, meaningful protection but still vulnerable.
- Full cover: `0.38`, strong position before constructed trenches.
- Hard cover: `0.50` maximum for rare natural rock or bone features; should still be weaker than a mature trench plus fortification.
- Movement: `normal`, `slow`, `verySlow`, `blockedWithGaps`, or `hazard`.
- LoS/fire: `none`, `conceal`, `partialBlock`, `block`, `rangePenalty`, or `aimPenalty`.

## Forty Natural Obstacle/Placement Definitions

| # | Name | Visual grid idea | Footprint / shape rules | Size range | Cover tier/value | Move | LoS / fire | Removed by | Spawn context | Gameplay purpose |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Shallow shell scrape | `.` single dark dents | Scattered singles or 2-3 cell flecks | 1x1 to 3x2 | Light 0.08 | normal | none | No, cosmetic terrain | No-man edges, approach lanes | Tiny stepping-stone cover for scouts |
| 2 | Old shell crater | `o` ring/crescent | Round blob with rim and open center | 3x3 to 9x9 | Half 0.18 on rim | slow center | partialBlock from rim | Infantry spade, low effort | No-man center, hot spots | First readable infantry cover |
| 3 | Deep shell crater | `O` heavy ring | Larger irregular ring, broken rim | 5x5 to 13x13 | Full 0.38 rim, negative center | verySlow center | partialBlock/block across rim | Engineers with planks or fill | Heavy bombardment bands | Creates defensive pockets |
| 4 | Crater pond | `~o~` oval water | Crater with water core and muddy bank | 4x4 to 14x9 | Light 0.08 bank | verySlow/blocked core | none | Pump or plank bridge | Low no-man zones | Forces detours and bridge choices |
| 5 | Mud pan | `~~~` flat blob | Soft oval or smeared patch | 5x5 to 20x14 | Negative to Light 0.04 | verySlow | none | Plank road, not cleared outright | Low ground, middle third | Punishes straight-line charges |
| 6 | Sucking bog | `~~#` dark irregular patch | Blob with blocked pockets | 6x6 to 24x18 | Negative 0.00 | hazard/verySlow | none | Engineer matting and planks | Wet flanks, low basins | Hazard field that breaks blobs |
| 7 | Reed fen | `||||` vertical streaks | Tall thin clusters, often near water | 4x6 to 18x24 | Light 0.08 | slow | conceal/rangePenalty | Cutters or burn team | Wet edges, crater ponds | Concealed scout movement |
| 8 | Dead grass rise | `^^^^` dry ridge flecks | Slight raised oval, mostly open | 4x4 to 20x12 | Negative 0.00 | normal | clearer LoS both ways | No | Dry high patches | Observation ground, dangerous exposure |
| 9 | Low earth berm | `====` soft line | 1-3 thick line, bent or crescent | 6x1 to 30x3 | Half 0.26 lee side | slow cross | partialBlock | Spades, medium effort | Ridges, field folds | Natural firing ledge |
| 10 | Clay bank | `#####` jagged wall | Thick broken line with gaps | 8x2 to 36x5 | Full 0.38 | blockedWithGaps | block | Picks or explosives | Dry stream cuts, slopes | Major lane divider |
| 11 | Dry drainage gully | `S` snaking trench-like lowland | Curving 2-5 wide snake | 12x2 to 60x5 | Half 0.26 inside | slow | partialBlock into/out | Bridge, fill, or ramps | Sloped ground, flanks | Natural trench-network seed |
| 12 | Ravine cleft | `S###S` wide snake | Long cut with steep lips and rare crossings | 20x5 to 90x12 | Full 0.38 floor/lip | blockedWithGaps | block across lips | Engineer bridge/ramp | Mid-map, lane borders | Large map-shaping obstacle |
| 13 | Stone outcrop | `###` rock cluster | Compact rocks, avoid perfect squares | 2x2 to 12x12 | Full/Hard 0.38-0.50 | blocked pockets | block | Explosives, high effort | Rocky knobs, dry rises | Strong anchor point |
| 14 | Shale scree | `:::` scatter | Loose scatter around slopes | 5x5 to 22x16 | Light/Half 0.08-0.18 | slow | none/aimPenalty | Engineers clear, medium | Hills, outcrop edges | Slows flanks without full blocking |
| 15 | Boulder field | `#.#.#` scattered rocks | Patch of 1x1 to 3x3 blockers | 8x8 to 30x30 | Half/Full mixed | slow weave | partialBlock | Demolition, high effort | Rocky no-man pockets | Firefight maze, anti-blob |
| 16 | Fossil rib cage | `)))` curved ribs | Curved parallel bone ribs with gaps | 6x4 to 24x14 | Full/Hard 0.38-0.50 | channeled | partialBlock like slats | Essence saw or explosives | TWB old-bone geology | Distinctive weird cover landmark |
| 17 | Fallen trunk | `TTTT` line | 1-cell wide log, rotate N/S/E/W | 1x4 to 1x14 | Half/Full 0.26-0.38 | slow vault | partialBlock | Saw, axe, or burn | Dead woods, copse edges | Quick cover line |
| 18 | Root tangle | `YyY` branching snake | Branching organic lines | 4x4 to 18x18 | Half 0.18 | verySlow | conceal | Axes or sappers | Woods, essence damp | Pulls engineers into cover work |
| 19 | Thorn brake | `xxx` dense bramble | Blob or broken hedge-like line | 3x4 to 20x16 | Light/Half 0.08-0.18 | slow/blocked pockets | conceal | Cutters or burn | Field edges, flanks | Soft denial and ambush cover |
| 20 | Ash-black copse | `TT..TT` dead trees | Loose forest patch with internal gaps | 8x8 to 36x36 | Half 0.18 | slow | block after 5 cells | Axes/fire, high effort | Rear flanks, mid-map | Scout hide and defensive grove |
| 21 | Splinterwood stand | `/|/|` jagged tree shards | Thin jagged columns and broken rows | 5x8 to 24x40 | Half 0.18 | slow | stripe partialBlock | Axes, medium effort | Burnt forest lanes | Directional sightline breakup |
| 22 | Burnt orchard rows | `||||` parallel rows | Parallel 1-cell rows with lanes between | 8x8 to 30x40 | Half 0.18 per row | normal along, slow across | lane-direction LoS | Axe/burn | Old farmland | Creates row fighting without fortifications |
| 23 | Hedge mound | `====` ragged living line | 1-3 thick broken line | 5x1 to 35x3 | Light/Half 0.08-0.18 | slow cross | conceal | Cutters/burn | Rural field edges | Early soft lane separator |
| 24 | Bracken sink | `,,,` low vegetation | Soft patch with hidden holes | 5x5 to 20x20 | Light 0.08 | slow | conceal | Cutters, low effort | Low woods, wet shade | Ambush and scout uncertainty |
| 25 | Bone shale ridge | `^^^^#` ribbed ridge | Arc or ridge of pale stone/bone | 10x3 to 50x8 | Half/Full 0.26-0.38 | slow cross | crest partialBlock | Picks/explosives | TWB fossil uplands | Natural defensive spine |
| 26 | Glassroot patch | `+*+` glowing roots | Crystal-root cluster, no perfect square | 3x3 to 14x14 | Light 0.08 | normal | aimPenalty/refraction | Harvest/clear with essence tools | Essence seams, damp ground | Magic-flavored minor cover/resource hook |
| 27 | Essence mire | `*~*` glowing wet pool | Irregular luminous mire | 4x4 to 18x18 | Negative 0.00 | slow/hazard | aimPenalty both sides | Ward stakes or drain | Magical seep zones | Risk/reward terrain, not safe cover |
| 28 | Whisper fungus grove | `ooo*` mushroom cluster | Round caps in clusters | 3x3 to 16x16 | Light/Half 0.08-0.18 | slow | conceal, false contact chance | Burn or essence knife | Damp hollows | Scouting confusion patch |
| 29 | Steam vent field | `'^'` vent dots | Dots in loose field, pulsing opacity | 5x5 to 24x18 | Light 0.08 intermittent | hazard pulses | conceal/rangePenalty pulses | Cap vents, engineer kit | Geothermal/steam weird zones | Dynamic soft cover |
| 30 | Tar seep | `@@@` black pools | Pools with sticky edges | 3x3 to 18x12 | Negative/Light 0.00-0.08 | verySlow/hazard | none | Burn off or excavate | Low ground, old marsh | Choke and attrition hazard |
| 31 | Ironstone knobs | `#:#` metallic stones | Small hard rocks in scatter | 6x6 to 20x20 | Half/Full 0.26-0.38 | slow weave | partialBlock/deflection | Explosives | Mineral-rich ridges | Reliable cover with ricochet flavor |
| 32 | Sulfur crust flats | `---` cracked yellow flats | Wide flat patch with brittle edges | 5x5 to 26x18 | Negative 0.00 | normal/slip | dust reveals movers | Flush or shovel, low effort | Steam/vent areas | Exposed crossing zone |
| 33 | Crystal scree | `***` shard scatter | Shards around essence seams | 4x4 to 18x18 | Light/Half 0.08-0.18 | slow | aimPenalty, sparkle false sight | Essence clear, medium | Magical edges | Weird cover that hurts accuracy |
| 34 | Salt pan cracks | `_/_/` cracked flat | Large open flat with crack lines | 10x10 to 50x30 | Negative 0.00 | normal/fast | long clear LoS | No | Dry center flats | Deliberate open killing ground |
| 35 | Loess waves | `~~~~` soft dune/ridge bands | Long soft ridges, parallel-ish | 5x10 to 40x80 | Light/Half lee 0.08-0.18 | slow uphill | partialBlock over crests | Shovel, low effort | Dry flanks | Gentle approach modulation |
| 36 | Flooded swale | `~~~~S` shallow water snake | Long 3-8 wide water line | 20x3 to 100x8 | Light bank 0.08 | slow | none | Plank bridge/pump | Low corridors | Separates local fights |
| 37 | Corpse-flower meadow | `,,,o` dark wildflowers | Soft oval vegetation patch | 6x6 to 24x24 | Light 0.08 | normal | conceal | Burn, low effort | Old casualty ground | Grim ambush/concealment tile |
| 38 | Static storm scar | `Zzz` jagged scar | Branching lightning-like line | 10x2 to 50x5 | Negative 0.00 | hazard pulses | rangePenalty/static | Ground rods or warding | Essence weather zones | Magical hazard and route tax |
| 39 | Subsurface sinkholes | `0.0` holes in patch | Cluster of holes with lips | 1x1 to 5x5 holes in 18x18 patch | Half 0.18 lip | blocked/hazard center | partialBlock | Fill/plank, medium | Undermined no-man zones | Anti-blob scatter and micro-cover |
| 40 | Mist hollow | `~~~` fog oval | Soft oval, can overlap low vegetation | 8x8 to 40x28 | Light conceal 0.08 | normal/slow | rangePenalty, shorter spotting | Flare/fan, temporary | Low/magic wet basins | Forces close scouting before contact |

## Random Generation Guidance

- Use placement templates, not individual random cells. Pick a template, choose orientation, apply a shape mask, then stamp cell effects.
- Partition the 600 x 1000 war grid into broad x-zones:
  - rear/base approach: low density, mostly small cover, no large blockers;
  - approach belts: moderate cover, scattered obstacles;
  - no-man center: highest crater/mud/ridge density;
  - flanks: more gullies, woods, wetlands, and long shaping features.
- Maintain three entry lanes per side. Each top/middle/bottom lane should get roughly equivalent cover budget, not identical terrain.
- Protect all 10 x 10 bases, entry-zone cells, and a corridor at least 35 cells forward from every entry zone.
- Also protect a soft lane spine from each entry zone: no fully blocked feature may span more than 40 percent of that lane width within the first 120 cells.
- Use cluster families:
  - micro cover clusters: 5-20 cells, high frequency;
  - tactical patches: 20-160 cells, medium frequency;
  - map shapers: 160-900 cells, rare and must have gaps/crossings.
- Keep hard blockers below about 4-6 percent of total war cells. Total terrain-influenced cells can be much higher, around 12-20 percent in no-man zones.
- Every large blocker or ravine must place at least one gap, ford, bridgeable lip, or soft crossing every 12-25 cells along its length.
- Run a flood-fill validation after generation:
  - each player entry zone can reach the center band;
  - each enemy entry zone can reach the center band;
  - top/middle/bottom lanes have at least two reachable crossing routes;
  - no single obstacle cluster seals the whole height of the map.
- Avoid perfect symmetry. Use budget symmetry instead: each faction gets comparable cover, route length, and blocker count inside its mirrored third, with 10-15 percent variance.
- Let some features overlap only by rule:
  - crater plus mud is good;
  - reeds plus water is good;
  - steam vents plus sulfur crust is good;
  - large ravine plus dense woods should be rare because it over-blocks.
- Reserve rare TWB weirdness. Essence/mist/steam/fossil terrain should be about 10-15 percent of terrain placements, enough to flavor the map without replacing WW1 mud and cover.
- Seeded generation should store the final stamped cells, not just the random seed, once save/load exists.

## Implementation-Ready Data Schema Suggestion

Use a definition plus stamped-cell model. This keeps authoring flexible and lets the current prototype map many definitions into broad buckets until rendering catches up.

```csharp
public enum NaturalObstacleId
{
    ShallowShellScrape,
    OldShellCrater,
    DeepShellCrater,
    // ...
}

public enum NaturalShapeKind
{
    Scatter,
    Blob,
    Ring,
    Crescent,
    Line,
    Snake,
    Ridge,
    Rows,
    Branching,
    Field
}

public enum NaturalCoverTier
{
    Negative,
    None,
    Light,
    Half,
    Full,
    Hard
}

public enum NaturalMovementEffect
{
    Normal,
    Slow,
    VerySlow,
    BlockedWithGaps,
    Hazard
}

public enum NaturalLosEffect
{
    None,
    Conceal,
    PartialBlock,
    Block,
    RangePenalty,
    AimPenalty
}

public sealed class NaturalObstacleDefinition
{
    public string Id;
    public string DisplayName;
    public char Glyph;
    public NaturalShapeKind[] Shapes;
    public int MinWidth;
    public int MaxWidth;
    public int MinHeight;
    public int MaxHeight;
    public NaturalCoverTier CoverTier;
    public float CoverValue;
    public NaturalMovementEffect Movement;
    public float MovementCostMultiplier;
    public NaturalLosEffect LosEffect;
    public float LosOpacity;
    public bool BlocksMovement;
    public bool Removable;
    public string RemovalToolTag;
    public float RemovalWork;
    public string[] SpawnContexts;
    public int Weight;
    public int MinDistanceFromEntry;
    public bool AllowsTrenchDigging;
    public float TrenchDigSpeedMultiplier;
}

public sealed class NaturalObstacleInstance
{
    public string DefinitionId;
    public int OriginX;
    public int OriginY;
    public int Width;
    public int Height;
    public int Rotation;
    public int Seed;
}

public struct NaturalObstacleCellEffect
{
    public string DefinitionId;
    public int X;
    public int Y;
    public float CoverValue;
    public float MovementCostMultiplier;
    public float LosOpacity;
    public bool BlocksMovement;
    public float RemovalWorkRemaining;
}
```

Prototype adapter:

- Negative/Light effects can map to exposed or crater-like cells.
- Half effects can map to rubble/crater behavior.
- Full/Hard effects can map to ruin-like cover, but only hard blockers should block movement.
- Wire should remain a built/war obstacle, not the default bucket for natural terrain.

## Top 10 To Implement First

1. Old shell crater - immediately improves ranged firefights.
2. Deep shell crater - creates durable infantry pockets.
3. Mud pan - slows blob charges without needing more AI.
4. Low earth berm - readable half-cover lines.
5. Dry drainage gully - naturally seeds trench-network behavior.
6. Stone outcrop - gives strong anchor points.
7. Boulder field - breaks LoS and movement at squad scale.
8. Root tangle - gives engineers a reason to matter.
9. Reed fen - supports scouting and concealment.
10. Mist hollow - adds TWB mood while testing reduced spotting ranges.

## Files Touched

- Created this report only: `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-natural-obstacle-design-report.md`

## Risks

- Too many full blockers will make the map feel jammed instead of organic.
- Too much magic terrain will dilute the WW1 mud-and-cover read.
- If all obstacle types are implemented visually before behavior, the map will look busy but not play differently.
- Current prototype data can support cover, integrity, and movement blocking, but richer LoS, concealment, movement-cost, and hazard behavior need data expansion.

## Memory-Worthy Notes

- Decision candidate - Natural terrain should be data-driven obstacle definitions stamped into cell effects, not 40 hard-coded enum values.
- Design direction - Natural map variability should prioritize sightline breaks, lateral detours, cover pockets, and trench-network seeds.
- Warning - Generation must reserve clear entry corridors and flood-fill validate routes from all six entry zones before a map is accepted.
