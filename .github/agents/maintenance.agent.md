---
description: 'Use when: running a performance audit, finding unused code, or cleaning up dead imports in dev2k-page'
agent: maintenance-assistant
---

# Maintenance Agent — dev2k-page

## Maintenance Tasks

### Unused Code

```bash
# Unused imports / locals
npx tsc --noEmit --noUnusedLocals --noUnusedParameters
```

### Bundle Size

```bash
npx ng build --stats-json
```

Flag: any lazy chunk > 100 KB, any initial bundle > 500 KB.

### Unused i18n Keys

Compare keys in `src/assets/i18n/de.json` against all `translate` pipe usages and `TranslateService.instant()` calls in `src/app/`.

### Memory Leaks

- Prefer `takeUntilDestroyed()` over manual `unsubscribe()`
- Signals auto-dispose — no cleanup needed for `computed()` / `effect()`

## Project-Specific Scope

- Scan path: `src/app/` (components, services, utils)
- Asset path: `src/assets/i18n/` — check for unused translation keys
- No stores folder — skip store-related checks
- Check for unused i18n keys: keys in `de.json` / `en.json` not referenced in any template or TS file
- Memory leaks: `takeUntilDestroyed()` preferred over manual `unsubscribe()` if RxJS is used
