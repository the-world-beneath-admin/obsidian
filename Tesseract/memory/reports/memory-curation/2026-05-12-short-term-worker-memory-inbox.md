# Memory Curation Report - 2026-05-12 - Short-Term Worker Memory Inbox

## Task

Set future workers to report into one shared short-term memory folder and require workers to clean up temporary artifacts they create.

## Result

Created the shared short-term worker memory inbox:

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\
```

Updated worker rules, reusable prompts, agent definitions, the TWB-Marketing dashboard handoff, and the hourly memory curation automation so future workers write reports to `memory/short-term/`.

The long-term memory promoter automation now reviews `memory/short-term/` first and checks legacy report folders only when needed.

## Files Changed

- `memory/short-term/README.md`
- `memory/AGENTS.md`
- `memory/wiki/memory/multi-agent-orchestration-system.md`
- `memory/wiki/memory/hourly-memory-curation-automation.md`
- `memory/briefs/current-twb-marketing-app-task.md`
- `memory/briefs/current-game-dev-task.md`
- `memory/briefs/current-marketing-task.md`
- `memory/briefs/current-memory-audit-task.md`
- `memory/briefs/current-intake-task.md`
- `templates/orchestrator-worker-handoff-prompt.md`
- `templates/specialist-hydration-prompt.md`
- `templates/task-brief-game-dev.md`
- `templates/task-brief-seo-marketing.md`
- `memory/reports/memory-curation/2026-05-12-short-term-worker-memory-inbox.md`
- `memory/index.md`
- `memory/hot.md`
- `memory/log.md`
- `C:\Users\yrred\Documents\New project 2\AGENTS.md`
- `C:\Users\yrred\Documents\New project 2\.codex\agents\orchestrator.toml`
- `C:\Users\yrred\Documents\New project 2\.codex\agents\app-dev.toml`
- `C:\Users\yrred\Documents\New project 2\.codex\agents\game-dev.toml`
- `C:\Users\yrred\Documents\New project 2\.codex\agents\seo-marketing.toml`
- `C:\Users\yrred\Documents\New project 2\.codex\agents\launch-coordinator.toml`
- `C:\Users\yrred\Documents\New project 2\.codex\agents\memory-curator.toml`
- `C:\Users\yrred\Documents\New project 2\.codex\agents\intake.toml`
- `C:\Users\yrred\Documents\New project 2\twb-marketing-presence-agent\DASHBOARD_MILESTONE_HYDRATION_PROMPT.md`
- `C:\Users\yrred\Documents\New project 2\twb-marketing-presence-agent\SUBAGENT_HYDRATION_PROMPT.md`

## Automation Updated

- `TWB Hourly Memory Curation` now uses `memory/short-term/` as its primary review inbox.

## Memory-Worthy Notes

- Decision - Future workers should write relevant reports and memory-worthy notes to `memory/short-term/`.
- Decision - The long-term memory promoter automation should review `memory/short-term/` first.
- Decision - Worker agents must clean up their own temporary artifacts when no longer needed.
- Warning - Workers must not delete source files, user files, raw evidence, reports, or another worker's work while cleaning up.

## Kept Only In Report

- Exact report filename conventions can be adjusted later if they prove awkward.
- Legacy role-specific report folders remain in place for old work.

## Rejected Or Ignored

- No existing reports were moved or deleted.

## Next Recommended Gate

Use the updated dashboard milestone hydration prompt for the app-dev worker, then let the hourly promoter automation review the resulting short-term report.
