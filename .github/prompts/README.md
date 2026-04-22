# dev2k-page — Project-Specific Prompts

This folder contains **only project-specific** prompt files for the `dev2k-page` Angular app.

## Contents

| File                                                       | Purpose                                                            |
| ---------------------------------------------------------- | ------------------------------------------------------------------ |
| [`copilot-project.prompt.md`](./copilot-project.prompt.md) | Full project context: stack, architecture, services, phase roadmap |

## What belongs here?

**Here:** Everything that is specific to `dev2k-page` — services, routing decisions, phase roadmap, i18n keys, component structure.

**Not here:** Generic workflows (TDD, Code Review, Quick Fix) live at workspace level under `.github/prompts/`.

**Current state:** `code-review` and `quick-fix` have been extracted to workspace level.
Local files for these two act as project-specific wrappers with additional guardrails.

## Structure Check

The current classification (keep / move / split) is documented here:

- [`PROMPT-STRUCTURE-CHECK.md`](../docs/PROMPT-STRUCTURE-CHECK.md)

## Loading Context

When working on `dev2k-page`, always load the project context first:

```
Use /copilot-project for full architecture context
```
