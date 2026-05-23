# Design Decision Workflow

## Purpose

Use this workflow whenever a game design choice changes how The World Beneath main game, a World Key/subgame, or a shared platform system should be built, tuned, presented, tested, or discussed.

Default scope is the main game. Treat Glassroot Garden or any other World Key as the scope only when the decision source or task brief says so.

The goal is to keep design direction findable and prevent important choices from being buried in chats, reports, or one-off notes.

## What Counts As A Design Decision

Record a design decision when it affects:

- Core loop
- Player fantasy
- Primary verbs
- Controls
- Companion, creature, party, or helper behaviour
- Dungeon, growth, crafting, inventory, society, trade, territory, or reward rules
- World Key-specific loops such as crops, drying, bundling, or contracts
- MVP scope
- UX structure
- Playtest interpretation
- Technical approach that changes game behaviour
- Marketing claims that would constrain design

Do not record:

- Temporary implementation experiments
- Rejected ideas
- One-off guesses
- Minor text edits
- Pure bug fixes with no design implication

## Required Decision Fields

Every design decision must include:

- Status
- Date
- Decision
- Reason
- Source
- Affected Areas
- Risks
- Review Trigger
- Superseded By

## Status Values

- Active - Current direction.
- Candidate - Recommended but not approved.
- Superseded - Replaced by a newer decision.
- Deferred - Not decided yet.

## Source Rules

Use at least one source when possible:

- User instruction
- Specialist report
- Raw playtest note
- Design source doc
- Technical source doc
- Marketing or SEO report

If a decision comes directly from the user, cite it as `User instruction - YYYY-MM-DD`.

If a decision comes from a report, link the report.

If a decision comes from raw evidence, link the raw source and the summary page.

## Supersession Rule

Do not delete old decisions.

When a decision is replaced:

1. Move or copy it under `Superseded Decisions`.
2. Set Status to `Superseded`.
3. Add the newer decision under `Superseded By`.
4. Explain the reason for the replacement.

## Promotion From Reports

The orchestrator may promote a report note into a design decision only if:

- The specialist explicitly marks it as memory-worthy, or
- The user approves it, or
- It resolves an open design question, or
- It changes future implementation or testing behaviour.

Do not promote weak recommendations into decisions. Keep them as hypotheses or open questions.

## Decision Record Template

```markdown
### YYYY-MM-DD - Short Decision Name

- Status: Active
- Decision: Clear statement of what we will do.
- Reason: Why this decision exists.
- Source: Link or source note.
- Affected Areas: Core loop, UI, Companion system, rewards, storage, marketing, etc.
- Risks: What might go wrong or need review.
- Review Trigger: Playtest, milestone, implementation blocker, or date.
- Superseded By: None.
```

## Current Decision Log

- [[design-decisions]]
