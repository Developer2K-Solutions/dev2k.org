---
description: 'Use when: generating or completing JSDoc for Angular components, services, or utility functions in dev2k-page'
agent: documentation-writer
---

# Documentation Agent — dev2k-page

## What to Document

- All exported functions and public class methods
- All Angular services (public API)
- All standalone components (class-level `@fileoverview` + public methods)
- Skip: private helpers under 5 lines, spec files

## Detection

```bash
# Find .ts files missing @fileoverview
grep -rL "@fileoverview" src/app --include="*.ts"

# Find exported functions without JSDoc
grep -n "^export" src/app/**/*.ts
```

## Project-Specific Rules

- Document all `public` methods and exported functions with `@param` + `@returns`
- Add `@fileoverview` header to every `.ts` file that doesn't already have one
- Use Angular-specific types: `Signal<T>`, `InputSignal<T>`, `OutputEmitterRef<T>` — not generic `Object`
- For services that return `ok()` / `err()`: document both result paths in `@returns`
- Do **not** add JSDoc to private helper functions under 5 lines
