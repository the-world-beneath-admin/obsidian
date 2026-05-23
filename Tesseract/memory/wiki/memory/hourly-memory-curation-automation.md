# Four-Hour Memory Curation Automation

## Status

Active automation plan - created 2026-05-12, changed from hourly to every 4 hours on 2026-05-12.

## Purpose

Review worker reports on a recurring basis and decide what should be promoted into permanent memory, what should stay in reports, and what should be ignored.

## Cadence

- Active schedule: every 4 hours.
- Automation id: `twb-hourly-memory-curation`.
- Display name: `TWB Memory Curation 4h Single Runner`.
- RRULE: `FREQ=HOURLY;INTERVAL=4`.

## Automation Workspace

The Codex automation should run from a single workspace only:

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract
```

Do not configure multiple `cwds` for this automation. Multiple workspaces can fan out into duplicate curation windows that review and edit the same memory files.

The Tesseract vault is intentionally the launch project now that the user saved it as a visible Codex project. The automation may still reference the orchestration workspace by absolute path when needed, but it should not launch from `C:\Users\yrred\Documents\New project 2` or any Unity project folder.

## Singleton Lock

Before reviewing reports or editing memory, the automation must acquire this lock:

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\.automation-locks\twb-memory-curation.lock.json
```

Rules:

- Create the lock with exclusive create/new-file semantics.
- If the lock exists and is less than 6 hours old, write a skipped-run report and stop without promoting memory.
- If the lock exists and is older than 6 hours, treat it as stale, report that, replace it, and continue.
- Release/delete the lock only after the run has written its report and finished memory updates.
- Do not review or promote memory if the lock could not be acquired.

## Scope

The automation primarily reviews the shared short-term worker memory inbox recursively:

- `memory/short-term/`
- Include Markdown reports in dated subfolders, such as `memory/short-term/YYYY-MM-DD-lane-name/report.md`; do not only scan direct child files.

Legacy role-specific report folders may be checked only when the short-term folder points to them or when there is no recent short-term report:

- `memory/reports/app-dev/`
- `memory/reports/game-dev/`
- `memory/reports/marketing/`
- `memory/reports/seo/`
- `memory/reports/intake/`
- `memory/reports/memory-audits/`

## Rules

- Acquire the singleton lock before reading reports or editing memory.
- Read `memory/AGENTS.md`, `memory/hot.md`, `memory/index.md`, and `memory/wiki/memory/multi-agent-orchestration-system.md` first.
- Review `memory/short-term/` recursively first. Do not wander the whole vault unless a short-term report points to a specific source.
- Promote only durable facts, decisions, repeated signals, warnings, open questions, implementation results, deployment results, and next gates.
- Do not promote weak guesses, rejected drafts, temporary experiments, redundant chat material, or unsupported claims.
- Do not delete worker reports or raw sources.
- If a worker left avoidable temporary artifacts, record it as a cleanup issue rather than silently deleting files outside the automation's own outputs.
- Mark replaced items as superseded rather than deleting old decisions.
- Write a curation report for each run under `memory/reports/memory-curation/`.
- Update `memory/hot.md`, `memory/index.md`, and `memory/log.md` only when needed.
- Keep quick reference files short.

## Output

Each run should report:

1. Lock status
2. Reports reviewed
3. Items promoted
4. Items kept only in reports
5. Items rejected or ignored
6. Files changed
7. Open questions or conflicts
8. Next recommended gate

## Memory Items

- Decision - Worker agents should write relevant notes into reports.
- Decision - Future worker agents should report into `memory/short-term/` so the promoter automation has one primary review inbox.
- Decision - Memory curation must scan `memory/short-term/` recursively so worker report folders with evidence files and a nested `report.md` are not missed.
- Decision - Memory curation automation may review reports and promote high-confidence durable memory.
- Decision - Memory curation automation runs once every 4 hours, not hourly.
- Decision - Memory curation automation should use only one configured workspace, `C:\Users\yrred\Desktop\Obsidian\Tesseract`, to keep automation windows visible in the saved Tesseract project.
- Decision - Memory curation automation must acquire `memory\.automation-locks\twb-memory-curation.lock.json` before reviewing or promoting memory.
- Warning - The automation must not treat every worker note as permanent memory.
- Warning - Multiple configured workspaces for the same curation automation can create duplicate windows and duplicate memory edits.
- Warning - Do not launch this automation from Unity folders, the main game project, or the orchestration workspace; use the saved Tesseract Codex project.
- Source: User request, 2026-05-12.
