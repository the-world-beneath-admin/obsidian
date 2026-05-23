# Worker Subagent Execution Model

Date: 2026-05-17

## Task

Update the TWB orchestration system so worker windows no longer do substantive work inline. Worker windows now coordinate their lane and spawn bounded child subagents for actual execution.

## Reviewed

- `memory/AGENTS.md`
- `memory/wiki/memory/multi-agent-orchestration-system.md`
- Obsidian orchestration templates
- Project `AGENTS.md`
- Project-scoped custom agent definitions
- Existing worker hydration prompts

## Promoted Rule

Worker windows may answer simple questions, clarify scope, inspect narrow status, review child reports, and write short-term reports inline.

For substantive work, worker windows should spawn bounded child subagents. This includes implementation, debugging, playtesting, QA, research, asset processing or integration, build/test verification, and substantial file review.

Child subagents are execution children only. They must not spawn further agents, update permanent Obsidian memory, write outside allowed paths, stage/commit/reset, broad-clean, or delete source/user/raw/report files.

While child work is active, the worker should set a Codex thread heartbeat/check-in for itself, currently about every 2 minutes, until the child reports back or is closed. The heartbeat is for status, review, and continuation only; it must not create cron automations, duplicate children, or restart the same task.

## Files Updated

- `memory/AGENTS.md`
- `memory/wiki/memory/multi-agent-orchestration-system.md`
- `templates/orchestrator-hydration-prompt.md`
- `templates/orchestrator-worker-handoff-prompt.md`
- `templates/specialist-hydration-prompt.md`
- `C:\Users\yrred\Documents\New project 2\AGENTS.md`
- `C:\Users\yrred\Documents\New project 2\.codex\agents\*.toml`
- Active worker hydration prompts under `C:\Users\yrred\Documents\New project 2\`

## Notes

- Historical short-term reports were not edited even where they still quote older no-subagent instructions.
- The superseded Trenchworks playtest prompt now points workers back to the current Trenchworks prompt before substantive work.
- The model remains hierarchical: Bob/orchestrator owns permanent memory, worker windows coordinate lanes, child subagents execute bounded work, and child subagents do not spawn grandchildren.

## Next Gate

Use this model in the next recommissioned worker window. If a worker spawns child work, it should set the 2-minute thread heartbeat immediately after the child handoff.
