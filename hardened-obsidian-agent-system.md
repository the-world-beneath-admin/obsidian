Hardened version of your idea

Yes — I would build this, but I would tighten the control model hard.

The safe version is not:

Master agent + several smart agents + everyone reads/writes Obsidian

The safe version is:

You
 ↓
Orchestrator
 ↓
Task brief
 ↓
Specialist agent does bounded work
 ↓
Specialist writes report
 ↓
Orchestrator updates Obsidian memory

That keeps the system useful without letting it turn into a messy pile of AI-written notes.

Codex supports this kind of setup because it can use subagents, custom agents, project-scoped agent files, layered AGENTS.md instructions, sandbox controls, and skills. Custom agents can live in .codex/agents/ for a project, and Codex’s docs specifically recommend making custom agents narrow and opinionated instead of broad general-purpose agents.

The hardened architecture
Core principle

The orchestrator owns memory. The subagents do work. The subagents do not directly maintain the permanent Obsidian wiki.

That one rule prevents most of the system from rotting.

What I would remove from your original idea
1. Remove: three separate Obsidian vaults

Bad idea.

Obsidian can open multiple vaults, but Obsidian warns against vaults inside vaults because links are local to a vault and may not update correctly. Obsidian notes are plain Markdown files in a local folder, and external edits refresh automatically, so one clean vault is enough.

Use one vault with sections:

memory/
  wiki/
    game-dev/
    marketing/
    competitors/
    playtesting/
    decisions/
    bugs/
    launch/

Do not create:

game-dev-vault/
marketing-vault/
orchestrator-vault/

That creates link problems, duplication, and memory drift.

2. Remove: subagents maintaining their own memory

Bad idea.

The game-dev agent and marketing agent should not update the permanent wiki themselves.

They should write reports only:

memory/reports/game-dev/
memory/reports/marketing/

Then the orchestrator decides what becomes permanent memory.

Why: if several agents update memory directly, you will get duplicate facts, contradictions, stale summaries, and agents overwriting each other’s context.

3. Remove: subagents scanning a whole wiki section every time

Mostly bad idea.

Instead of saying:

“Marketing agent reads the marketing wiki.”

Say:

“Marketing agent reads the task brief first, then only the pages named in the task brief.”

That keeps the subagent focused.

The brief should act like a mission packet.

4. Remove: master chat as permanent memory

This is important.

Do not rely on one massive orchestrator chat forever. Codex’s own best-practice guidance warns against using one thread per project because context gets bloated and worse over time. Use the chat to operate, but use the Markdown memory files as the real long-term memory.

The orchestrator can be the main control point, but the memory lives in Obsidian, not in the chat thread.

5. Remove: deep agent nesting

Do not let the marketing agent spawn other agents, then those agents spawn more agents.

Codex docs say subagents can spawn, but deeper recursion increases token use, latency, local resource use, and predictability risk. The default depth limit is meant to prevent runaway fan-out.

Use this rule:

Only the orchestrator can spawn or direct subagents. Subagents do not spawn other subagents.

What I would keep from your idea
1. Keep: orchestrator as the control center

This is good.

The orchestrator should:

talk to you
read top-level memory
decide what context matters
create the task brief
assign work to game-dev or marketing agents
review their reports
update Obsidian
keep the memory clean

Codex supports orchestration across subagents, including spawning specialized agents, routing follow-up instructions, waiting for results, and consolidating results. It only spawns a new agent when explicitly asked.

2. Keep: separate specialist agents

Also good.

Use project-scoped custom agents:

.codex/
  agents/
    orchestrator.toml
    game-dev.toml
    marketing.toml
    memory-curator.toml

Codex custom agent files can be placed under .codex/agents/ for project-scoped agents, and each custom agent defines its own name, description, and instructions.

3. Keep: quick-reference memory

Good idea, but make it controlled.

Use quick-reference files like:

memory/wiki/game-dev/_game-dev-quickref.md
memory/wiki/marketing/_marketing-quickref.md

These should be short. Think 1–3 pages max, not a full wiki dump.

They should contain:

current direction
most important constraints
recent decisions
“do not break this” notes
links to deeper pages
4. Keep: task-specific Markdown file

This is one of the strongest parts of your idea.

The orchestrator should create a task file before handing work to a specialist:

memory/briefs/current-game-dev-task.md
memory/briefs/current-marketing-task.md

This file tells the subagent exactly what to read, what to ignore, and what to return.

Final hardened file structure

I would use this:

GameProject/
  AGENTS.md

  .codex/
    config.toml
    agents/
      orchestrator.toml
      game-dev.toml
      marketing.toml
      memory-curator.toml

  memory/
    AGENTS.md
    index.md
    hot.md
    log.md

    briefs/
      current-game-dev-task.md
      current-marketing-task.md
      current-memory-audit-task.md

    wiki/
      game-dev/
        _game-dev-quickref.md
        core-loop.md
        systems.md
        controls.md
        enemies.md
        level-design.md
        technical-constraints.md

      marketing/
        _marketing-quickref.md
        positioning.md
        steam-page.md
        trailer-hooks.md
        campaign-tests.md
        creator-outreach.md

      competitors/
        competitor-index.md
        steam-patterns.md
        review-complaints.md

      playtesting/
        recurring-feedback.md
        loved-moments.md
        confusion-points.md

      decisions/
        design-decisions.md
        marketing-decisions.md
        technical-decisions.md

      bugs/
        known-bugs.md
        fixed-bugs.md
        fragile-systems.md

      launch/
        launch-checklist.md
        wishlist-strategy.md
        press-kit.md

    reports/
      game-dev/
      marketing/
      memory-audits/

    raw/
      playtests/
      competitor-research/
      campaign-results/
      screenshots/
      transcripts/

This gives us one clean memory system, but still separates the types of knowledge.

Agent roles
1. Orchestrator agent

This is the boss agent.

Reads
memory/hot.md
memory/index.md
memory/wiki/decisions/
memory/wiki/playtesting/
relevant quickref files
Writes
memory/briefs/
memory/wiki/
memory/index.md
memory/hot.md
memory/log.md
Does not do
large code changes directly
random marketing output directly
dumping entire chats into memory
rewriting raw evidence
Main job

Turn your rough goal into a clear task, send it to the right specialist, then decide what should become permanent memory.

2. Game-dev agent

This agent handles the game itself.

Reads first
memory/briefs/current-game-dev-task.md
Then reads only what the brief names

Example:

memory/wiki/game-dev/_game-dev-quickref.md
memory/wiki/game-dev/core-loop.md
memory/wiki/bugs/fragile-systems.md
memory/wiki/playtesting/confusion-points.md
Writes
src/
assets/ if needed
memory/reports/game-dev/
Does not write
memory/wiki/
memory/index.md
memory/hot.md
memory/log.md
Main job

Implement, debug, test, and report.

3. Marketing agent

This agent handles positioning, campaigns, copy, competitor research, Steam strategy, trailers, and creator outreach.

Reads first
memory/briefs/current-marketing-task.md
Then reads only what the brief names

Example:

memory/wiki/marketing/_marketing-quickref.md
memory/wiki/marketing/positioning.md
memory/wiki/competitors/steam-patterns.md
memory/wiki/playtesting/loved-moments.md
Writes
marketing/
memory/reports/marketing/
Does not write
memory/wiki/
memory/index.md
memory/hot.md
memory/log.md
Main job

Produce marketing work and report what should be remembered.

4. Memory-curator agent

This is optional but valuable.

It should not run every day. Use it weekly or after a big milestone.

Reads
memory/wiki/
memory/reports/
memory/log.md
Writes
memory/reports/memory-audits/
Does not write directly
memory/wiki/
Main job

Find:

contradictions
stale claims
duplicate pages
missing links
weak evidence
bad summaries
old decisions that should be marked superseded

The orchestrator then decides what to clean up.

The strongest workflow
Game development workflow
You give goal
 ↓
Orchestrator reads hot.md + index.md
 ↓
Orchestrator creates current-game-dev-task.md
 ↓
Game-dev agent reads task brief first
 ↓
Game-dev agent does work
 ↓
Game-dev agent writes report
 ↓
Orchestrator reviews report
 ↓
Orchestrator updates Obsidian memory
 ↓
Orchestrator tells you what changed

Example user prompt to the orchestrator:

We need to make early combat feel less chaotic without making it boring.
Use the game-dev agent. Create a narrow task brief first.
Only update permanent memory after reviewing the game-dev report.
Marketing workflow
You give goal
 ↓
Orchestrator reads hot.md + index.md
 ↓
Orchestrator creates current-marketing-task.md
 ↓
Marketing agent reads task brief first
 ↓
Marketing agent creates output or research
 ↓
Marketing agent writes report
 ↓
Orchestrator reviews report
 ↓
Orchestrator updates Obsidian memory

Example user prompt:

We need a stronger Steam page hook based on what players actually liked.
Use the marketing agent. Pull from playtesting and competitor memory only.
Return copy options and update memory only after the report is reviewed.
The task brief format

Every task brief should be small and strict.

# Current Game Dev Task

## Goal
Fix early enemy spawn pacing so the first 5 minutes feel readable but not empty.

## Read first
- memory/wiki/game-dev/_game-dev-quickref.md
- memory/wiki/game-dev/enemies.md
- memory/wiki/bugs/fragile-systems.md
- memory/wiki/playtesting/confusion-points.md

## Ignore
- marketing campaign notes
- competitor notes unless specifically needed
- launch checklist

## Constraints
- Do not change player movement.
- Do not change the core combat loop.
- Keep difficulty lower before minute 3.
- Make the smallest safe change.

## Done when
- Spawn pacing is changed.
- Relevant tests/checks are run.
- Files touched are listed.
- Risks are listed.
- A report is written to memory/reports/game-dev/.

## Report required
Return:
1. What changed
2. Files touched
3. Tests/checks run
4. Risks
5. Memory-worthy notes
6. Follow-up recommendations

That is not fluff. That is the control layer.

The report format

Subagents should report in a predictable format.

# Game Dev Report — YYYY-MM-DD — Enemy Spawn Pacing

## Task
What the agent was asked to do.

## Result
What changed.

## Files touched
List only changed files.

## Checks run
What was tested or verified.

## Risks
What might break or need review.

## Memory-worthy notes
Only stable facts, decisions, bugs, and lessons.

## Do not promote to memory
Ideas, guesses, temporary experiments, or weak claims.

The “do not promote to memory” section matters. It helps the orchestrator avoid polluting the wiki with random ideas.

Memory rules
Permanent memory must be labeled

Every important memory item should be one of these:

Type	Meaning
Fact	Confirmed project truth
Decision	Something we chose and should follow
Hypothesis	A guess we are testing
Signal	Evidence from players, market, competitors, or tests
Warning	A known danger or mistake to avoid
Open question	Something unresolved
Superseded	Old info replaced by a newer decision

This prevents marketing guesses from being treated like design facts.

Example:

## Signal — 2026-05-10
Playtesters repeatedly liked the fast combat moments, but several were confused by enemy spawns before they understood movement.

Source: memory/raw/playtests/2026-05-10-playtest-notes.md

That is better than:

Players like fast combat.

The first one is useful. The second one is too vague and dangerous.

Permissions model
Orchestrator

Can write:

memory/wiki/
memory/briefs/
memory/index.md
memory/hot.md
memory/log.md
Game-dev agent

Can write:

src/
assets/
memory/reports/game-dev/

Cannot write:

memory/wiki/
Marketing agent

Can write:

marketing/
memory/reports/marketing/

Cannot write:

memory/wiki/
Memory-curator agent

Can write:

memory/reports/memory-audits/

Cannot directly rewrite permanent memory unless the orchestrator assigns that cleanup step.

Codex sandboxing and approvals can help enforce this because the CLI/app can restrict write access and ask for approval depending on the sandbox and approval settings. Defaults include no network access and write access limited to the active workspace unless configured otherwise.

AGENTS.md strategy

Codex reads AGENTS.md files before it starts work. It layers global guidance, project guidance, and closer directory guidance, with closer files overriding broader ones. The default combined project-doc limit is 32 KiB, so the files should stay short.

Use AGENTS.md for stable rules only.

Do not cram the whole wiki into AGENTS.md.

Root AGENTS.md

Purpose:

project identity
build/test commands
high-level workflow
agent routing rule
memory ownership rule

Important rule:

Permanent memory is owned by the orchestrator only. Specialist agents may write reports, but they must not update memory/wiki directly.
memory/AGENTS.md

Purpose:

memory format
raw source rules
no-secrets rule
labeling system
update rules

Important rule:

Do not rewrite raw sources. Do not delete old decisions. Mark old decisions as superseded instead.
src/AGENTS.md

Purpose:

coding standards
engine-specific rules
test/build commands
fragile systems
no-touch rules
marketing/AGENTS.md

Purpose:

voice
audience
platform rules
Steam page style
campaign format
evidence standards
Codex custom agents

The project should have these:

.codex/agents/orchestrator.toml
.codex/agents/game-dev.toml
.codex/agents/marketing.toml
.codex/agents/memory-curator.toml

Keep them short. Custom agents should define job boundaries, not contain the whole operating manual.

For example, the game-dev agent should say:

You are the game development specialist.
Read the current game-dev task brief first.
Do not update memory/wiki.
Write a report to memory/reports/game-dev when done.
Make the smallest safe code change.
Run the relevant checks when possible.

That is enough. The details live in the task brief and wiki pages.

When to use subagents

Use subagents for:

game feature implementation
bug investigation
playtest issue analysis
competitor research
Steam page copy passes
campaign analysis
code review
memory audits

Do not use subagents for every tiny task.

Bad use:

Change one button label.

Good use:

Analyze playtest feedback, identify the top onboarding problems, suggest fixes, and update the game-dev brief.

Codex notes that subagent workflows consume more tokens than comparable single-agent runs, so they should be used when the split actually helps.

Where it will still fail
1. Memory will get bloated

Fix:

quickrefs must stay short
index must stay current
stale items get marked superseded
weekly memory audit
2. The orchestrator may summarize too aggressively

Fix:

raw sources stay untouched
permanent claims link back to source files
memory items get labels: fact, decision, signal, hypothesis, warning
3. Marketing may distort game direction

Fix:

marketing memory cannot create game design decisions
marketing can create signals and hypotheses
only orchestrator can promote a marketing insight into a design decision
4. Game-dev may ignore marketing context

Fix:

orchestrator includes marketing/player context only when relevant
game-dev agent reads task brief first, not the whole marketing wiki
5. Agents may make changes in the wrong place

Fix:

directory-specific AGENTS.md
clear write permissions
report-only rule for subagents
use worktrees for risky code work
keep memory updates centralized
6. You may create too much process

Fix:

Start with only:

orchestrator
game-dev agent
marketing agent
memory/
briefs/
reports/
wiki/

Add memory-curator later.

Do not start with plugins, automations, MCP, browser tools, analytics tools, and ten agents on day one.

Best first version
Version 1 should be this
One Obsidian vault.
One orchestrator.
Two specialist agents.
One task brief per active task.
Reports from specialists.
Only orchestrator updates permanent memory.

That is enough to get the value.

Version 1 should not include
multiple vaults
agents writing permanent memory directly
deeply nested agents
automatic memory updates after every tiny task
giant AGENTS.md files
plugin dependency as the foundation
unrestricted read/write access everywhere
The final hardened system
User
 ↓
Orchestrator Agent
 - reads hot.md and index.md
 - creates narrow task brief
 - chooses specialist
 - reviews specialist report
 - updates Obsidian memory
 ↓
Specialist Agent
 - reads task brief first
 - reads only named wiki pages
 - does the work
 - writes report only
 ↓
Orchestrator
 - promotes useful facts/decisions/signals into memory
 - updates quickref, index, hot, and log

This is the clean version of your idea.

It is not “three agents with memory.” It is better than that:

One memory system, one memory owner, several narrow workers.

That is the version I would actually trust for game development and marketing.
