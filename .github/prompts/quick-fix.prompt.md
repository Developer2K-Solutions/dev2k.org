---
description: 'Use when: fixing issues in dev2k-page with minimal scope and project-specific constraints'
agent: 'agent'
argument-hint: 'Describe the problem or paste the error message (e.g. TS2322 in header.component.ts:42)'
tools: ['search/codebase', 'edit/editFiles', 'execute/runInTerminal', 'execute/getTerminalOutput']
---

# Quick Fix

## Generic Fix Workflow

1. **Understand** — Read `$input`, the error message, failing spec, and expected behavior.
2. **Root cause** — Isolate to a single file/module first before expanding scope.
3. **Implement** — Make the smallest safe change. No refactoring, no new abstractions.
4. **Verify** — Run the affected spec and check TypeScript: `npx tsc --noEmit`.
5. **Report** — State what changed, why it failed, and why this fix is sufficient.

Then apply these dev2k-page specific rules:

## Project Context

- Use [copilot-project.prompt.md](./copilot-project.prompt.md) as the architectural baseline.
- Keep changes minimal and local.
- No architectural changes within a quick-fix scope.

## Guardrails

- i18n rules: [i18n-copy.instructions.md](../instructions/i18n-copy.instructions.md)
- SCSS/BEM rules: [scss-bem-responsive.instructions.md](../instructions/scss-bem-responsive.instructions.md)
- Test rules: [testing-vitest.instructions.md](../instructions/testing-vitest.instructions.md)

## Verify

- For behavior changes, run at minimum the affected spec file.
- Where practical, confirm full suite status with `npx ng test --watch=false`.

## If `$input` is empty

Ask for the error description, file, and line number if available.
