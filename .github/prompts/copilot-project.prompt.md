---
description: 'Full dev2k.org project context. Use when: starting a new feature, reviewing architecture, planning phases, or needing the complete tech stack overview.'
---

# dev2k.org — Portfolio App: Full Project Context

## Overview

Personal developer portfolio as a **Progressive Web App (PWA)**.
Angular 21.2, no backend, no Firebase. TDD-first with Vitest, SCSS/BEM, i18n (de/en), dark/light theming.

**Repo:** `github.com/KosMaster87/dev2k.org` — branch `main`

---

## Tech Stack

| Layer     | Technology                                     | Why                                      |
| --------- | ---------------------------------------------- | ---------------------------------------- |
| Framework | Angular 21.2 (Standalone, Signals)             | Modern, no NgModules                     |
| Testing   | Vitest v4.1.0 via `@angular/build:unit-test`   | Fast, native ESM, no Karma               |
| Styling   | SCSS + BEM + CSS Custom Properties             | Maintainable, theme-friendly             |
| State     | Angular Signals only                           | No async complexity needed for portfolio |
| i18n      | ngx-translate (de / en)                        | JSON-based, runtime language switch      |
| PWA       | `@angular/pwa` — dual manifests (dark / light) | Installable on desktop + mobile          |
| Hosting   | Vercel (static)                                | Free, fast, zero config                  |
| Backend   | None                                           | Portfolio = static content               |

---

## Architecture Decisions (ADRs)

| Decision         | Choice                                                          | Reason                                                                          |
| ---------------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| State management | Signals only (no NgRx)                                          | No complex async patterns — signals are sufficient                              |
| Navigation       | Scroll-based + Angular Router (standard `PathLocationStrategy`) | Legal pages (`/impressum`, `/datenschutz`); Vercel SPA-Rewrite in `vercel.json` |
| i18n             | ngx-translate                                                   | Runtime switch without reload, JSON files                                       |
| Theming          | `data-theme` attribute on `<html>`                              | CSS custom properties cascade from root                                         |
| Testing          | Vitest, not Karma                                               | esbuild-native, faster, vi.spyOn API                                            |
| SSR              | No SSR                                                          | Static portfolio, Vercel serves pre-built dist                                  |

---

## Project Structure

```
src/
├── app/
│   ├── app.config.ts              # provideRouter(routes), provideHttpClient, i18n
│   ├── app.routes.ts              # Routes: /impressum, /datenschutz, ** → ''
│   ├── app.ts                     # Root layout: header + router-outlet + footer
│   ├── core/
│   │   └── services/              # 5 singleton services (providedIn: 'root')
│   ├── layout/
│   │   ├── header/                # HeaderComponent
│   │   ├── footer/                # FooterComponent
│   │   └── legal/
│   │       ├── imprint/           # ImprintComponent (/impressum)
│   │       └── privacy/           # PrivacyComponent (/datenschutz)
│   ├── features/
│   │   ├── hero/
│   │   ├── about/
│   │   ├── projects/
│   │   ├── skills/
│   │   └── contact/
│   └── shared/
│       └── components/
├── assets/
│   └── i18n/
│       ├── de.json
│       └── en.json
├── styles/                        # Global SCSS (_variables, _mixins, _reset)
└── public/
    ├── manifest-dark.webmanifest
    └── manifest-light.webmanifest
```

---

## Core Services

All `providedIn: 'root'`, `inject()`, TDD-tested with Vitest. **40/40 tests green** (Phase 3a). Total: **64/64 tests green**.

| Service              | Responsibility                                                   | Key API                                 |
| -------------------- | ---------------------------------------------------------------- | --------------------------------------- |
| `ThemeService`       | Light/dark/system via `<html data-theme>`, localStorage, OS pref | `toggleTheme()`, `activeTheme`          |
| `SeoService`         | Dynamic `<title>` + `<meta>` tags per section                    | `updateMeta(PageMetadata)`              |
| `ScrollService`      | Smooth scroll to section or top                                  | `scrollToFragment(id)`, `scrollToTop()` |
| `NavStateService`    | Mobile hamburger open/close state                                | `toggleMenu()`, `isMenuOpen`            |
| `TranslationService` | Loads `assets/i18n/{lang}.json`, dot-notation key lookup         | `use(lang)`, `translate(key)`           |

---

## Signal Architecture

```
ThemeService.currentTheme  signal<'dark'|'light'|'system'>
                   ↓
ThemeService.activeTheme   computed<'dark'|'light'>      ← components read THIS
                   ↓
  effect() → document.documentElement.setAttribute('data-theme', ...)
           → localStorage.setItem('theme', ...)
```

```
NavStateService._isMenuOpen  signal<boolean>  (private — service writes)
NavStateService.isMenuOpen   computed<boolean> (public — components read)
```

---

## Testing Setup

- **Command all:** `npx ng test --watch=false`
- **Command single:** `npx ng test --watch=false --include="**/theme.service.spec.ts"`
- **JSDOM polyfill** needed for `window.matchMedia` (ThemeService)
- **Spy injection order:** Spy must be set up BEFORE `TestBed.inject()` when service reads state during field initialization

---

## Phase Roadmap

| Phase | Description                                               | Status          |
| ----- | --------------------------------------------------------- | --------------- |
| 1     | Planning + ROADMAP.md                                     | done            |
| 2     | Angular Setup (ng new, PWA, i18n, path aliases)           | done            |
| 3a    | Core Services (5 services, 42 tests, JSDoc)               | done `3fbe4a5`  |
| 3b    | Layout — Header, Footer, Legal components + Routing (TDD) | done `64 tests` |
| 4     | Feature Sections (Hero, About, Projects, Skills, Contact) | pending         |
| 5     | Styling & Design System (SCSS variables, global)          | pending         |
| 6     | Content & SEO (real copy, structured data)                | pending         |
| 7     | CI/CD & Vercel deployment                                 | pending         |

---

## Commit Convention (project)

```
feat(layout): add HeaderComponent with theme and language toggle
fix(seo): correct og:image meta attribute name
test(scroll): add spec for scrollToTop with window.scrollTo spy
refactor(nav-state): rename isOpen to isMenuOpen for clarity
docs(core): add JSDoc to translation service
chore(config): update angular.json build budgets
style(header): fix BEM naming for navigation element
```

---

## Definition of Done

- [ ] TypeScript strict mode, no `any`
- [ ] All functions ≤ 14 lines, one task per function
- [ ] TDD: spec written before implementation
- [ ] All existing tests still pass
- [ ] JSDoc on all public methods
- [ ] BEM naming in all SCSS files, CSS custom properties only
- [ ] Responsive down to 320px (mobile-first)
- [ ] No console errors
