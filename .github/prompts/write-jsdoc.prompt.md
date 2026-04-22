---
description: 'Use when: reviewing or writing JSDoc for Angular components, services, or utility functions in dev2k-page'
agent: 'agent'
argument-hint: 'File path or class name (e.g. src/app/services/theme.service.ts, HeaderComponent)'
tools: ['search/codebase', 'edit/editFiles']
---

# Write / Review JSDoc: $input

## JSDoc Workflow

**Step 1 — Analyze the file**
Read `$input` and identify: all exported functions, return patterns used, existing `@typedef` definitions.

**Step 2 — Assess gaps**

| Check                 | Problem                     | Action                |
| --------------------- | --------------------------- | --------------------- |
| No JSDoc              | Exported but undocumented   | Add full JSDoc        |
| `@returns {Object}`   | Too generic                 | Use concrete type     |
| `@param` without type | Type missing                | Add concrete type     |
| Missing `@typedef`    | Same type inline repeatedly | Add `@typedef` at top |

**Step 3 — Apply changes**

- Only exported functions and public methods
- No JSDoc for private helpers under 5 lines
- Do not touch existing correct JSDoc

**Step 4 — Validate**

- All exports documented, no `{Object}` / `{*}` / `{any}`, `@param` names match signature

## Project-Specific Rules

- Use Angular-specific types: `Signal<T>`, `InputSignal<T>`, `OutputEmitterRef<T>`, `WritableSignal<T>`
- For services: document the public API only — skip private helpers under 5 lines
- `@fileoverview` header: include component/service purpose and its place in the app (`layout/`, `features/`, `shared/`, `services/`)
- Do **not** use JSDoc return types like `{Object}` or `{any}` — always use the concrete Angular/TypeScript type
- Do **not** add `@fileoverview` to spec files

## Validation

After changes:

- [ ] All exported functions and public methods have JSDoc
- [ ] No `{Object}`, `{*}`, or `{any}` as types
- [ ] `@param` names match the function signature exactly
- [ ] Run `npx tsc --noEmit` to confirm no type errors introduced
