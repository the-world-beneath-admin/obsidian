# Codex Work Order

## Purpose

This is the actual production sequence Codex should follow.

Do not jump around randomly.
Finish one stage enough to prove the system works, then move forward.

## Stage 0: Establish pipeline foundation

### Goal

Set up the file structure and tooling assumptions.

### Tasks

1. Create the folder structure from `08_FILE_STRUCTURE_AND_EXPORT.md`.
2. Define naming conventions in code/config comments if needed.
3. Define common asset size expectations.
4. Define Unity import assumptions.
5. Create a simple art-pipeline checklist document or internal TODO list.

### Done when

- folders exist
- naming exists
- import rules are clear
- no asset production is happening in chaos

## Stage 1: First biome terrain source set

### Goal

Create one fully usable terrain visual foundation.

### Biome

Temperate battlefield / damp earth.

### Required assets

1. one material source sheet
2. trench mask family
3. sandbag overlay family
4. trench line/detail masks
5. trench shadow masks
6. decal set
7. crater set

### Done when

- Codex can assemble a readable trench scene from modular pieces
- straight trench and junction trench both work
- the result is usable in a prototype map

## Stage 2: Battlefield prop pack

### Goal

Make the trenches feel occupied and believable.

### Required assets

- ammo crate
- supply crate
- barrel
- sandbag pile
- loose boards
- support posts
- ladder
- duckboards
- wire spool
- debris cluster
- shell box

### Done when

- a trench area can be dressed with battlefield clutter
- props do not clash with terrain scale

## Stage 3: Core weapon emplacement pack

### Goal

Create the iconic battlefield weapons.

### Required assets

- machine gun emplacement
- mortar emplacement
- optional artillery emplacement
- damaged variants if possible

### Required supporting assets

- muzzle flashes
- smoke
- impact effects
- ammo props

### Done when

- the battlefield can show active defensive and indirect-fire positions
- weapon systems are visually distinct

## Stage 4: Basic infantry pack

### Goal

Add readable military units.

### Required units

- rifleman
- engineer
- support gunner
- mortar crewman or support infantry

### Minimum animation set

- idle
- move
- fire

### Direction count

- 4 directions first

### Done when

- units read clearly in motion
- helmets and guns are visible
- they fit the trench scale

## Stage 5: Vehicle and logistics pack

### Goal

Support battlefield logistics and larger combat identity.

### Required units

- supply truck
- light utility vehicle or tractor
- tank or armored support unit

### Supporting assets

- dust puffs
- exhaust
- wreck state if possible

### Done when

- movement and supply visuals are present
- battlefield no longer depends only on infantry

## Stage 6: Factory / production visuals

### Goal

Bridge the factory game and the trench war simulation.

### Required assets

- simple industrial building modules
- conveyor parts
- loading dock clutter
- supply pallets
- machine housings
- pipe clusters
- vent/fan module
- storage bins

### Done when

- factory areas look intentional
- the supply side and war side share one visual language

## Stage 7: UI and icon pass

### Goal

Make the prototype feel complete.

### Required outputs

- unit icons
- resource icons
- build icons
- selection ring
- build ghost visuals
- progress bars or supporting visual widgets
- basic military-style panels

### Done when

- player interactions are easy to read
- the prototype looks like a real game instead of a tool scene

## Stage 8: Effects polish pass

### Goal

Make the game feel active.

### Required outputs

- better muzzle flashes
- better smoke
- better impacts
- destruction loops
- industrial smoke / steam
- selection and alert effects

### Done when

- combat and production feel alive
- simple animation no longer feels dead

## Stage 9: Second biome only after first slice works

### Goal

Expand safely.

### Rule

Do not start desert, jungle, snow, or other major biome sets until:

- first biome terrain works
- props work
- units work
- VFX works
- UI works

Then duplicate the system and adapt:

- palette
- materials
- decals
- sandbag wear style
- environment clutter

## Implementation philosophy

For every stage, Codex should do this:

1. create source assets
2. organize them
3. define how they are used
4. wire them into the prototype
5. verify in-scene readability
6. only then move on

## Quality threshold

Each stage is acceptable when the asset:

- is clear
- is usable
- matches the style
- integrates in the game
- does not require human repainting to function

That is the standard.

## Final rule

**Do not chase perfection. Build a complete working art system.**
