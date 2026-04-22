# dev2k.org Agent Playbook

Use this file as the shared working agreement for Copilot workflows in this workspace.

## Core Principle

Use focused prompts and instructions for repeatable work. Keep changes small and aligned with the current portfolio architecture.

## Recommended Flow

1. Load `/copilot-project` first.
2. Identify impacted layers: services, components, styles, i18n, tests.
3. Pick the narrowest matching prompt.
4. Implement in small slices.
5. Run or update tests before closing.

## When To Work Directly

- Single-file fixes.
- Small copy or translation updates.
- Minor styling adjustments.
- Typos and comment cleanup.

## When To Use Prompt Workflows

- Changes touching more than three files.
- Service and component refactors.
- Large layout or responsive behavior updates.
- Test coverage work.
- Pre-commit quality checks.

## High-Risk Areas

- `src/app/core/services/`
- `src/app/layout/`
- `src/app/features/`
- `src/assets/i18n/`
- `public/manifest-dark.webmanifest`
- `public/manifest-light.webmanifest`

For these areas, prefer review-first and include test checks.

## Definition Of Done

- Behavior is correct across desktop and mobile.
- Existing architecture rules remain intact.
- i18n keys are valid for `de` and `en`.
- Tests were added or updated where behavior changed.
- No prompt or instruction conflicts with current project decisions.
