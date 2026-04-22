---
applyTo: 'src/**/*.spec.ts'
---

# Testing With Vitest (dev2k-page)

- Tests run with Vitest via `@angular/build:unit-test`.
- Preferred command: `npx ng test --watch=false`.
- Use `describe`, `it`, `expect`, `beforeEach`, `afterEach`, and `vi` from `vitest`.
- Use Angular `TestBed` for DI-based tests.
- Reset Angular testing state in `afterEach()` when the suite configures test modules.
- Follow Arrange / Act / Assert structure.
- For signal-based logic, test derived state synchronously and keep side-effect assertions explicit.
- For behavior changes, update or add specs before closing the task.
