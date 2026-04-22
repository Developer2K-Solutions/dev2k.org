---
description: 'Use when: reviewing Angular components, services, or SCSS files in dev2k-page for quality, standards compliance, and project-specific rules'
agent: code-reviewer
---

# Code Review Agent — dev2k-page

## Review Checklist

### TypeScript / Angular

- [ ] All functions ≤ 14 lines, single responsibility
- [ ] No `any` types, explicit return types on all functions
- [ ] `inject()` for DI — no constructor injection
- [ ] `input()` / `output()` API — not `@Input` / `@Output`
- [ ] Signals for state (`signal()`, `computed()`) — no BehaviorSubject
- [ ] Standalone component — no NgModule
- [ ] `export type` for type-only exports
- [ ] JSDoc on all public methods

### SCSS / BEM

- [ ] BEM naming consistent (`block__element--modifier`)
- [ ] CSS Custom Properties — no hardcoded color/size values
- [ ] Mobile-first media queries

### Tests

- [ ] Vitest only — no Jasmine/Karma imports
- [ ] AAA pattern (Arrange / Act / Assert)
- [ ] `afterEach: TestBed.resetTestingModule()`
- [ ] Spec covers behavior change and edge cases

## Project-Specific Constraints

- **State**: Signals only (`signal()`, `computed()`) — no RxJS BehaviorSubject, no NgRx
- **DI**: `inject()` only — no constructor injection
- **Components**: Standalone only — no NgModule
- **Testing**: Vitest only — no Jasmine/Karma imports
- **i18n**: All user-facing strings via `ngx-translate` — no hardcoded text
- **Architecture**: Scroll-based SPA — no Angular Router navigation between sections

## Instruction Files

- [i18n-copy.instructions.md](../instructions/i18n-copy.instructions.md)
- [scss-bem-responsive.instructions.md](../instructions/scss-bem-responsive.instructions.md)
- [testing-vitest.instructions.md](../instructions/testing-vitest.instructions.md)
