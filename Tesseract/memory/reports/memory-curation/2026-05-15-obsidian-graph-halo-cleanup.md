# Obsidian Graph Halo Cleanup

## Status

Complete - 2026-05-15.

## Problem

The Obsidian graph view had a large outer halo of dots. A link scan found the noise was mostly transient worker reports and evidence files:

- `157` degree-zero notes in `memory/short-term/`
- additional unlinked or weakly linked report, raw, template, and process files
- one empty root daily note and the default Obsidian welcome note also appeared as clutter

## Changes Made

- Updated `.obsidian/graph.json` so the default graph hides:
  - `memory/short-term/`
  - `memory/reports/`
  - `memory/raw/`
  - `memory/briefs/`
  - `templates/`
  - orphan notes
  - unresolved links
- Added [[wiki/memory/obsidian-graph-hygiene]] to document the display policy.
- Linked the new graph-hygiene note and this report from [[index]].
- Added a concise log entry to [[log]].
- Deleted two root-level vault starter clutter notes:
  - `Welcome.md`, the default Obsidian welcome note
  - `2026-05-11.md`, an empty root daily note

## What Was Not Deleted

No worker reports, raw sources, task briefs, or provenance files were deleted. The cleanup hides transient material from the graph while preserving it for search, review, and memory promotion.

## Next Gate

Reopen or refresh Obsidian Graph View. If the graph still shows clutter, verify the graph search filter is active:

```text
-path:memory/short-term -path:memory/reports -path:memory/raw -path:memory/briefs -path:templates
```

The durable wiki/index graph should now be much cleaner.
