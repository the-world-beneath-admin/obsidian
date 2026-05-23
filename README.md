# The World Beneath Obsidian Brain

Backup of Bob's local Obsidian brain for The World Beneath work.

Primary vault:

- `Tesseract/`

Top-level planning notes:

- `hardened-obsidian-agent-system.md`
- `obsidian-workflow-integration-plan.md`

## Backup Policy

This repository intentionally excludes volatile or credential-bearing Obsidian runtime files:

- `.obsidian/workspace*.json`
- `.obsidian/plugins/**/data.json`
- local REST API plugin runtime data
- `.trash/`
- logs, temporary files, local databases, and cache folders

The goal is to preserve the durable brain content, briefs, wiki pages, reports, templates, and source attachments without publishing local API keys or private runtime state.
