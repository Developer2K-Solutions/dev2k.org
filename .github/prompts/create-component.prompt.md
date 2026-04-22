---
description: 'Use when: creating a new Angular component, adding a feature section, adding a layout or shared component, implementing a new UI element'
agent: 'agent'
argument-hint: 'ComponentName (e.g. HeaderComponent, ProjectCard, ContactForm)'
tools:
  [
    'search/codebase',
    'edit/editFiles',
    'execute/runInTerminal',
    'execute/getTerminalOutput',
    search,
  ]
---

# Create Component: $input

## Phase 1: Understand Context

Before writing code, read the relevant standards:

1. Read [copilot-project.prompt.md](./copilot-project.prompt.md) — project structure and available services
2. Read [i18n-copy.instructions.md](../instructions/i18n-copy.instructions.md) — i18n rules and key handling
3. Read [scss-bem-responsive.instructions.md](../instructions/scss-bem-responsive.instructions.md) — BEM, tokens, responsiveness
4. Read [testing-vitest.instructions.md](../instructions/testing-vitest.instructions.md) — Vitest and AAA rules

Determine:

- Where does the component belong? (`layout/`, `features/`, `shared/`)
- Which existing services are needed? (ThemeService, NavStateService, ScrollService, SeoService, TranslationService)
- What inputs and outputs does the component require?

## Phase 2: Spec First (TDD — Red Phase)

Create the **spec file first** — before the component exists.

File: `src/app/[path]/[name].component.spec.ts`

```typescript
// Follow AAA pattern (Arrange / Act / Assert)
// Use: vi.spyOn(), TestBed.configureTestingModule(), provideExperimentalZonelessChangeDetection()
// afterEach: TestBed.resetTestingModule()
// Test: rendering, inputs, outputs, service integration
```

Run the tests — they should be **red**:

```bash
npx ng test --watch=false --include="**/$input.spec.ts"
```

## Phase 3: Implementation

Create the component following these standards:

```typescript
// ✅ Standalone component
// ✅ inject() instead of constructor DI
// ✅ signal() / computed() for state
// ✅ input() / output() API (no @Input/@Output decorators)
// ✅ ChangeDetectionStrategy.OnPush
// ✅ JSDoc @fileoverview header
// ✅ BEM in SCSS (no hardcoded values, CSS custom properties only)
// ✅ Functions ≤ 14 lines
```

If i18n is needed: use the `translate` pipe from `TranslationService`.
If theme-awareness is needed: read `ThemeService.activeTheme` as a signal.

## Phase 4: Verify

1. Run the component tests — they should be **green**:
   ```bash
   npx ng test --watch=false --include="**/$input.spec.ts"
   ```
2. Full suite still green?
   ```bash
   npx ng test --watch=false
   ```
3. TypeScript errors? `npx tsc --noEmit`
4. Definition of Done (from `copilot-project.prompt.md`):
   - [ ] Strict mode, no `any`
   - [ ] All functions ≤ 14 lines
   - [ ] Spec exists with meaningful tests
   - [ ] JSDoc header present
   - [ ] BEM in SCSS correct

## If `$input` is empty

Ask:

1. What is the component name?
2. Where should it live? (`layout/`, `features/[section]/`, `shared/`)
3. Which services does it need?
4. What inputs and outputs does it have?
