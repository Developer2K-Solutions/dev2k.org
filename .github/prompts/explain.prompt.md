---
description: 'Use when: explaining code, understanding an Angular pattern in dev2k-page, learning why something works, explaining a TypeScript type or Signal pattern'
agent: 'ask'
argument-hint: 'Paste code, name a file or function, or describe the concept (e.g. inject() with InjectionToken, scroll-based navigation)'
---

# Explain Code or Concept — dev2k-page

## Explanation Workflow

**Phase 1 — Identify what to explain**

| Input type            | Action                                                   |
| --------------------- | -------------------------------------------------------- |
| File path             | Read the file, identify the main exported symbol(s)      |
| Function / class name | Search the codebase, read definition and usages          |
| Pasted code           | Analyze directly                                         |
| Concept description   | Explain the Angular/TS concept with a short code example |

**Phase 2 — Structure the explanation**

1. **Purpose** — What does this do? One sentence.
2. **How it works** — Step-by-step logic. Reference specific lines if reading code.
3. **Why this way** — Angular/TypeScript design rationale.
4. **Integration** — How does it connect to the rest of the app?
5. **Caveats** — Common mistakes or edge cases.

**Phase 3 — Provide a minimal example** (for concept explanations, not existing code)

## Project Context

When explaining patterns in this project, use these as the baseline:

- [copilot-project.prompt.md](./copilot-project.prompt.md) — architecture, services, tech decisions
- [scss-bem-responsive.instructions.md](../instructions/scss-bem-responsive.instructions.md) — for SCSS/BEM questions
- [testing-vitest.instructions.md](../instructions/testing-vitest.instructions.md) — for Vitest/testing questions

## Project-Specific Concepts to Know

- **Signals-only** state: `signal()`, `computed()`, `effect()` — no RxJS state
- **Scroll navigation**: SPA with scroll-based section switching (no `RouterModule`)
- **`inject()`** for all DI — no constructor injection
- **`input()` / `output()`** API — not `@Input` / `@Output` decorators
- **ngx-translate**: all labels via translation keys, never hardcoded
