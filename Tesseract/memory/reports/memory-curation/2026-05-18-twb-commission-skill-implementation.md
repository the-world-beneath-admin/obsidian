# TWB Commission Skill Implementation

Date: 2026-05-18

## Source

User requested a callable `twb-commission` skill so Bob/orchestrator can commission a project worker or general-use worker from a short request such as `twb-commission garden` or `twb-comission app-dev`. User also clarified that "agent" means "worker" in this system.

## What Changed

- Created local Codex skill `twb-commission` at `C:\Users\yrred\.codex\skills\twb-commission`.
- Added `SKILL.md` with commissioning workflow, output modes, required handoff contents, and boundaries.
- Added `references/worker-types.md` for project/general worker mapping.
- Added `references/commissioning-workflow.md` for brief, worker folder, hydration prompt, and memory-promotion rules.
- Added `references/hydration-prompt-schema.md` for a standard worker hydration prompt.
- Added OpenAI interface metadata for the skill.
- Validated the skill with the skill-creator quick validation script.

## Durable Rules Promoted

- Use `twb-commission` when creating, recommissioning, or hydrating a project/general worker.
- Treat user wording like "agent" as "worker."
- A commissioned worker should have scope, read-first files, allowed and forbidden write paths, done criteria, report destination, child-subagent policy, heartbeat/check-in guidance, cleanup rules, and decommission behavior.
- Do not commission workers for trivial tasks or vague goals.
- Do not use commissioning to create risky automation, platform integrations, deployments, account connections, or social posting workflows without the normal safety gates.

## Files Updated

- `C:\Users\yrred\.codex\skills\twb-commission\SKILL.md`
- `C:\Users\yrred\.codex\skills\twb-commission\agents\openai.yaml`
- `C:\Users\yrred\.codex\skills\twb-commission\references\worker-types.md`
- `C:\Users\yrred\.codex\skills\twb-commission\references\commissioning-workflow.md`
- `C:\Users\yrred\.codex\skills\twb-commission\references\hydration-prompt-schema.md`
- `memory/wiki/memory/multi-agent-orchestration-system.md`
- `memory/AGENTS.md`
- `memory/hot.md`
- `memory/index.md`
- `memory/log.md`
- `C:\Users\yrred\Documents\New project 2\AGENTS.md`

## Next Recommended Gate

Use `twb-commission` the next time the user asks for a fresh worker window, especially after a `twb-decommission` report has been returned to Bob/orchestrator.
