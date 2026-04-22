# dev2k.org — Portfolio App

Angular 21.2 portfolio (PWA, no backend, no Firebase, no NgRx).

## Stack Decisions (project-specific, not general Angular rules)

- **State management:** Angular Signals only — `signal()`, `computed()`, `effect()`. No NgRx, no RxJS BehaviorSubject.
- **Navigation:** Scroll-based single page — `ScrollService.scrollToFragment()`. No Angular Router between sections.
- **i18n:** `ngx-translate` with `assets/i18n/de.json` + `en.json`.
- **Theming:** `<html data-theme="dark|light">` via `ThemeService`. Dual PWA manifests.
- **Testing:** Vitest via `@angular/build:unit-test`. Command: `npx ng test --watch=false`.
- **Hosting:** Vercel (static, no SSR).

## Always follow

- Conventional commits: `feat(scope): message` — no emojis, max 72 chars, imperative mood.
- TDD-first: spec before implementation.
- JSDoc on all public methods: `@fileoverview`, `@param`, `@returns`.

## Detailed project context

Use `/copilot-project` prompt for full architecture, services, phases and decisions.
