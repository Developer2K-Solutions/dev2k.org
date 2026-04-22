---
description: 'Use when: generating a conventional commit message, summarizing staged changes, writing a git commit'
agent: 'ask'
argument-hint: 'Optional: describe what changed, or leave empty to analyze staged files'
---

# Commit Message Generator

## Context

This is the **dev2k.org** Angular 21.2 portfolio project.
Read [project context](copilot-project.prompt.md) for tech stack, scope, and architectural constraints.

## Workflow

### Phase 1: Gather Changes

If `$input` is empty:

- Run `git diff --cached --stat` to list staged files
- Run `git diff --cached` to read the actual diff

If `$input` describes the change:

- Use the description as the primary source of intent
- Still confirm scope from the file paths

### Phase 2: Determine Type and Scope

**Allowed types:**

| Type       | When to use                           |
| ---------- | ------------------------------------- |
| `feat`     | New visible feature or component      |
| `fix`      | Bug fix — wrong behavior corrected    |
| `test`     | Adding or updating tests only         |
| `refactor` | No behavior change, code restructured |
| `docs`     | JSDoc, README, markdown only          |
| `style`    | SCSS, BEM naming, formatting only     |
| `chore`    | Config, dependencies, build tooling   |
| `perf`     | Performance improvement               |
| `ci`       | GitHub Actions, workflow changes      |

**Allowed scopes** (use the most specific applicable one):

```
layout, header, footer, hero, about, projects, skills, contact
nav-state, theme, scroll, seo, i18n, translation
core, config, styles, pwa, animations
```

Use no scope only if the change spans more than 3 unrelated scopes – then omit it.

### Phase 3: Write the Commit Message

Format:

```
<type>(<scope>): <imperative summary in lowercase, max 72 chars>

[optional body: what changed and why — not how]

[optional footer: BREAKING CHANGE or issue reference]
```

**Imperative mood examples:**

- `feat(hero): add animated text cycling with Signal-based counter`
- `fix(scroll): prevent double-trigger on scrollToTop for iOS Safari`
- `test(theme): add spec for applyTheme with document.body spy`
- `refactor(nav-state): rename isOpen to isMenuOpen for clarity`
- `docs(translation): add JSDoc to getTranslation return type`
- `style(header): fix BEM modifier naming for active state`
- `chore(config): update angular.json build memory budget to 2mb`

**Rules:**

- Summary line in lowercase (no uppercase first letter)
- No period at the end of summary
- Body: explain _why_, not _what_ — the diff already shows _what_
- Max one commit message per logical change

### Phase 4: Output

Return the full commit message as a code block so it can be copied directly:

```
<type>(<scope>): <summary>
```

If multiple distinct concerns are staged, list them as separate commit message suggestions with a recommendation for which to squash or split.

## When `$input` is empty and no staged files exist

Ask:

- "What did you change? Describe the intent, or stage your files with `git add` first."
