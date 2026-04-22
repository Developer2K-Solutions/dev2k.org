# Prompt Structure Check (dev2k-page)

Date: 2026-04-22

## Status Update

- Done: generic `code-review` moved to workspace root `.github/prompts/code-review.prompt.md`.
- Done: generic `quick-fix` moved to workspace root `.github/prompts/quick-fix.prompt.md`.
- Done: local `dev2k-page` prompts kept as project wrappers with guardrails.
- Done: dead references removed from `create-component.prompt.md` and `write-tests.prompt.md`.

## Goal

Classify prompts as project-specific or cross-project and recommend where they should live.

## Findings

### Keep in dev2k-page/.github/prompts

- `copilot-project.prompt.md`
  - Reason: full app architecture, services, roadmap, and project conventions.
- `commit-message.prompt.md`
  - Reason: scope list and examples are tightly coupled to this portfolio app.

### Split into generic + local wrapper

- `create-component.prompt.md`
  - Current state: mixed generic workflow and project context.
  - Recommendation: move generic Angular/TDD workflow to workspace root `.github/prompts`, keep a short local wrapper that injects project paths/services.
- `write-tests.prompt.md`
  - Current state: mixed generic test workflow and project references.
  - Recommendation: move generic Vitest workflow to workspace root `.github/prompts`, keep local rules for signals/i18n/theme specifics.

### Best moved to workspace root .github/prompts

- `code-review.prompt.md`
  - Reason: mostly reusable quality checklist pattern.
- `quick-fix.prompt.md`
  - Reason: generic bug-fix flow with minimal project-specific content.

Status: migrated.

## Blocking References (previously missing)

The following referenced files do not exist in workspace root `.github`:

- `.github/prompts/angular/01-coding-standards.md`
- `.github/prompts/angular/02-component-structure.md`
- `.github/docs/TDD-Guide-Angular-Vitest.md`
- `.github/skills/tdd-vitest/SKILL.md`
- `.github/agents/code-review/checklist.md`

Impact before cleanup:

- Prompt instructions contained links that could not be resolved.
- Some workflows were partially non-functional until links were replaced.

Current status:

- References in `create-component.prompt.md` and `write-tests.prompt.md` are now local and valid.
- Wrapper links for `code-review` and `quick-fix` now point to existing root prompt files.

## Recommended Migration Order

1. Create reusable root prompt set: `code-review`, `quick-fix`, generic `create-component`, generic `write-tests`.
2. Keep local project wrappers in `dev2k-page/.github/prompts` that reference local architecture context.
3. Replace broken external references with local `instructions/` files or real root docs.
4. Re-check all markdown links after migration.
