# Chat Summary Intake System

## Status

Active workflow - created 2026-05-11.

## Purpose

Use a fresh chat window to ingest summaries from active working windows, remove redundant or weak material, and promote only useful durable information into the Obsidian memory system.

This is for chat summaries, not raw project files.

## Core Rule

The intake chat acts as the orchestrator for memory intake.

It should:

- read the current memory map first
- classify each useful item
- reject noise and duplicates
- update only the relevant permanent memory pages
- write a short intake report
- update `hot.md`, `index.md`, and `log.md` only when the intake changes active context or adds important new pages

It should not:

- paste whole chat summaries into the wiki
- create giant transcript dumps
- promote guesses as facts
- overwrite raw evidence
- update unrelated wiki pages
- preserve redundant process chatter

## Intake Inputs

The user may paste:

- working-window summaries
- decisions from active chats
- implementation summaries
- marketing summaries
- bug or playtest summaries
- deployment summaries
- open questions
- next-step lists

## Step-By-Step Workflow

1. Read `memory/AGENTS.md`.
2. Read `memory/hot.md`.
3. Read `memory/index.md`.
4. Ask the user to paste one or more working-window summaries if none were provided.
5. Split the pasted material into candidate memory items.
6. Label each candidate as Fact, Decision, Hypothesis, Signal, Warning, Open Question, Superseded, Task, or Discard.
7. Compare candidates against existing relevant wiki pages.
8. Discard duplicates, process chatter, weak claims, stale drafts, and unsupported detail.
9. Promote only stable items into the correct permanent pages.
10. Create an intake report under `memory/reports/intake/`.
11. Update `memory/index.md` if new pages were added.
12. Update `memory/hot.md` only if the active focus or next gate changed.
13. Update `memory/log.md` with a brief line describing the intake.

## Placement Map

Use this placement map when promoting memory:

| Item Type | Destination |
|---|---|
| Main-game design fact | `memory/wiki/game-dev/` |
| World Key design fact | `memory/wiki/game-dev/world-keys.md` or a specific game-dev page |
| Marketing decision | `memory/wiki/decisions/marketing-decisions.md` |
| Design decision | `memory/wiki/decisions/design-decisions.md` |
| Technical decision | `memory/wiki/decisions/technical-decisions.md` |
| SEO decision | `memory/wiki/decisions/seo-decisions.md` |
| SEO or market signal | `memory/wiki/marketing/`, `memory/wiki/competitors/`, or an intake report until validated |
| Playtest signal | `memory/wiki/playtesting/` |
| Launch readiness item | `memory/wiki/launch/` |
| Bug or fragility | `memory/wiki/bugs/` |
| Unresolved question | the relevant wiki page's Open Questions section |
| Weak, duplicate, or temporary detail | intake report only or discard |

## Promotion Standard

Promote an item only when at least one of these is true:

- it is a confirmed user decision
- it changes the current project direction
- it records a real implementation or deployment result
- it captures a repeated playtest or market signal
- it creates or closes an important open question
- it warns against a likely future mistake
- it supersedes an older memory item

## Discard Standard

Discard or keep only in the intake report when an item is:

- repeated elsewhere with no new detail
- speculative without evidence
- a transient to-do already completed
- chat process commentary
- vague encouragement or brainstorming
- draft copy that was rejected
- an implementation detail unlikely to matter later
- contradicted by stronger current memory

## Required Intake Report

Each intake run should write:

```text
memory/reports/intake/YYYY-MM-DD-short-topic.md
```

Report sections:

1. Intake Source
2. Useful Items Promoted
3. Items Kept Only In Report
4. Discarded As Redundant Or Unuseful
5. Wiki Pages Updated
6. Hot/Index/Log Updates
7. Risks Or Ambiguities
8. Next Gate

## Source Handling

Do not archive the full pasted summary by default.

If a pasted summary contains raw evidence that cannot be safely distilled, ask whether to save it under:

```text
memory/raw/chat-intake/
```

Otherwise, treat the pasted material as temporary intake material and preserve only the useful distilled output.

## Hydration Prompt

Use [[templates/chat-summary-intake-hydration-prompt]] when starting a new intake chat.

## Warning

This workflow is a filter, not a storage bin. If the intake chat saves everything, it has failed in the most tedious possible way.
