# dev2k-page Copilot Setup

Project-specific Copilot setup for the `dev2k-page` repository.

## What is versioned here

- `copilot-instructions.md` as always-on project rules
- `AGENTS.md` as workflow agreement
- `instructions/` for focused file-type and domain guardrails
- `prompts/` for repeatable project tasks
- `docs/` for project planning context
- `governance/` for naming and maintenance rules

## Scope boundaries

- This folder is intentionally committed in `dev2k-page`.
- Workspace-level local files belong to the parent folder `.github/` and are ignored by the parent `.gitignore`.
- Generic cross-project prompts should live in workspace-level `.github/`.
- Only portfolio-specific context should live in this repository folder.

## Recommended usage

1. Start larger tasks with `/copilot-project`.
2. Use prompt workflows for multi-file changes.
3. Keep naming consistent with `governance/naming-schema.md`.
4. Update docs when architecture decisions change.
