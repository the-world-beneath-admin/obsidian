# Daily Memory Audit Cleaner

## Status

Active automation - created 2026-05-15.

## Purpose

Run a daily audit-and-clean pass over the Tesseract Obsidian memory system so current memory stays connected, concise, and useful.

## Scope

The audit checks:

- `memory/hot.md`
- `memory/index.md`
- `memory/log.md`
- current task briefs
- `memory/wiki/`
- `memory/short-term/`
- `memory/reports/`
- `memory/raw/`
- `templates/`

## Automation Workspace

The automation runs from the saved Tesseract Codex project:

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract
```

## Singleton Lock

The automation must acquire:

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\.automation-locks\twb-daily-memory-audit.lock.json
```

If a fresh lock exists, the run should write a skipped-run report and stop.

## Cleanup Policy

Allowed cleanup:

- delete empty files
- delete default starter clutter
- delete duplicate zero-content notes
- fix stale current-task gates
- harden links and hub pathways
- add missing index links for durable wiki notes
- keep `hot.md` short and current

Not allowed without explicit review:

- deleting worker reports
- deleting raw sources
- deleting generated evidence
- deleting short-term reports
- deleting source/project files
- erasing superseded decisions instead of marking them superseded

## Memory Items

- Decision - A daily audit-and-clean automation should maintain the memory archive in addition to the four-hour promoter/curation automation.
- Decision - The daily audit may delete empty or clearly useless local memory clutter, but it must preserve evidence and report all deletions.
- Decision - The daily audit should harden memory pathways by fixing stale task gates, links, indexes, and concise current-state notes.
- Warning - Cleanup must not become evidence loss; non-empty questionable material should be listed as a candidate, not silently removed.
- Warning - `memory/log.md` is oversized and should be split or archived only after a deliberate plan, not as a casual cleanup action.
- Warning - `memory/reports/memory-curation/2026-05-18-210204-twb-hourly-memory-curation.md` contains literal placeholder variables; preserve it as evidence rather than editing away the flaw.
- Source: User request, 2026-05-15.
