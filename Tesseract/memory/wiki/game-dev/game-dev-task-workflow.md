# Game Dev Task Workflow

## Purpose

Use this workflow for meaningful The World Beneath main-game work, World Key/subgame work, shared platform work, debugging, tuning, testing, or playtest-response work.

Default scope is the main game. Treat Glassroot Garden or another World Key as the task scope only when the user request or task brief says so.

The goal is to keep game work focused and prevent permanent memory from becoming a heap of half-remembered implementation chatter.

## When To Use This Workflow

Use it for:

- New mechanics
- Bug investigation
- Tuning crop, Companion, reward, timing, or processing systems
- Playtest issue follow-up
- Storage, drying, bundling, contract, or World Key storage changes
- Cloudflare/platform integration work
- Risky UI or interaction changes

Do not use it for:

- Tiny text edits
- One-line visual tweaks
- File organization with no design impact
- Pure note cleanup

## Workflow Loop

```text
User goal
  -> Orchestrator reads hot.md and index.md
  -> Orchestrator checks game-dev quickref and relevant decision/warning pages
  -> Orchestrator creates or updates current-game-dev-task.md
  -> Game-dev specialist reads the task brief first
  -> Game-dev specialist reads only named files unless blocked
  -> Game-dev specialist does bounded work
  -> Game-dev specialist runs relevant checks
  -> Game-dev specialist writes a report
  -> Orchestrator reviews the report
  -> Orchestrator promotes stable memory only
  -> Orchestrator updates hot.md, index.md, log.md, or wiki pages if needed
  -> Orchestrator tells the user what changed
```

## Orchestrator Duties Before Work

Before sending work to the game-dev specialist, the orchestrator must:

1. Read [[memory/hot]].
2. Read [[memory/index]].
3. Read [[_game-dev-quickref]].
4. Check relevant deeper notes such as [[wiki/game-dev/current-mechanics]], [[wiki/game-dev/design-constraints]], [[wiki/game-dev/technical-constraints]], `fragile-systems` if it exists, or [[wiki/game-dev/open-questions]].
5. Create a narrow task brief in [[memory/briefs/current-game-dev-task]].
6. Name only the pages and source files the specialist should read.
7. Define the constraints and done condition.

## Task Brief Requirements

Every meaningful game-dev task brief must include:

- Goal
- Scope
- Read First
- Also Read, if needed
- Ignore
- Constraints
- Done When
- Report Required

The brief should be narrow enough that the specialist can tell what success looks like without reading the whole wiki.

The brief must state whether the work touches the main game, Glassroot Garden, another World Key, or a shared platform/account system.

## Specialist Duties During Work

The game-dev specialist must:

- Read `memory/briefs/current-game-dev-task.md` first.
- Read only the files named in the brief unless more context is necessary.
- Make the smallest safe change.
- Preserve design decisions unless the brief explicitly changes them.
- Run relevant checks when possible.
- Write a report to `memory/reports/game-dev/`.
- Avoid updating `memory/wiki/`, `memory/index.md`, `memory/hot.md`, or `memory/log.md`.

## Report Naming

Use this filename pattern:

```text
YYYY-MM-DD-short-task-name.md
```

Example:

```text
2026-05-11-seed-bag-click-fallback.md
```

## Report Required Sections

Each report must include:

- Task
- Result
- Files touched
- Checks run
- Risks
- Memory-worthy notes
- Do not promote to memory
- Follow-up recommendations

## Memory Promotion Rules

After reviewing the report, the orchestrator may promote:

- Fact - Confirmed project truth
- Decision - Chosen direction
- Signal - Evidence from testing, playtesting, market, or implementation
- Warning - Known risk or fragile area
- Open Question - Unresolved issue worth tracking
- Superseded - Old decision replaced by a newer one

Design decisions must follow [[memory/wiki/decisions/design-decision-workflow]] and be recorded in [[memory/wiki/decisions/design-decisions]].

The orchestrator must not promote:

- Temporary experiments
- Weak guesses
- Rejected ideas
- Implementation notes with no future relevance
- Unsupported claims
- Internal browser verification as player feedback

## Closure Checklist

A game-dev task is closed only when:

- The report exists in `memory/reports/game-dev/`.
- Relevant checks were run or the reason they could not run is documented.
- Risks are documented.
- Memory-worthy notes were reviewed.
- Any permanent memory updates were made by the orchestrator.
- `memory/log.md` records the task outcome when meaningful.
- `memory/hot.md` is updated if the current focus changed.

## Current Status

- Decision - This workflow is active for future meaningful game-dev work.
- Warning - The first actual pilot task should be small enough to test the workflow without creating process sludge.
