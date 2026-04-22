---
description: 'Use when: writing unit tests with Vitest, creating a missing spec file, expanding test coverage, TDD red-green-refactor workflow for Angular components or services'
agent: 'agent'
argument-hint: 'Component or service name (e.g. HeaderComponent, ThemeService)'
tools: ['search/codebase', 'edit/editFiles', 'execute/runInTerminal', 'execute/getTerminalOutput']
---

# Write Tests: $input

First read the project context:
[copilot-project.prompt.md](./copilot-project.prompt.md)

Then the test rules:
[testing-vitest.instructions.md](../instructions/testing-vitest.instructions.md)

## Step 1: Analyze The Target

Read the code at `$input` and identify:

- What is the **single responsibility** of this unit?
- What are its **inputs and outputs**?
- Which **services** are injected? (→ must be spied on)
- Are there **signals or computed()** that need to be tested?
- Are there `window.*` accesses? (→ polyfills needed, e.g. `matchMedia`)

## Step 2: Plan Test Cases

For each relevant path:

| Category           | Examples                                      |
| ------------------ | --------------------------------------------- |
| **Happy Path**     | Normal call with valid inputs                 |
| **Edge Cases**     | Empty inputs, null/undefined, boundary values |
| **Error Cases**    | Error handling, service call fails            |
| **Signal Updates** | Signal value changes → computed reacts        |

## Step 3: Create The Spec File

File: `$input.spec.ts` (next to the source file)

```typescript
// Stack: Vitest v4.1.0 via @angular/build:unit-test
// Imports: describe, it, expect, vi, beforeEach, afterEach from 'vitest'
// TestBed: provideExperimentalZonelessChangeDetection()
// afterEach: TestBed.resetTestingModule()
// Spies: vi.spyOn() — set up BEFORE TestBed.inject() when service reads state on init
// No Jasmine (jasmine.createSpy, jasmine.objectContaining, etc.)
```

Structure:

```typescript
describe('[ClassName]', () => {
  // Arrange (shared setup)

  describe('[method/function]', () => {
    it('should [expected behavior]', () => {
      // Arrange
      // Act
      // Assert
    });
  });
});
```

## Step 4: Run The Tests

```bash
npx ng test --watch=false --include="**/$input.spec.ts"
```

- All new tests **green**?
- Full suite still green? `npx ng test --watch=false`
- If red: analyze and fix, do not skip

## If `$input` is empty

Ask what should be tested — component or service?
