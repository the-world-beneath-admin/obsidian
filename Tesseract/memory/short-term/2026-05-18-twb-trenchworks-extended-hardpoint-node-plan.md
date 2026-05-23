# TWB Trenchworks Extended Hardpoint And Node Plan

## Purpose

Capture the intended hardpoint blueprint model for TWB Trenchworks as a short-term worker note. This is not permanent memory.

Hardpoints should not be pre-designated functional combat/support nodes during trench generation. The generator should create access trenches and empty hardpoint pads only. The actual node identity and function should emerge later through engineer construction and specialist squad claiming.

## Generation Order

1. Establish the paired front lines.
2. Add front-to-support access trenches.
3. Establish the support trench line.
4. Establish supply lanes back to base.
5. Generate hardpoint access trenches and empty hardpoint pads last.

Hardpoint pads should be downstream from the completed trench network, not mixed into the first support-line pass.

## Empty Hardpoint Blueprint Contract

- Hardpoint blueprint output should consist of an access trench plus an empty square place-marker pad.
- Pads should be either 4x4 or 8x8, depending on intended future node scale.
- Access trenches should branch from support trenches and/or existing access trenches.
- Access trenches should extend roughly 1-2 access-trench distances before reaching the pad.
- Pads should remain empty in blueprint form.
- Pads should not pre-select mortar, aid, observation, food, supply, or other node identity.
- Pads should not be functional when generated.

## Later Gameplay Contract

- Engineers must build an empty hardpoint pad to Tier 1 before it becomes claimable.
- Specialist squads can then claim/fill the pad with an attack or support node.
- Possible node types include mortars, aid tents, observation posts, food caches, supply caches, and other specialist structures.
- Specialist squads offload required supplies at the claimed pad.
- Engineers must build the claimed node to Tier 2 before it becomes functional.

## Current Implementation Scope

The current trench-generation task should only implement the blueprint layout portion:

- Generate access trenches to future hardpoint locations.
- Generate empty 4x4 and/or 8x8 hardpoint pads.
- Ensure hardpoint pad generation happens after front, access, support, and supply lanes are in place.
- Keep hardpoint pads visibly empty and non-functional.
- Preserve the staged construction model and avoid returning to pre-designated functional hardpoints.

## Deferred Work

- Specialist squad claiming rules for empty pads.
- Supply offload requirements.
- Tier 1 pad construction behavior.
- Tier 2 node construction behavior.
- Node identity selection and balancing.
- Functional logic for mortars, aid tents, observation posts, food caches, supply caches, and other node types.
- Final art for hardpoint pads and filled node variants.

## Risks/Open Questions

- Exact rules for choosing 4x4 versus 8x8 pads need design tuning.
- The number of hardpoint pads per sector should be constrained so the trench system does not become cluttered.
- Access trenches to pads must not create accidental front-line fighting positions.
- Pads should be readable as future build sites without looking like completed structures.
- The generator needs enough spacing to keep pads from overlapping support trenches, supply lanes, or each other.
- Later node claiming must avoid letting specialist squads bypass the engineer construction gate.
