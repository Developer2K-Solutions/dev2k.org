---
description: 'Use when: reviewing dev2k-page code with project-specific architecture and quality constraints'
agent: 'agent'
argument-hint: 'File path or component name (e.g. src/app/layout/header/)'
tools: ['search/codebase', search]
---

# Code Review: $input

## Generic Review Workflow

1. **Correctness** — Are there logic errors, edge cases, or potential regressions?
2. **Maintainability** — Are functions ≤ 14 lines? Single responsibility? No magic numbers?
3. **Styling / UI** — Is BEM consistent? CSS Custom Properties used? No hardcoded values?
4. **Tests** — Does the spec cover the behavior change and edge cases?
5. **Output** — Return top findings ordered by severity. For each: problem, risk, concrete fix.

Then check `$input` against these dev2k-page specific rules:

## Project Rules: Architecture And State

- Architecture context from [copilot-project.prompt.md](./copilot-project.prompt.md) respected?
- Signals-only approach maintained, no additional state layers introduced?
- Scroll and routing decisions of the project followed?

## Project Rules: i18n, Styling, Tests

- i18n rules from [i18n-copy.instructions.md](../instructions/i18n-copy.instructions.md) followed?
- SCSS/BEM rules from [scss-bem-responsive.instructions.md](../instructions/scss-bem-responsive.instructions.md) followed?
- Vitest rules from [testing-vitest.instructions.md](../instructions/testing-vitest.instructions.md) followed?

## Output

- Return findings ordered by severity.
- For each finding: problem, risk, concrete fix.
- If no findings: confirm that clearly and add at most one optional improvement note.

## If `$input` is empty

Ask which file or folder should be reviewed.
