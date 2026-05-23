# TWB Unity Open Questions

## Starter Guardians

- How many guardian angel starter pets are planned?
- What are their intended A-Series affinities and combat roles?
- Is the latest regenerated Stanly sprite accepted by the user?
- Should `special-ephemrial-spirit-stanly-1024.png` be resized or renamed if its current dimensions are 1254x1254?
- What is the exact next starter pet identity, role, skill, combat affinity, and reference set?
- Should Legendary starter companion cards receive bespoke UI badge/treatment beyond `ItemRarity.Legendary`?
- Should guardian starters continue using regular Tier 1 envelopes or eventually get a named special Tier 1 legendary template?

## World Map

- What is the final rule for long-range route connectivity between display-owner nodes?
- Should collapsed towns hide all town text/markers or keep labels only for major named owners?
- What is the final visual target for node dungeon and inspect dungeon subwindows?
- Should the temporary world-map dungeon run `DEV COMPLETE` control remain as editor/debug UI, move into System Console, or be removed after reward-loop testing stabilizes?
- Does the cleaned run-complete claim rewards modal pass live visual review without overlapping frames or text?
- Should icon presence be covered by focused System Console tests for Inventory, Craft Create, Craft Apply, Archive, dungeon pet selection, and card summary surfaces?

## Shared Platform

- What backend event contract, idempotency model, lock lifetime policy, and conflict resolution should govern the eventual remote companion mutation protocol?

## Sources

- [[short-term/2026-05-12-twb-unity-worldmap-working-window-intake]]
- [[short-term/2026-05-12-twb-starter-pets-working-window-intake]]
- [[short-term/2026-05-16-twb-main-game-worker-final-decommission-report]]
