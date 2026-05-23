# TWB Decommission Skill Implementation

Date: 2026-05-18

## Source

User requested a callable skill for the "summarize back to orchestrator" worker-window shutdown process, so a worker can create its final report back to Bob/orchestrator when being decommissioned.

## What Changed

- Created local Codex skill `twb-decommission` at `C:\Users\yrred\.codex\skills\twb-decommission`.
- Added `SKILL.md` with the worker decommission workflow.
- Added `references/decommission-report-schema.md` with the required short-term report structure.
- Added OpenAI interface metadata for the skill.
- Validated the skill with the skill-creator quick validation script.

## Durable Rules Promoted

- Use `twb-decommission` inside a worker window when the worker is being stopped, restarted, retired, summarized, or asked to report back to Bob/orchestrator.
- The skill writes exactly one final Markdown report under `memory/short-term/`.
- The worker must not update permanent memory during decommission.
- The report must include scope, work completed, files touched, child subagent work, checks run, cleanup performed, risks/blockers, memory-worthy notes, do-not-promote notes, and the next recommended gate.
- After writing the report, the worker should tell the user the report path and stop work.

## Report-Only Notes

- The first scaffold used an incorrect spelling. The folder, frontmatter, metadata, references, and report text were corrected to `twb-decommission` before validation.

## Files Updated

- `C:\Users\yrred\.codex\skills\twb-decommission\SKILL.md`
- `C:\Users\yrred\.codex\skills\twb-decommission\agents\openai.yaml`
- `C:\Users\yrred\.codex\skills\twb-decommission\references\decommission-report-schema.md`
- `memory/wiki/memory/multi-agent-orchestration-system.md`
- `memory/AGENTS.md`
- `memory/hot.md`
- `memory/index.md`
- `memory/log.md`
- `C:\Users\yrred\Documents\New project 2\AGENTS.md`

## Next Recommended Gate

Use `twb-decommission` the next time a worker window needs to be retired or restarted, then bring the generated report path back to Bob/orchestrator for memory review.
