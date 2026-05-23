# Starter Pet Art Pipeline

## Current Guidance

Starter pet art should start from original user references when the existing cutout or generated image is artifact-ridden.

## Cutout And Matte Rules

- Regenerate clean source rather than endlessly patching a flawed cutout.
- Use high-contrast matte checks to inspect edges before accepting an asset.
- Prefer magenta or bright-pink matte checks when practical, and treat visible matte spill, cutout halos, or outline artifacts as QA failures.
- Do not promote failed cleanup scripts or temporary preview composites as durable workflow.

## Stanly Status

The latest Stanly regenerated sprite was created after rejected artifact-ridden cleanup attempts. It still needs explicit user acceptance before it is treated as final.

Known issue to verify:

- `special-ephemrial-spirit-stanly-1024.png` may be named as a 1024 asset while the generated image was checked at 1254x1254.

## Chuck Status

Chuck's generated sprite is reported as an isolated transparent groundhog pet sprite with no porch, prop, platform, fruit, mound, or background. It still needs explicit user/Bob acceptance before being treated as final.

Chuck source and runtime PNGs were reported as `1254x1254` RGBA with transparent corners.

## Sources

- [[short-term/2026-05-12-twb-starter-pets-working-window-intake]]
- [[short-term/2026-05-13-twb-unity-starter-pets-worker-final-decommission-report]]
- [[wiki/twb-creature-spritesheets/asset-contract]]
