# Current Intake Task

## Status

Standing workflow - use when the user wants to paste summaries from working chat windows into the Obsidian brain.

## Workflow

- [[wiki/memory/chat-summary-intake-system]]

## Goal

Convert pasted working-window summaries into useful permanent memory while discarding redundant, weak, temporary, or unuseful information.

## Read First

- [[AGENTS]]
- [[hot]]
- [[index]]
- [[wiki/memory/chat-summary-intake-system]]

## Inputs

- User-pasted chat summaries
- Working-window summaries
- Implementation summaries
- Deployment summaries
- Marketing or SEO summaries
- Playtest or bug summaries

## Constraints

- Do not paste whole summaries into the wiki.
- Do not create transcript dumps.
- Do not promote weak guesses as facts.
- Do not duplicate memory that already exists.
- Do not update unrelated pages.
- Do not archive full pasted summaries by default.
- Ask before saving raw pasted source material under `memory/raw/chat-intake/`.

## Done When

- Useful candidates are classified.
- Redundant or unuseful details are discarded.
- Durable memory candidates are recommended for promotion.
- An intake report is written under `memory/short-term/`.
- Cleanup performed is listed.
- `memory/hot.md`, `memory/index.md`, and `memory/log.md` are updated only by the orchestrator or promoter automation where needed.

## Output

- Intake reports under `memory/short-term/`
- Permanent memory updates under `memory/wiki/`
- Hydration prompt at [[templates/chat-summary-intake-hydration-prompt]]

## Report Required

Use [[templates/chat-summary-intake-report]].
