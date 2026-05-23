# SEO Research Workflow

## Purpose

Use this workflow for keyword research, competitor research, Steam tag investigation, store-page positioning, content angle research, creator/channel research, and campaign interpretation for The World Beneath main game and any explicitly scoped World Key/subgame.

Default scope is the main game. Treat Glassroot or any other World Key as the scope only when the research brief says so.

The goal is to separate evidence, hypotheses, decisions, and copy ideas so SEO work improves the project instead of smearing marketing fog across the wiki.

## When To Use This Workflow

Use it for:

- Keyword research
- Steam tag research
- Competitor store-page analysis
- Search intent analysis
- Steam page hook research
- Trailer title and description research
- Devlog/topic research
- Creator outreach research
- Campaign result analysis
- Wishlist or conversion hypothesis review

Do not use it for:

- Tiny copy edits
- One-off tagline brainstorming with no research
- Pure design decisions
- Claims about player response without playtest or campaign evidence

## Workflow Loop

```text
SEO question
  -> Orchestrator reads hot.md and index.md
  -> Orchestrator checks marketing quickref, game-dev quickref, and relevant decisions
  -> Orchestrator creates or updates current-marketing-task.md
  -> SEO marketing specialist reads the task brief first
  -> SEO marketing specialist reads only named local sources first
  -> SEO marketing specialist performs bounded research
  -> SEO marketing specialist writes a report to memory/reports/seo/
  -> Orchestrator reviews the report
  -> Orchestrator promotes only stable signals, decisions, warnings, and open questions
```

## Orchestrator Duties Before Research

Before starting SEO research, the orchestrator must:

1. Read [[memory/hot]].
2. Read [[memory/index]].
3. Read [[_marketing-quickref]].
4. Read [[memory/wiki/game-dev/_game-dev-quickref]] so marketing stays tied to game truth.
5. Check relevant decision pages such as [[memory/wiki/decisions/design-decisions]] and [[memory/wiki/decisions/seo-decisions]].
6. Create a narrow research brief in [[memory/briefs/current-marketing-task]].
7. Define the exact research question.
8. Name local memory pages and raw sources the specialist should read.
9. Define whether web/current research is allowed or required.
10. Define the report destination.

## Research Brief Requirements

Every meaningful SEO research brief must include:

- Goal
- Research Question
- Read First
- Also Read
- Allowed External Sources
- Ignore
- Constraints
- Done When
- Report Required

The brief should be narrow enough to prevent the specialist from wandering through the entire internet wearing a monocle and calling it strategy.

## Specialist Duties During Research

The SEO marketing specialist must:

- Read `memory/briefs/current-marketing-task.md` first.
- Read named local sources before external sources.
- Cite or list sources reviewed.
- Separate facts, signals, hypotheses, decision candidates, warnings, and open questions.
- Avoid turning draft copy into permanent strategy.
- Avoid creating game design decisions.
- Write a report to `memory/reports/seo/`.
- Avoid updating `memory/wiki/`, `memory/index.md`, `memory/hot.md`, or `memory/log.md`.

## Source Rules

Use the strongest available sources:

- Existing game memory
- Raw game-design source docs
- Playtest notes
- Campaign results
- Steam/store pages
- Official platform docs where relevant
- Public competitor pages
- Analytics exports, if available later

When using web/current research, record:

- Date checked
- Source link
- What was observed
- Why it matters
- Confidence level

## Evidence Labels

Use these labels in SEO reports:

- Fact - Confirmed project truth.
- Signal - Evidence from search, competitors, Steam pages, campaigns, players, or tests.
- Hypothesis - A testable marketing idea.
- Decision Candidate - A recommendation for orchestrator/user approval.
- Warning - Risk, trap, or misleading pattern.
- Open Question - Something unresolved.
- Superseded - Replaced older marketing or SEO direction.

## Report Naming

Use:

```text
YYYY-MM-DD-short-research-topic.md
```

Example:

```text
2026-05-11-steam-tag-comparison.md
```

## Report Required Sections

Each SEO research report must include:

- Task
- Research Question
- Result
- Sources Reviewed
- Signals
- Hypotheses
- Decision Candidates
- Risks
- Memory-Worthy Notes
- Do Not Promote To Memory
- Follow-Up Recommendations

## Memory Promotion Rules

After reviewing the report, the orchestrator may promote:

- Strong competitor or search signals
- Validated campaign findings
- User-approved positioning decisions
- Warnings that prevent misleading copy
- Open questions worth tracking
- Superseded SEO choices

The orchestrator must not promote:

- Search guesses without evidence
- Unsupported keyword lists
- Rejected copy
- One-off competitor observations with no relevance
- Campaign results without source/context
- Marketing claims that conflict with game design memory

## Current Status

- Decision - This workflow is active for future meaningful SEO research.
- Warning - Current SEO memory is seeded from a light source scan and game truth. It is not validated keyword strategy yet.
