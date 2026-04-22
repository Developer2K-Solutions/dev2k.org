# dev2k.org Naming Schema

Use this schema for future Copilot customization files in this workspace.

## Goals

- Keep names predictable.
- Make discovery easy for humans and Copilot.
- Avoid duplicate or overlapping customizations.

## File Types

### Instructions

Pattern: `<scope-or-domain>.instructions.md`

Examples:

- `angular-architecture.instructions.md`
- `scss-bem.instructions.md`
- `i18n-keys.instructions.md`

Rules:

- One concern per file.
- Keep `applyTo` narrow and intentional.
- Prefer domain words over internal abbreviations.

### Agents

Pattern: `<domain>-<purpose>.agent.md`

Examples:

- `layout-regression.agent.md`
- `signals-services.agent.md`
- `pwa-readiness.agent.md`

Rules:

- Use a domain first, then the job.
- Avoid generic names like `helper` or `general-review`.
- Keep the `agent:` frontmatter value aligned with the invoke name.

### Prompts

Pattern: `<verb>-<object>.prompt.md`

Examples:

- `create-component.prompt.md`
- `write-tests.prompt.md`
- `quick-fix.prompt.md`

Rules:

- Start with an action verb.
- Keep prompts workflow-oriented.
- Prefer one prompt per repeatable task.

### Skills

Pattern: `.github/skills/<workflow-name>/SKILL.md`

Examples:

- `feature-change-workflow`
- `ui-regression-check`
- `release-check`

Rules:

- Folder name must match the workflow name.
- Skills are for repeatable multi-step work.
- Avoid creating skills for one-off tasks.

## Description Style

Use this pattern in descriptions:

`Use when: ...`

Good:

- `Use when: changing app-wide theming behavior or data-theme interactions`
- `Use when: adding or refactoring portfolio feature sections`

Avoid:

- vague wording
- file-name-only descriptions
- internal shorthand without context

## Reserved Domain Words

Prefer these project words for consistency:

- `theme`
- `seo`
- `scroll`
- `nav-state`
- `translation`
- `layout`
- `features`
- `legal`
- `pwa`
- `i18n`

## Avoid Duplication

Before creating a new file, check:

1. Can an existing prompt absorb the task?
2. Is this a skill instead of a prompt?
3. Is this an instruction instead of an agent?
4. Does the name overlap semantically with an existing file?
