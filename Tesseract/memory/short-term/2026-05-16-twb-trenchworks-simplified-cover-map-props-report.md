# TWB Trenchworks Simplified Cover And Map Props Report

Date: 2026-05-16

Scope: standalone TWB Trenchworks Unity 2D prototype at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

This report supersedes `2026-05-16-twb-trenchworks-natural-obstacle-design-report.md` for implementation direction. The previous report was too granular and included effects, such as ricochet-style behavior, that are not needed for the prototype.

## Core Direction

Use a simple battlefield readability model:

- Cover means bullets are physically blocked.
- Concealment means enemies have trouble seeing or identifying the unit.
- Concealment does not stop bullets once a target is known.
- Terrain can also slow movement, block movement, or make digging easier/harder.
- Map props should be readable grid/box shapes that combine these few effects, not forty unique physics tricks.

## Soldier Exposure Model

Posture should be part of unit state, not part of the prop itself.

| Posture | Meaning | Can fire? | Exposure | Typical use |
|---|---|---:|---|---|
| Above ground standing | Normal surface movement/firing | Yes | High | Scouting, crossing, assaulting |
| Above ground crouching | Lower profile on surface | Yes | Medium | Using low cover, moving cautiously |
| Above ground prone | Laying down on surface | Limited/slow | Low | Surviving in open ground, waiting |
| Below ground standing | Standing in trench, crater, gully, or pit | Yes | Low to medium | Firing from prepared/depressed ground |
| Below ground crouching | Crouched low inside trench, crater, gully, or pit | No or limited | Very low | Hiding, surviving bombardment, waiting |

Prototype rule of thumb:

- Standing ignores half cover if the cover is too low.
- Crouching uses half cover well.
- Prone can benefit from tiny ground depressions but moves slowly.
- Below-ground standing can fire while receiving half/full cover from the lip.
- Below-ground crouching gets full cover and strong concealment, but should not contribute much fire.

## Cover And Concealment Tiers

Use only these tiers at first.

| Tier | Gameplay meaning | Suggested numeric model |
|---|---|---|
| No cover | Bullets can hit normally | `coverBlockChance = 0.00` |
| Half cover | Some bullets are blocked if posture lines up | `coverBlockChance = 0.45` |
| Full cover | Most direct small-arms fire is blocked | `coverBlockChance = 0.80` or direct-fire immune unless flanked/adjacent |
| No concealment | Unit is visible if in sight range | `spottingMultiplier = 1.00` |
| Half concealment | Unit is harder to spot | `spottingMultiplier = 0.60` |
| Full concealment | Unit is difficult to spot until close/contact | `spottingMultiplier = 0.25` |

Important distinction:

- A soldier behind full concealment but no cover can still be hit once known.
- A soldier behind full cover but no concealment is visible but hard to damage.
- A wooded patch can provide both partial concealment and partial cover.
- A mud patch provides neither and slows movement, making it a killing field.

## Revised Map Prop List

| # | Prop | Shape / footprint | Cover | Concealment | Movement | Posture interaction | Gameplay purpose |
|---|---|---|---|---|---|---|---|
| 1 | Open hardpan | Large irregular patch, 20x20 to 80x60 | None | None | Normal | Standing/prone only | Baseline exposed ground |
| 2 | Mud patch | Blob, 8x8 to 40x30 | None | None | Slow | Prone is poor; crouch/stand slog | Killing field that punishes crossing |
| 3 | Deep mud pit | Dark blob pockets, 4x4 to 18x18 | None | None | Very slow | Units avoid unless desperate | Strong route tax without cover |
| 4 | Flooded mud | Shallow water blob, 8x6 to 50x24 | None | Half concealment if reeds overlap | Very slow | Below-ground not allowed | Creates dangerous low crossing |
| 5 | Shell-churned ground | Broken patch, 12x12 to 60x50 | None to half cover by micro-depressions | None | Slow | Prone gets light survival bonus | Makes no-man land uneven |
| 6 | Shallow shell scrape | Scattered 1x1 to 3x2 dents | Half cover only while prone/crouched | None | Normal | Surface crouch/prone useful | Tiny survival footholds |
| 7 | Old shell crater | Ring/blob, 4x4 to 10x10 | Half cover on rim/lip | None | Slow center | Below-ground standing/crouching allowed | Core infantry cover pocket |
| 8 | Deep shell crater | Larger ring, 8x8 to 16x16 | Full cover inside/lip | Half concealment inside | Slow/very slow | Below-ground standing/crouching strong | Durable holding point |
| 9 | Crater chain | 3-8 craters in a loose line | Half/full per crater | None to half inside | Slow between craters | Units can hop cover to cover | Encourages organic advances |
| 10 | Crater pond | Crater with flooded center, 6x6 to 16x14 | Half cover on dry rim | None | Very slow/blocked center | Below-ground only on rim | Forces movement around bad ground |
| 11 | Low earth berm | Bent line, 1-3 thick, 8-40 long | Half cover from one/both sides | None | Slow crossing | Crouch/standing fire from behind | Readable firing ledge |
| 12 | High earth bank | Jagged line, 2-5 thick, 10-50 long | Full cover behind bank | None | Blocked except gaps | Standing behind cannot shoot over unless adjacent/lip | Strong lane divider |
| 13 | Dry drainage gully | Snaking 2-5 wide line, 20-90 long | Half cover inside | Half concealment inside | Slow | Below-ground movement/firing | Natural trench seed |
| 14 | Deep ravine | Snaking 5-12 wide line, 30-120 long | Full cover inside/lips | Half concealment | Blocked/slow with crossings | Below-ground strong, crossing costly | Major map-shaping feature |
| 15 | Raised ridge | Long soft ridge, 3-8 thick, 20-100 long | Half cover on far side | None | Slow crossing | Standing can see/fire better but exposed on crest | Creates crest fights |
| 16 | Stone outcrop | Compact rock blob, 2x2 to 12x12 | Full cover against direct fire | None | Blocks some cells | Crouch/stand behind edges | Hard anchor point |
| 17 | Boulder scatter | Scatter field, 8x8 to 35x35 | Half cover, occasional full | None | Slow weave | Crouch/stand behind stones | Breaks blobs into smaller fights |
| 18 | Fallen trunk | Line, 1x4 to 1x18 | Half cover | None | Slow crossing | Crouch/prone behind it | Simple low cover line |
| 19 | Root tangle | Branching patch, 6x6 to 24x24 | Half cover in thick roots | Half concealment | Slow/very slow | Crouch useful, standing exposed | Mixed woodland obstacle |
| 20 | Dead tree cluster | Loose tree patch, 8x8 to 36x36 | Half cover near trunks | Half concealment | Slow | Standing/crouch both useful | Small wooded fight pocket |
| 21 | Dense wooded area | Large irregular patch, 20x20 to 90x70 | Half cover near trunks | Full concealment at depth | Slow | Units break visual contact inside | Big concealment zone with some cover |
| 22 | Sparse wooded area | Open patch, 15x15 to 70x50 | Light/half cover near trunks | Half concealment | Slight slow | Units remain partially visible | Softer terrain variation |
| 23 | Reed bed | Wet oval/line, 8x8 to 50x30 | None | Full concealment | Slow | Prone/crouch hide well, little protection | Ambush/scout terrain |
| 24 | Tall grass field | Patch, 12x12 to 80x50 | None | Half concealment | Normal/slight slow | Prone hides well | Concealment without protection |
| 25 | Thorn brush | Blob/line, 6x6 to 40x18 | None to half cover at thick edge | Half concealment | Slow | Crouch hidden, standing partly visible | Soft route friction |
| 26 | Hedge line | Broken line, 1-3 thick, 8-60 long | Half cover | Half concealment | Slow crossing, normal along | Crouch/stand behind hedge | Rural lane separator |
| 27 | Dense hedge | Thicker broken line, 2-4 thick, 10-50 long | Half cover | Full concealment across it | Blocked/slow gaps | Units can hide but not safely cross fast | Ambush boundary |
| 28 | Bracken patch | Soft blob, 8x8 to 35x35 | None | Half concealment | Slow | Prone/crouch strong concealment | Low vegetation variation |
| 29 | Mist hollow | Soft fog oval, 15x15 to 70x45 | None | Full concealment | Normal/slight slow | Concealment independent of posture | Forces close scouting |
| 30 | Smoke/steam vent patch | Small field, 8x8 to 35x25 | None | Half/full concealment intermittent | Normal/hazard optional later | Visibility changes; no bullet blocking | TWB/steam mood without weird ballistics |
| 31 | Ruined stump field | Scatter, 10x10 to 45x45 | Half cover near stumps | Half concealment | Slow | Crouch among stumps | Dead battlefield woods |
| 32 | Sinkhole cluster | Holes in patch, 10x10 to 35x35 | Half/full cover at lips | Half concealment inside holes | Slow/blocked centers | Below-ground crouch/stand allowed in holes | Natural foxhole field |
| 33 | Ditch line | Straight/bent 1-3 wide line, 10-80 long | Half cover inside | Half concealment inside | Slow | Below-ground posture allowed | Small linear cover path |
| 34 | Deep ditch | 2-5 wide line, 15-90 long | Full cover inside | Half concealment | Slow; crossing slow | Below-ground strong | Pre-trench network seed |
| 35 | Sand wash | Pale open patch, 20x20 to 90x60 | None | None | Slight slow | Exposed crossing | Clear shooting lane |
| 36 | Gravel scree | Patch around rocks, 8x8 to 50x35 | None to half at edges | None | Slow | No hiding, noisy/exposed later | Movement tax near cover |
| 37 | Corpse-flower meadow | Dark field patch, 8x8 to 40x40 | None | Half concealment | Normal/slight slow | Prone hides well | TWB-flavored concealment field |
| 38 | Glassroot thicket | Glowing root patch, 6x6 to 24x24 | Half cover from roots | Half concealment | Slow | Crouch/standing behind roots | Magic-flavored mixed terrain |
| 39 | Essence fog patch | Irregular glowing fog, 10x10 to 50x40 | None | Full concealment | Normal/slow | Hides movement, does not stop bullets | Rare magical visibility terrain |
| 40 | Bare killing flat | Intentional open lane, 30x20 to 120x80 | None | None | Normal or slightly fast | Standing easiest, prone survival only | Deliberate exposed danger zone |

## Terrain Patch Families

Use these as implementation groups instead of forty bespoke systems.

| Family | Examples | Cover | Concealment | Movement |
|---|---|---|---|---|
| Open/exposed | open hardpan, sand wash, bare killing flat | None | None | Normal |
| Slow exposed | mud patch, deep mud, flooded mud | None | None/conditional | Slow/very slow |
| Depressed ground | craters, gullies, ditches, sinkholes | Half/full by depth | None/half inside | Slow |
| Raised hard cover | berms, banks, ridges, rocks | Half/full | None | Slow/blocked |
| Vegetation concealment | grass, reeds, bracken, brush | None/half | Half/full | Normal/slow |
| Woodland mixed | sparse/dense woods, stump fields, root tangles | Half | Half/full | Slow |
| Rare TWB terrain | glassroot, essence fog, corpse-flower meadow | None/half | Half/full | Normal/slow |

## Generation Guidance

- Generate patches first, then props inside patches.
- Keep open killing flats intentional, not accidental map emptiness.
- Protect all bases, entry zones, and the first 35-50 cells in front of each entry zone from full blockers.
- Each top/middle/bottom lane should receive comparable budgets:
  - exposed ground budget
  - half-cover pockets
  - full-cover anchors
  - concealment zones
  - slow terrain
- Avoid full-height blockers. Every large line feature needs gaps or crossings.
- Use cover and concealment budgets separately. A map can be fair even if one side has more concealment and the other has more hard cover, but the total tactical value should be close.
- Place mud/exposed fields between cover pockets so squads must choose when to cross.
- Place gullies/ditches in broken diagonals and curves so trench networks naturally connect to them.
- Dense woods and full concealment should be rare near bases so early movement remains readable.
- Flood-fill each generated map from all six entry zones to the middle band before accepting it.

## Data Schema Suggestion

This should become data-driven cell effects, not a large enum full of special cases.

```csharp
public enum CoverTier
{
    None,
    Half,
    Full
}

public enum ConcealmentTier
{
    None,
    Half,
    Full
}

public enum MovementTier
{
    Normal,
    Slow,
    VerySlow,
    Blocked
}

public enum Stance
{
    SurfaceStanding,
    SurfaceCrouching,
    SurfaceProne,
    BelowGroundStanding,
    BelowGroundCrouching
}

public sealed class WarMapPropDefinition
{
    public string Id;
    public string DisplayName;
    public char Glyph;
    public CoverTier Cover;
    public ConcealmentTier Concealment;
    public MovementTier Movement;
    public bool AllowsBelowGroundStance;
    public bool BlocksMovement;
    public bool BlocksLineOfFire;
    public bool BlocksLineOfSight;
    public int MinWidth;
    public int MaxWidth;
    public int MinHeight;
    public int MaxHeight;
    public string ShapeKind;
    public int SpawnWeight;
    public string[] SpawnContexts;
    public bool Removable;
    public string RemovalToolTag;
}

public struct WarCellTerrainEffect
{
    public CoverTier Cover;
    public ConcealmentTier Concealment;
    public MovementTier Movement;
    public bool AllowsBelowGroundStance;
    public bool BlocksMovement;
    public bool BlocksLineOfFire;
    public bool BlocksLineOfSight;
}
```

Prototype combat rule:

- If a target is not known, concealment reduces spotting chance.
- If a target is known, concealment no longer blocks shots.
- Cover reduces or blocks hit chance after a shot is taken.
- Full cover should block direct small-arms fire unless attacker is flanking, adjacent, elevated, or using future artillery/explosives.

## First 12 To Implement

1. Mud patch
2. Old shell crater
3. Deep shell crater
4. Low earth berm
5. High earth bank
6. Dry drainage gully
7. Stone outcrop
8. Boulder scatter
9. Tall grass field
10. Reed bed
11. Sparse wooded area
12. Dense wooded area

This set proves the full model: no protection, half/full cover, half/full concealment, slow terrain, below-ground posture, and large terrain patches.

## Files Touched

- Created this revised report: `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-simplified-cover-map-props-report.md`

## Risks

- If concealment is allowed to reduce bullet hit chance after the target is known, it will quietly become cover and muddy the design.
- If full cover is too common, squads will stall.
- If mud is too common, the war map will feel slow and frustrating rather than tactical.
- Grid-step movement will still look mechanical until Unity rendering interpolates between simulation cells.

## Memory-Worthy Notes

- Decision candidate - Use posture plus cover/concealment tiers as the war terrain model.
- Decision candidate - Cover blocks bullets; concealment blocks detection only.
- Decision candidate - Terrain props should be grouped into effect families before becoming full art/content lists.
- Warning - Remove ricochet/deflection-style obstacle behavior from the terrain design direction for now.
