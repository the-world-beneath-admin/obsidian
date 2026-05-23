# Multi-Agent Orchestration System

## Status

Active operating workflow - created 2026-05-11.

## Purpose

Make the orchestrator and worker-agent system explicit for game development, SEO marketing, launch work, memory audits, and chat-summary intake.

## Core Model

```text
User
  -> Orchestrator
  -> Narrow task brief
  -> Specialist worker/coordinator
  -> Worker-spawned execution child subagent(s)
  -> Child report back to worker
  -> Worker review/integration and short-term report
  -> Orchestrator review
  -> Permanent Obsidian memory update
```

## Important Reality Check

Custom agent files define reusable roles. They do not automatically make the system run itself.

The orchestrator still has to:

- read the memory state
- create the brief
- choose the specialist
- hand off a bounded task
- review the report
- promote only durable memory

The workers do not own permanent memory. Worker windows now coordinate their lane and keep their own context smaller by spawning bounded child subagents for actual work.

## Worker-Spawned Execution Subagents

Worker windows may answer simple questions, clarify scope, inspect narrow status, review child reports, and write their own short-term reports inline.

For substantive execution, worker windows should spawn a bounded child subagent instead of doing the work inline. This includes:

- implementation
- debugging
- playtesting and QA
- research
- asset processing or integration
- build/test verification
- substantial file review

Child subagents are execution children, not new permanent workers.

Rules:

- Use one child subagent when the work has one write area or cannot be cleanly split.
- Use parallel child subagents only for genuinely separate read-only questions or disjoint write areas.
- Every child prompt must include scope, read-first files, allowed write paths, forbidden write paths, done criteria, report-back instructions, and the no-grandchildren rule.
- Child subagents must not spawn further agents.
- Child subagents must not update `memory/wiki/`, `memory/index.md`, `memory/hot.md`, or `memory/log.md`.
- Child subagents must not stage, commit, reset, deploy, broad-clean, or delete source/user/raw/report files unless the worker prompt explicitly allows a narrow operation.
- While child work is active, the worker should set a Codex thread heartbeat/check-in for itself, currently about every 2 minutes, until the child reports back or is closed.
- The heartbeat should check status, continue review, and prevent stale chat state. It must not create cron automations, spawn duplicate children, or restart the same task.
- The worker must review child results before integrating them or reporting them to the user.
- When the user says `REPORT`, `report`, or `decommission`, the worker writes one short-term report summarizing the child work and current state.
- Workers may use the local Codex skill `twb-decommission` to create that final short-term report and stop cleanly.

## TWB Workflow Skills

The repeated advisory triad, worker commissioning, and worker shutdown report workflows are now formalized as local Codex skills under:

```text
C:\Users\yrred\.codex\skills\
```

Use:

- `twb-commission` for creating or updating project/general worker briefs, worker folders, and hydration prompts. In this system, user wording like "agent" means "worker."
- `twb-audit` for substantial audits, reviews, stress-tests, worker-report reviews, memory-promotion reviews, architecture checks, launch/marketing checks, and risky implementation result reviews.
- `twb-planning` for substantial implementation plans, task briefs, feature approaches, research plans, marketing plans, worker handoffs, and master plans before execution.
- `twb-decommission` for worker-window final reports back to Bob/orchestrator when a worker is being stopped, retired, summarized, or restarted.

The triad roles are:

- Helpful Genius: constructive expert, strongest practical path, useful examples.
- Devil's Advocate: skeptical risk finder, failure modes, overreach, policy and architecture risks.
- Doe-Eyed Intern: obvious-question asker, unclear terms, missing setup, handoff clarity.

Use full triad loops for high-risk or cross-system work:

1. Triad audit or planning pass.
2. Main-agent consolidation.
3. Triad re-audit of the consolidated result.
4. Final main-agent synthesis and next gate.

Use lightweight triad loops for medium-risk work. Skip the skills for trivial edits, simple answers, routine status, and mechanical cleanup.

The skills do not override the orchestration hierarchy. The main worker or orchestrator owns the final synthesis; child subagents remain bounded execution/advisory children and must not spawn further agents or update permanent memory. `twb-commission` prepares scoped worker entry points; it does not justify broad or vague workers. `twb-decommission` writes one report under `memory/short-term/` for Bob/orchestrator review and must not update permanent memory.

## Short-Term Worker Memory

Future worker agents should write task reports and memory-worthy notes to:

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\
```

This folder is the shared short-term memory inbox for the long-term memory promoter automation.

Workers should also clean up their own mess:

- remove temporary files, scratch files, generated screenshots, throwaway logs, and dev artifacts they created when no longer needed
- leave source files, user files, raw evidence, reports, and other workers' changes alone
- explain any remaining temporary artifacts in their report

Permanent wiki memory is still owned by the orchestrator or the approved promoter automation.

## Current Project-Scoped Agents

Stored under:

```text
C:\Users\yrred\Documents\New project 2\.codex\agents\
```

Current roles:

| Agent | Job |
|---|---|
| orchestrator | Controls task routing, memory promotion, briefs, and final user communication |
| game-dev | Bounded implementation, debugging, testing, and game-system work |
| app-dev | Bounded local app scaffolding, implementation, testing, and reports for TWB-Marketing app work |
| twb-creature-spritesheet-worker | Bounded Tier 1 creature walk sprite-sheet generation, repacking, QA, queue updates, cleanup, and short-term reports |
| glassroot-garden-worker | Bounded Phaser/Vite implementation, playtesting, and reporting for The Garden / Glassroot Garden World Key prototype |
| twb-unity-worldmap-worker | Bounded main-game Unity world map, HoloGlyph UI, and starter guardian validation work |
| twb-main-game-reward-flow-worker | Bounded main-game Unity dungeon run reward-flow verification, temporary dev helper review, and narrow reward UI polish |
| twb-unity-starter-pets-worker | Bounded main-game Unity starter-pet implementation, validation, art acceptance checks, and reporting |
| twb-shared-platform-worker | Bounded website account, shared inventory, shared pets, starter selection, and World Key persistence contract work |
| alchemy-lab-worldkey-worker | Bounded Phaser/Vite implementation, cave/pet loop testing, and reporting for The Alchemy Lab World Key |
| twb-trenchworks-worker | Bounded Unity 2D research/planning for the TWB Trenchworks factory/logistics and automated trench-war game |
| twb-trenchworks-playtest-worker | Longer-lived bounded Unity 2D prototype steward for Trenchworks play-mode entry fixes, playtesting, diagnostics, and small stabilization |
| seo-marketing | SEO, positioning, store copy, competitor research, campaign analysis |
| launch-coordinator | itch.io, Kickstarter, Steam, website funnel, and release-readiness work |
| memory-curator | Memory audits, contradictions, stale claims, duplicate notes, missing sources |
| intake | Pasted chat-summary filtering and intake-report generation |

## Deferred Specialist Candidates

| Candidate | Use Only After |
|---|---|
| social-ops | Platform-specific rules, account permissions, and manual approval workflow have been reviewed |

Warning: `social-ops` must never be scoped to spam, fake engagement, rule evasion, or auto-posting without explicit user approval and a platform-safe integration plan.

## When To Use Workers

Use workers for:

- implementation work with clear scope
- local app development work with clear write paths
- bug investigations
- playtest issue analysis
- SEO research
- competitor research
- Steam, itch.io, Kickstarter, or website launch work
- memory audits
- pasted summary intake

Do not use workers for:

- one-line text edits
- trivial file lookups
- simple status answers
- vague brainstorming with no output target
- decisions that require the user directly

## Orchestrator Responsibilities

The orchestrator must:

1. Read `memory/hot.md`.
2. Read `memory/index.md`.
3. Read `memory/wiki/game-dev/project-hierarchy.md` when project scope matters.
4. Create or update a narrow task brief.
5. Specify scope, allowed write paths, forbidden write paths, sources to read, done criteria, and report destination.
6. Direct the specialist.
7. Review the specialist report.
8. Promote only stable memory.
9. Update `hot.md`, `index.md`, and `log.md` only when needed.
10. Tell the user what changed and what remains blocked.

## Worker Responsibilities

Each worker must:

- read its task brief first
- read only named memory pages unless more context is required
- stay inside its allowed write scope
- keep simple answers, clarification, scope control, child-report review, and short-term report writing inline
- spawn bounded child subagents for actual implementation, investigation, playtesting, QA, research, asset work, or other substantive execution
- give child subagents scope, read-first files, allowed write paths, forbidden write paths, done criteria, report-back instructions, and the rule that they must not spawn further agents
- set a Codex thread heartbeat/check-in, currently about every 2 minutes, while child work is active
- review child results before integrating or reporting them
- avoid direct permanent memory changes unless explicitly authorized
- write a report in `memory/short-term/` unless the brief explicitly says otherwise
- list checks run and risks
- identify memory-worthy notes without promoting them directly
- clean up temporary artifacts they created, without deleting source/user/raw/report files or other workers' work

## Handoff Packet

Every worker handoff should include:

- task name
- scope
- brief path
- read-first pages
- allowed write paths
- forbidden write paths
- done criteria
- report destination, normally `memory/short-term/`
- risks to watch
- instruction not to revert other workers' edits
- instruction to clean up temporary artifacts created by the worker
- instruction that the worker coordinates the lane and should use bounded child subagents for substantive execution
- instruction to set a Codex thread heartbeat/check-in, currently about every 2 minutes, while child work is active

Use [[templates/orchestrator-worker-handoff-prompt]] for reusable handoffs.

## Fresh Window Usage

If using separate chat windows rather than built-in subagents:

1. Open a new chat window.
2. Paste the matching specialist hydration prompt or the worker handoff prompt.
3. Include the task brief path.
4. Have the worker write only its report and allowed files.
5. Bring the worker report back to the orchestrator chat.
6. Let the orchestrator decide what enters permanent memory.

## Built-In Subagent Usage

When the user explicitly asks to use subagents, specialist agents, worker agents, or parallel work, the orchestrator can spawn top-level workers with a bounded prompt.

Current standing policy: worker windows should also spawn bounded execution child subagents for substantive work, while keeping only simple answers and orchestration inline.

Rules:

- The orchestrator creates or updates the relevant brief before top-level worker handoff.
- A worker may spawn execution child subagents for its own lane.
- Child subagents must not spawn further agents.
- Workers should use a Codex thread heartbeat/check-in, currently about every 2 minutes, while child subagents are active.
- Do not split overlapping write areas across parallel child subagents.
- Do not allow child subagents to update permanent memory.
- Review reports before promotion.

## Plugin And Skill Decision

Current recommendation:

- Use custom agents now.
- Use Obsidian templates now.
- Use hydration prompts now.
- Use `twb-commission` when creating, recommissioning, or hydrating project/general workers.
- Use `twb-audit` and `twb-planning` for the proven advisory-triad audit and planning workflows.
- Use `twb-decommission` when retiring or restarting a worker window so it writes a consistent short-term report back to Bob/orchestrator.
- Defer a full plugin unless the system needs custom tools, external integrations, or packaging beyond prompt/workflow skills.
- Defer additional skills until repeated usage proves what should be automated.

Reason:

Plugins are useful when there are custom tools, external integrations, or reusable packaged capabilities. This system currently needs disciplined prompts, briefs, and memory rules more than code.

## Next Useful Skill Candidate

Future skill name:

```text
twb-obsidian-orchestrator
```

Possible trigger:

Use when the user asks to run The World Beneath Obsidian memory workflow, orchestrate specialist agents, process chat summaries, create task briefs, or promote reports into permanent memory.

Do not create this skill until the workflow has been used enough to see what should be automated and what should stay human-directed.

## Warning

A multi-agent system is useful only if the briefs are narrow. Broad workers create broad messes. Broad messes then require memory-curator work, which is how one invents bureaucracy while pretending to invent efficiency.
