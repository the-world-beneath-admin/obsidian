# Memory Rules

Permanent memory is owned by the orchestrator only. Specialist agents may write reports, but they must not update `memory/wiki/` directly.

## Rules

- Do not rewrite raw sources.
- Do not delete old decisions.
- Mark replaced decisions as superseded.
- Label important memory as Fact, Decision, Hypothesis, Signal, Warning, Open Question, or Superseded.
- Cite a source when possible.
- Keep weak claims, drafts, and experiments in reports until validated.
- Keep quick reference files short and current.

## Chat Summary Intake

Use `memory/wiki/memory/chat-summary-intake-system.md` when the user pastes summaries from other working chats.

- Do not paste whole chat summaries into the wiki.
- Do not archive full pasted summaries by default.
- Promote only durable facts, decisions, signals, warnings, superseded items, open questions, implementation results, deployment results, or next gates.
- Discard redundant, weak, temporary, already-completed, or unuseful information.
- Write intake reports under `memory/reports/intake/`.
- Use `templates/chat-summary-intake-hydration-prompt.md` to start a fresh intake chat.

## Multi-Agent Orchestration

Use `memory/wiki/memory/multi-agent-orchestration-system.md` when the user asks for orchestrator/worker flow, specialist agents, sub-windows, or multi-agent work.

- The orchestrator owns permanent memory.
- Specialists do bounded work and write reports.
- Future workers should write relevant task reports and memory-worthy notes to `memory/short-term/` unless a brief explicitly says otherwise.
- Workers must clean up temporary files and artifacts they created, without deleting source files, user files, raw evidence, reports, or another worker's work.
- Create or update the task brief before handing work to a specialist.
- Use `templates/orchestrator-worker-handoff-prompt.md` for worker handoffs.
- Use `templates/orchestrator-hydration-prompt.md` for a fresh orchestrator chat.
- Use `templates/specialist-hydration-prompt.md` for a fresh worker chat.
- Do not use workers for trivial tasks.
- Worker windows should handle simple answers, clarification, scope control, child-report review, and short-term report writing.
- Worker windows should spawn bounded child subagents for actual implementation, investigation, playtesting, QA, research, asset work, or other substantive execution.
- Worker-spawned child subagents are execution children only: they must not spawn further agents, update permanent memory, or write outside the paths the worker explicitly allows.
- When a worker has active child subagent work that may take more than a brief local step, it should set a Codex thread heartbeat/check-in for itself, currently about every 2 minutes, until the child reports back or is closed. Do not create cron automations or duplicate child workers for this check-in.
- Use the local Codex skills `twb-audit` and `twb-planning` for substantial triad-style audit and planning workflows. Skip them for trivial edits, simple answers, routine status, and mechanical cleanup.
- Use the local Codex skill `twb-commission` when creating, recommissioning, or hydrating a project/general worker. In this system, user wording like "agent" means "worker."
- Use the local Codex skill `twb-decommission` when a worker window needs to summarize back to Bob/orchestrator, write its final report under `memory/short-term/`, and stop cleanly.
- Defer additional plugins or skills until repeated usage shows what should be automated.

## Codex Project Hardening

Use `memory/wiki/memory/codex-project-hardening-standard.md` when improving repo readiness, AGENTS instructions, project docs, test entry points, or failure visibility.

- Each active code project should have local entry-point docs that explain architecture, commands, conventions, tests, and common pitfalls.
- Prefer one reliable verification path per repo or lane. JavaScript apps may use `npm run build`, `npm run typecheck`, `npm run lint`, and `npm test`; Unity/static-site projects may need repo-appropriate PowerShell, `dotnet`, Wrangler, or manual Play Mode checks instead.
- Do not add fake passing test scripts. Missing tests should either be clearly documented as missing or return a useful failure message until real tests exist.
- Make failure easy to see: document setup blockers, stale paths, known flaky checks, required local services, and log locations.
