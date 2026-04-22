---
description: 'Use when: refactoring oversized components, cleaning up Angular patterns, splitting responsibilities in dev2k-page'
agent: refactoring-assistant
---

# Refactoring Agent — dev2k-page

## Detection

```bash
# Components over 400 LOC
find src/app -name "*.component.ts" -exec wc -l {} \; | awk '$1 > 400 {print $2, ":", $1, "lines"}'

# Services over 100 LOC
find src/app -name "*.service.ts" -exec wc -l {} \; | awk '$1 > 100 {print $2, ":", $1, "lines"}'
```

## Refactoring Strategy

- Extract reusable UI → `shared/`
- Extract section logic → `features/[section]/`
- Extract layout wrappers → `layout/`
- Replace `BehaviorSubject` with `signal()` + `computed()`
- Split large methods into named, single-purpose functions ≤ 14 lines

## Project-Specific Rules

- **Size limit**: Component `.ts` files max 400 LOC, services max 100 LOC
- **No stores**: Skip store-related refactoring checks
- **Extraction targets**: Move reusable UI parts to `shared/`, section logic to `features/`, layout wrappers to `layout/`
- **Signal refactoring**: Replace any remaining `BehaviorSubject` with `signal()` + `computed()`
- **After refactoring**: Run `npx ng test --watch=false` to verify no regressions
