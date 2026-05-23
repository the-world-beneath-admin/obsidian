# Short-Term Worker Memory

## Purpose

This is the shared short-term memory inbox for future worker agents.

Workers should write their task reports, memory-worthy notes, cleanup notes, risks, and follow-up recommendations here so the long-term memory promoter automation has one primary place to review.

## Rules For Workers

- Write one report per substantial task.
- Use a filename that starts with the date and role, for example `2026-05-12-app-dev-dashboard-milestone-1.md`.
- Include what changed, files touched, checks run, safety boundaries, risks, memory-worthy notes, do-not-promote notes, and follow-up recommendations.
- Clean up temporary files, scratch files, generated screenshots, throwaway logs, and dev artifacts created during the task when they are no longer needed.
- Do not delete source files, user files, raw evidence, reports, or work from other workers.
- If a temporary artifact must remain, explain why in the report.
- Do not update `memory/wiki/`, `memory/index.md`, `memory/hot.md`, or `memory/log.md` directly unless the orchestrator explicitly authorizes it.

## Promotion

The long-term memory promoter automation reviews this folder, promotes durable notes into permanent Obsidian memory, and records what was kept or rejected.

