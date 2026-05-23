# Obsidian Workflow Integration Plan

## Purpose

Use one Obsidian vault as the long-term memory system for game design, playtesting, production decisions, and SEO marketing. Codex remains the active working assistant, but Obsidian becomes the durable source of truth.

The core rule is simple:

The orchestrator owns permanent memory. Specialist agents do bounded work and write reports. Permanent Obsidian notes are updated only after review.

## Scope

This plan integrates Obsidian into two workflows:

1. Game design and development workflow
2. SEO marketing workflow for the games being created

It deliberately starts with a lightweight version. The first version should prove the habit before adding automation, analytics integrations, plugins, or extra agents.

## Non-Negotiable Rules

- Use one Obsidian vault, not multiple vaults.
- Do not put a vault inside another vault.
- Do not let specialist agents maintain permanent memory directly.
- Subagents write reports only.
- The orchestrator reviews reports before updating permanent memory.
- Raw source material is never rewritten.
- Old decisions are marked superseded instead of deleted.
- Every permanent memory item should be labelled as Fact, Decision, Hypothesis, Signal, Warning, Open Question, or Superseded.
- Quick reference files must stay short enough to be useful.
- Task briefs control what each specialist reads and ignores.

## Formal Step-By-Step Plan

### Step 1 - Confirm the Obsidian vault location

Use this folder as the working Obsidian integration location:

```text
C:\Users\yrred\Desktop\Obsidian Integration
```

If this becomes the actual Obsidian vault, open this folder directly in Obsidian. If a separate vault already exists later, move the structure into that vault rather than creating competing vaults.

Deliverable:

- One confirmed Obsidian vault location.

Done when:

- Obsidian can open the folder and display the Markdown files.

### Step 2 - Create the memory structure

Create the project memory folder structure inside the vault.

Recommended structure:

```text
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
      seo-strategy.md
      keyword-research.md
      steam-page.md
      trailer-hooks.md
      campaign-tests.md
      creator-outreach.md

    competitors/
      competitor-index.md
      steam-patterns.md
      review-complaints.md
      seo-patterns.md

    playtesting/
      recurring-feedback.md
      loved-moments.md
      confusion-points.md

    decisions/
      design-decisions.md
      marketing-decisions.md
      technical-decisions.md
      seo-decisions.md

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
    seo/
    memory-audits/

  raw/
    playtests/
    competitor-research/
    campaign-results/
    keyword-research/
    screenshots/
    transcripts/
```

Deliverable:

- A clean one-vault memory structure.

Done when:

- Every folder exists and empty placeholder Markdown files exist for the main wiki pages.

### Step 3 - Define memory ownership

Add memory rules to `memory/AGENTS.md`.

The essential rule:

```text
Permanent memory is owned by the orchestrator only. Specialist agents may write reports, but they must not update memory/wiki directly.
```

Also include:

- Do not rewrite raw sources.
- Do not delete old decisions.
- Mark old decisions as superseded.
- Claims in permanent memory must cite a source when possible.
- Weak ideas stay in reports until validated.

Deliverable:

- `memory/AGENTS.md`

Done when:

- The memory rules are short, clear, and enforceable.

### Step 4 - Create the project-level operating rules

Create or update the root `AGENTS.md` for the game project.

It should define:

- Project identity
- Build and test commands
- Game development workflow
- SEO marketing workflow
- Agent routing rules
- Memory ownership rules
- Report-first workflow for specialists

Deliverable:

- Root `AGENTS.md`

Done when:

- Codex can understand where work happens, which agent should handle it, and who may update memory.

### Step 5 - Create the Codex custom agents

Create these project-scoped custom agent files:

```text
.codex/
  agents/
    orchestrator.toml
    game-dev.toml
    marketing.toml
    seo-marketing.toml
    memory-curator.toml
```

Keep each custom agent narrow.

The first version should use:

- `orchestrator.toml`
- `game-dev.toml`
- `seo-marketing.toml`

The `marketing.toml` and `memory-curator.toml` agents can be added when the workflow proves itself.

Deliverable:

- Custom agent definitions.

Done when:

- Each agent has a clear job boundary, read rules, write rules, and report format.

### Step 6 - Add note templates

Create templates for common note types.

Recommended templates:

```text
templates/
  task-brief-game-dev.md
  task-brief-seo-marketing.md
  game-dev-report.md
  seo-marketing-report.md
  decision-entry.md
  signal-entry.md
  competitor-entry.md
  playtest-summary.md
  weekly-memory-audit.md
```

Deliverable:

- Reusable Markdown templates.

Done when:

- Starting a new task brief or report requires filling in a template, not inventing a format.

### Step 7 - Seed the game design memory

Add the first stable game design notes.

Start with:

- Core loop
- Player fantasy
- Primary verbs
- Current mechanics
- Known fragile systems
- Controls
- Current design constraints
- Current open design questions

Use labels:

- Fact
- Decision
- Hypothesis
- Warning
- Open Question

Deliverable:

- Initial game design wiki pages.

Done when:

- A new Codex thread can read the quickref and understand the game direction without needing old chat history.

### Step 8 - Seed the playtesting memory

Create the basic playtesting memory layer.

Start with:

- Recurring feedback
- Loved moments
- Confusion points
- Raw playtest notes
- Open questions for the next playtest

Important rule:

Raw playtest notes go in `memory/raw/playtests/`. Summaries and conclusions go in `memory/wiki/playtesting/`.

Deliverable:

- Playtesting wiki pages and raw-source folders.

Done when:

- The game-dev agent can use playtest evidence without reading every raw note.

### Step 9 - Define the game design task workflow

Use this loop for game work:

```text
User goal
  -> orchestrator reads hot.md and index.md
  -> orchestrator creates current-game-dev-task.md
  -> game-dev agent reads the task brief first
  -> game-dev agent reads only named files
  -> game-dev agent implements or investigates
  -> game-dev agent writes a report
  -> orchestrator reviews the report
  -> orchestrator updates permanent memory
  -> orchestrator summarizes the result to the user
```

Deliverable:

- A repeatable game-dev task brief and report flow.

Done when:

- Every meaningful game design or development task produces a report before memory changes.

### Step 10 - Define the design decision workflow

Every meaningful design choice should become a decision entry.

Each decision entry should include:

- Decision
- Date
- Reason
- Source
- Affected systems
- Risks
- Superseded by, if replaced later

Deliverable:

- `memory/wiki/decisions/design-decisions.md`

Done when:

- Design direction is no longer buried in chat messages.

### Step 11 - Seed the SEO marketing memory

Create the SEO marketing layer.

Start with:

- Target audience
- Genre keywords
- Steam tags
- Search phrases players might use
- Competitor store pages
- YouTube/search content angles
- Landing page topics
- Press and creator angles
- Wishlist strategy

Add these files:

```text
memory/wiki/marketing/seo-strategy.md
memory/wiki/marketing/keyword-research.md
memory/wiki/competitors/seo-patterns.md
memory/wiki/decisions/seo-decisions.md
memory/raw/keyword-research/
```

Deliverable:

- Initial SEO marketing wiki pages.

Done when:

- The SEO marketing agent can create a task brief from actual game positioning, not generic marketing sludge.

### Step 12 - Define the SEO research workflow

Use this loop for SEO research:

```text
SEO question
  -> orchestrator creates current-marketing-task.md
  -> seo-marketing agent reads only the named sources
  -> seo-marketing agent researches keywords, competitors, or content angles
  -> seo-marketing agent writes report to memory/reports/seo/
  -> orchestrator promotes only stable findings into memory/wiki/
```

SEO research should separate:

- Signals: observed search, competitor, player, or market evidence
- Hypotheses: possible positioning or content ideas
- Decisions: chosen SEO direction
- Open Questions: items needing validation

Deliverable:

- SEO research report workflow.

Done when:

- Keyword and competitor findings are traceable back to raw notes or sources.

### Step 13 - Define the SEO content workflow

Use Obsidian to manage SEO content planning for each game.

Track:

- Store page copy
- Steam short description
- Steam long description
- Capsule text themes
- Website page titles
- Meta descriptions
- Devlog topics
- Trailer titles and descriptions
- YouTube descriptions
- Press kit language
- Creator outreach hooks

Deliverable:

- `memory/wiki/marketing/seo-strategy.md`
- `memory/wiki/marketing/steam-page.md`
- `memory/wiki/launch/press-kit.md`

Done when:

- SEO content is connected to game design truth, player signals, and competitor evidence.

### Step 14 - Define the Steam and store page workflow

Use this loop before major store-page changes:

```text
Store page goal
  -> orchestrator reviews positioning, playtesting signals, and competitor memory
  -> seo-marketing agent drafts options
  -> seo-marketing agent reports rationale and risks
  -> orchestrator promotes selected copy and decisions into memory
  -> final copy is stored in the marketing or launch wiki
```

Track:

- Current hook
- Alternate hooks
- Target keywords
- Genre signals
- Player-loved moments
- Competitor patterns
- Copy tests
- Final selected copy

Deliverable:

- Store page memory workflow.

Done when:

- Store page changes are deliberate and tied to evidence.

### Step 15 - Define the report-to-memory promotion process

After each specialist report, the orchestrator should decide what gets promoted.

Promote:

- Confirmed facts
- Final decisions
- Repeated playtest signals
- Strong SEO signals
- Warnings
- Open questions

Do not promote:

- One-off guesses
- Draft copy that was rejected
- Temporary experiments
- Weak competitor assumptions
- Raw chat summaries with no source

Deliverable:

- A consistent promotion checklist.

Done when:

- Obsidian memory gets cleaner over time instead of larger and vaguer.

### Step 16 - Maintain quick reference files

Keep quickrefs short and current.

Use:

```text
memory/wiki/game-dev/_game-dev-quickref.md
memory/wiki/marketing/_marketing-quickref.md
```

Each quickref should include:

- Current direction
- Important constraints
- Recent decisions
- Warnings
- Open questions
- Links to deeper notes

Deliverable:

- Current game-dev and marketing quickrefs.

Done when:

- A specialist can read a quickref in a few minutes and avoid obvious mistakes.

### Step 17 - Add a weekly memory review

Run a weekly or milestone-based memory review.

Review for:

- Stale claims
- Contradictions
- Duplicate notes
- Missing sources
- Oversized quickrefs
- Old decisions that should be marked superseded
- SEO hypotheses that were never tested
- Game design ideas that were never validated

Deliverable:

- Memory audit report in `memory/reports/memory-audits/`.

Done when:

- The memory system remains useful after several weeks of work.

### Step 18 - Pilot the system with one game task and one SEO task

Run two small pilot tasks before expanding the process.

Pilot game task:

```text
Create a task brief for improving or clarifying one game mechanic. Have the game-dev agent report results. Promote only stable notes into memory.
```

Pilot SEO task:

```text
Create a task brief for one SEO positioning pass. Have the seo-marketing agent produce keyword, competitor, and copy recommendations. Promote only stable signals and decisions into memory.
```

Deliverable:

- One completed game-dev report.
- One completed SEO marketing report.
- Updated quickrefs, index, hot file, and log.

Done when:

- The workflow works once in both lanes without creating memory clutter.

## Day-One Implementation Checklist

For the first usable version, create only:

- One Obsidian vault
- `memory/`
- `memory/briefs/`
- `memory/wiki/`
- `memory/reports/`
- `memory/raw/`
- Root `AGENTS.md`
- `memory/AGENTS.md`
- Orchestrator agent
- Game-dev agent
- SEO marketing agent
- Game-dev quickref
- Marketing quickref
- One game-dev task brief template
- One SEO marketing task brief template
- One report template

Do not add:

- Multiple vaults
- Deep subagent nesting
- Automatic memory updates
- Ten agents
- Heavy plugin dependencies
- Analytics automation before the manual workflow works

## Operating Rhythm

Daily:

- Update `memory/hot.md` with the current focus.
- Use task briefs before specialist work.
- Write reports after specialist work.

Per meaningful task:

- Create a brief.
- Run the specialist.
- Review the report.
- Promote only stable memory.
- Update quickrefs only if the change affects future work.

Weekly:

- Review open questions.
- Mark stale items superseded.
- Tighten quickrefs.
- Check SEO hypotheses against actual evidence.
- Check game design decisions against playtest feedback.

Milestone:

- Run a memory audit.
- Refresh positioning.
- Refresh Steam page memory.
- Review launch checklist.
- Archive old reports that no longer need attention.

## Success Criteria

The integration is working when:

- Game design decisions are easy to find.
- SEO positioning is based on the actual game, not generic marketing.
- New Codex threads can resume work from Obsidian memory.
- Specialist agents stay focused because briefs tell them what to read.
- Raw evidence remains intact.
- The permanent wiki contains stable facts and decisions, not every idea.
- Weekly review improves memory quality instead of simply adding more notes.

## Step Count

This formal plan has 18 steps.
