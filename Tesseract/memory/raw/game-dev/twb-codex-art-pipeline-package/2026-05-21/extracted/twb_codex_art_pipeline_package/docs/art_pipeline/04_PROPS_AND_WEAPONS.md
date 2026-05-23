# Props and Weapons

## Purpose

This document defines the battlefield props, support objects, and weapon emplacements.

These assets give the map identity and make the trenches feel inhabited and functional.

## 1. Prop philosophy

Props should be:

- top-down readable
- modular
- reusable
- silhouette-clear
- small enough to place flexibly
- detailed enough to identify
- not so detailed that consistency breaks

## 2. Prop categories

### Battlefield clutter

- ammo crates
- supply crates
- barrels
- sandbag stacks
- loose planks
- tool bundles
- posts / stakes
- wire spool
- shell boxes
- tarps
- fuel drums

### Defensive support

- barbed wire segment
- anti-vehicle obstacles
- wooden braces
- trench ladders
- duckboards
- spotting periscope
- command table if needed

### Industrial / logistics

- pallet stacks
- supply piles
- conveyor modules
- small generator
- repair bench
- storage rack
- loading platform accessories

## 3. Machine gun emplacement

This is a core battlefield identity asset.

### Visual goals

The player should instantly recognize:

- stationary heavy weapon
- forward firing arc
- defensive position

### Silhouette recipe

- long barrel body
- support mount or tripod
- ammo feed box or drum
- sandbag nest or low cover context
- optional spare ammo nearby

### Simplification rules

- no need for exact mechanical realism
- barrel and support silhouette matter most
- recoil animation can be simple
- crew can be separate small infantry sprites

### Variants

- sandbag nest MG
- tripod MG on flat ground
- bunker slit MG representation
- mounted defensive gun in trench pocket

## 4. Mortar emplacement

Another key battlefield asset.

### Visual goals

- obvious upward-firing support weapon
- easy to identify from top-down view
- clear distinction from machine gun

### Silhouette recipe

- base plate
- upward tube
- small support legs if visible
- ammo shells/crates nearby
- circular or semi-circular firing pit

### Simplification

- no need for complex crew animation
- a separate mortar crew sprite can support it
- firing can be sold by flash/smoke/shell trail

### Variants

- light mortar
- medium mortar
- reinforced mortar pit

## 5. Artillery / field gun

If included, keep it simplified.

### Silhouette recipe

- larger gun tube
- carriage or frame
- trail legs or mounting support
- nearby shell crate
- larger footprint than MG or mortar

### Use

- static emplacement
- special support object
- rear battery representation

## 6. Bunker and firing position props

### Bunker visual goals

- low reinforced structure
- obvious defensive purpose
- visible slit or hatch
- top-down readable roof or opening

### Variants

- small MG bunker
- command bunker
- supply bunker entrance
- damaged bunker

### Simplification

Bunkers should look sturdy and squat, not like full buildings with complex perspective.

## 7. Supply props

Supply visuals help both the trench war game and the logistics/factory side.

### Required supply assets

- generic crate
- ammo crate
- shell crate
- fuel drum
- ration crate
- medical crate
- sandbag pile
- spare wheel / part pile
- tool kit pile

### Color coding

Use subtle marking differences, not giant bright labels, unless needed for gameplay clarity.

## 8. Factory / logistics props

These should visually bridge the war and production layers.

### Assets

- conveyor segment
- loading dock clutter
- small industrial bins
- crate pallet
- workshop table
- machine housing
- pipe cluster
- vent/fan housing
- stack of processed supplies
- rail or truck loading accessory

### Style

- simple industrial shapes
- wartime practical look
- top-down readable
- not modern shiny sci-fi

## 9. Prop set deliverables

Codex should create prop art in grouped sets.

### Set A: battlefield clutter

- 10 to 20 small isolated prop assets

### Set B: weapon emplacements

- MG set
- mortar set
- artillery set if needed

### Set C: logistics clutter

- industrial props
- supply props

### Set D: trench support parts

- ladders
- duckboards
- braces
- post segments
- loose sandbags

## 10. Animation expectations

Most props are static.

### Animated props only when useful

- rotating fan
- blinking indicator on industrial object if needed
- MG recoil
- mortar firing bounce
- artillery recoil
- smoke from generator or chimney

Do not animate everything.

## 11. What props should look like

Props should feel like:

- functional equipment
- a little worn
- built for war
- small but believable
- visually clean enough to read at gameplay zoom

If the player says “that’s obviously a mortar,” “that’s clearly an ammo crate,” or “that is definitely a machine gun nest,” the asset succeeds.
