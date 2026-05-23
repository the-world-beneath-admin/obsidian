# VFX and Particles

## Purpose

Effects are critical because they make simple art feel alive.

Good VFX can make low-frame-count units and props feel much more complete.

## 1. VFX philosophy

Effects should be:

- readable
- fast
- supportive
- consistent with the art style
- not overblown
- easy to reuse

## 2. Core effect categories

### Weapon fire

- muzzle flashes
- smoke puffs
- shell ejection optional

### Projectile / launch

- mortar launch puff
- shell trail
- tracer line
- rocket trail if relevant

### Impact

- dirt hit
- sandbag hit
- metal spark hit
- explosion burst
- crater effect

### Environmental

- dust puff
- smoke plume
- fire loop
- industrial steam
- chimney smoke

### Unit feedback

- selection ring
- move marker
- hit indicator
- suppression or alert icon if used

## 3. Visual style

Effects should match the game:

- painterly but simple
- stylized battlefield particles
- not hyper-realistic volumetrics
- not cartoony magic unless specifically needed
- good contrast against muddy terrain

## 4. Muzzle flashes

### Required families

- rifle flash
- machine gun flash
- cannon flash
- mortar launch flash/puff

### Style

- compact bright shape
- short-lived
- slight smoke follow-up
- do not make giant Hollywood fireballs for small arms

## 5. Smoke

### Types

- shot smoke
- mortar smoke
- explosion smoke
- wreck smoke
- industrial smoke

### Rules

- soft shape
- layered opacity
- desaturated gray/brown
- battlefield smoke can be darker
- industrial smoke can be more regular

## 6. Impact effects

### Terrain hit

- dirt burst
- mud burst
- sand kick

### Sandbag hit

- dust burst
- cloth/dirt specks

### Metal hit

- small sparks
- gray dust / impact flecks

### Explosion

- flash + dust + smoke
- debris fragments optional
- scalable sizes

## 7. Mortar and artillery effects

### Mortar launch

- base smoke puff
- brief recoil
- shell ascent implied

### Mortar impact

- dirt burst
- smoke plume
- crater decal spawn if needed

### Artillery impact

- larger burst
- bigger dust column
- heavier smoke
- optional camera shake support in code

## 8. Movement effects

### Infantry

- subtle dust or mud puff optional

### Vehicles

- dust trail
- exhaust puff
- heavier movement presence

### Logistics objects

- conveyor particle bits optional
- steam vent optional

## 9. Fire and destruction

### Required

- small flame loop
- medium flame loop
- small black smoke loop
- heavy smoke loop
- wreck ember flicker optional

These help destroyed units and damaged structures feel final.

## 10. UI support effects

### Useful small effects

- selection pulse
- build placement ghost highlight
- repair spark
- production completion pop
- objective ping
- warning flash

These can be very simple and still improve the game a lot.

## 11. Production format

Effects can be made as:

- sprite sheets
- flipbook animation
- layered particle elements
- additive flashes plus alpha smoke

Codex should prefer reusable small effect sheets over giant bespoke effect scenes.

## 12. What VFX should accomplish

The player should feel:

- gunfire is active
- shells are landing
- objects have weight
- the battlefield is alive
- factories and machines are operating

If the underlying art is simple, good VFX will help the game feel complete.
