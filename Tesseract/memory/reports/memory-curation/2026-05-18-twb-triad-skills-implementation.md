# TWB Triad Skills Implementation

Date: 2026-05-18

## Source

User requested that the repeated Helpful Genius / Devil's Advocate / Doe-Eyed Intern audit-and-planning workflow be codified as easy-to-type skills named `twb-audit` and `twb-planning`.

## What Changed

- Created local Codex skill `twb-audit` at `C:\Users\yrred\.codex\skills\twb-audit`.
- Created local Codex skill `twb-planning` at `C:\Users\yrred\.codex\skills\twb-planning`.
- Each skill includes a concise `SKILL.md`, OpenAI interface metadata, role prompts, workflow rules, and output schemas.
- Validated both skills with the skill-creator quick validation script.

## Durable Rules Promoted

- Use `twb-audit` for substantial audits, reviews, stress-tests, worker-report reviews, memory-promotion reviews, architecture checks, launch/marketing checks, and risky implementation result reviews.
- Use `twb-planning` for substantial implementation plans, task briefs, feature approaches, research plans, marketing plans, worker handoffs, and master plans before execution.
- Use full triad loops only for high-risk or cross-system work; use lightweight loops for medium-risk work; skip the skills for trivial work.
- The advisory triad supports the main worker/orchestrator. It does not replace final synthesis, orchestration ownership, or permanent-memory promotion rules.
- Child subagents remain bounded and must not spawn further agents or update permanent Obsidian memory.

## Report-Only Notes

- The initial `twb-audit` scaffold failed to create interface metadata because the short description was one character too short. The metadata was regenerated successfully with a valid description.
- Broad inspection of live agent threads was not performed. The durable change came from the user-described repeated workflow plus the triad planning pass.

## Files Updated

- `C:\Users\yrred\.codex\skills\twb-audit\SKILL.md`
- `C:\Users\yrred\.codex\skills\twb-audit\agents\openai.yaml`
- `C:\Users\yrred\.codex\skills\twb-audit\references\role-prompts.md`
- `C:\Users\yrred\.codex\skills\twb-audit\references\audit-output-schema.md`
- `C:\Users\yrred\.codex\skills\twb-audit\references\workflow-rules.md`
- `C:\Users\yrred\.codex\skills\twb-planning\SKILL.md`
- `C:\Users\yrred\.codex\skills\twb-planning\agents\openai.yaml`
- `C:\Users\yrred\.codex\skills\twb-planning\references\role-prompts.md`
- `C:\Users\yrred\.codex\skills\twb-planning\references\planning-output-schema.md`
- `C:\Users\yrred\.codex\skills\twb-planning\references\workflow-rules.md`
- `memory/wiki/memory/multi-agent-orchestration-system.md`
- `memory/AGENTS.md`
- `memory/hot.md`
- `memory/index.md`
- `memory/log.md`
- `C:\Users\yrred\Documents\New project 2\AGENTS.md`

## Next Recommended Gate

Use `twb-audit` on the next substantial worker report, then use `twb-planning` for the next implementation plan that touches multiple systems or has real rework risk.
