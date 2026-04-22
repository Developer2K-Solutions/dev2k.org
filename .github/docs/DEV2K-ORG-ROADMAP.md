# dev2k.org — Projekt-Roadmap

> **Ziel:** Professionelle Portfolio-Website als digitale Visitenkarte für Freelance-Akquise.
> **Stack:** Angular 21 · SCSS (`@dev2k/scss-library`) · Reactive Forms (`@dev2k/reactive-forms`) · Vercel · GitHub Actions
> **Letztes Update:** 25. März 2026

---

## Projektstruktur im Workspace

```
dev2k.org/                          ← Workspace Root
├── .github/
│   ├── docs/
│   │   ├── ai/                     ← Copilot Workflow, Prompts & Diagnostics Docs
│   │   ├── angular/                ← Angular Signals, TDD Guide
│   │   ├── pwa/                    ← PWA Best Practices, Service Worker, Manifest
│   │   ├── security/               ← COOP und weitere Security-Docs
│   │   ├── styling/                ← CSS-Funktionen, Light/Dark, SCSS-Library-Workflow
│   │   └── DEV2K-ORG-ROADMAP.md    ← diese Datei
│   ├── prompts/angular/            ← Coding Standards (01–07), gelten workspace-weit
│   └── skills/                     ← angular-component, bem-scss, prd-writing Skills
├── dev2k-page/                     ← Angular App (dev2k.org SPA)
├── dev2k_modules/
│   ├── scss-library/               ← @dev2k/scss-library v1.1.0
│   └── reactive-forms/             ← @dev2k/reactive-forms
├── social-media/posts/             ← LinkedIn Build-in-Public Posts
└── another-projects/
    └── Portfolio.dev2k/            ← Referenz-App (portfolio.dev2k.org)
```

> **Hinweis `.github`-Configs:** Die Copilot-Skills und Prompts unter `.github/` gelten automatisch
> für alle Dateien im VS Code Workspace. Kein Kopieren in `dev2k-page/` nötig — aber die
> `applyTo`-Patterns in den `.prompt.md`-Files sollten `dev2k-page/**` abdecken.

---

## Phase 1 — Angular Project Setup ✅

**Ziel:** Saubere, produktionsreife Basis in `dev2k-page/`. Einmalig, dann nie wieder anfassen.

### Schritte

- [x] `ng new dev2k-page --routing=false --style=scss --strict`
- [x] `angular.json` Build-Budgets setzen:
  ```json
  "budgets": [
    { "type": "initial", "maximumWarning": "400kB", "maximumError": "800kB" },
    { "type": "anyComponentStyle", "maximumWarning": "8kB", "maximumError": "16kB" }
  ]
  ```
- [x] Path-Aliases in `tsconfig.json`:
  ```json
  "@core/*": ["src/app/core/*"],
  "@shared/*": ["src/app/shared/*"],
  "@features/*": ["src/app/features/*"],
  "@scss-lib": ["../dev2k_modules/scss-library/_index.scss"]
  ```
- [x] `@dev2k/scss-library` via `github:` Protokoll + `npm link` für lokale Entwicklung
- [x] `stylePreprocessorOptions.includePaths` in `angular.json` → `@use 'scss-library'` Kurzform
- [x] Folderstruktur angelegt: `core/`, `features/`, `layout/`, `shared/`
- [x] PWA-Setup: `@angular/pwa`, `manifest-dark.webmanifest`, `manifest-light.webmanifest`
- [x] i18n: Custom `TranslationService` (Signal-basiert) + `public/i18n/de.json` + `en.json` — kein ngx-translate (zu schwer, Signals-inkompatibel)
- [x] `vercel.json` angelegt: SPA-Rewrite + Security-Headers

**Deliverable:** `ng serve` läuft, leere App sauber, Themes + i18n bereit. ✅

---

## Phase 2 — Core Infrastructure ✅

**Ziel:** Services, Layout-Shell, Design-Tokens. Grundlage für alle Features.

### Services (`src/app/core/services/`) ✅

| Service              | Funktion                                                                       | Status |
| -------------------- | ------------------------------------------------------------------------------ | ------ |
| `ThemeService`       | `data-theme="light/dark"` auf `<html>`, Signal-basiert, localStorage           | ✅     |
| `SeoService`         | Meta-Tags + OG-Tags pro Route/Section                                          | ✅     |
| `ScrollService`      | `scrollToFragment(id)` smooth, `triggerPageFlash()`                            | ✅     |
| `NavStateService`    | Mobile-Menü open/close Signal                                                  | ✅     |
| `TranslationService` | Custom Signal-basierter i18n-Wrapper (kein ngx-translate), `isLoaded()` Signal | ✅     |

### Layout-Komponenten (`src/app/layout/`) ✅

- [x] `HeaderComponent` — sticky, Logo, Nav-Links (Fragment-Scroll), Theme-Toggle, Hamburger Mobile
- [x] `FooterComponent` — Links, Copyright, Social-Icons
- [x] `ImprintComponent` — `/imprint` Route (BEM)
- [x] `PrivacyComponent` — `/privacy` Route (BEM)
- [x] Routing: `provideRouter(routes)` + `vercel.json` SPA-Rewrite — saubere URLs `/imprint`, `/privacy`

### Design-Tokens (`src/styles.scss`) ✅

- [x] `@use 'scss-library'` als globale Basis
- [x] Shared `:root` — Brand-Palette (primary: `#0a84ff`, secondary: `#30d158`, accent: `#ff453a`)
- [x] `:root, [data-theme='light']` — GitHub Light Oberflächen-Tokens
- [x] `[data-theme='dark']` — GitHub Dark Oberflächen-Tokens

**Deliverable:** Header + Footer + Legal-Pages rendern, Theme-Switch funktioniert, Services per `inject()` nutzbar. Router aktiv. ✅

---

## Phase 3 — Feature Sections (TDD-Workflow)

> **TDD-Ansatz:** Für jede Section zuerst die Spec-Datei schreiben (Red → Green → Refactor).
> `ng test --watch` läuft während der Entwicklung permanent im Hintergrund.
> Jede Komponente: Spec-File **vor** oder **gleichzeitig** mit dem `.ts`-File anlegen.

### TDD-Flow pro Section

```
1. spec.ts schreiben → Test schlägt fehl (RED)
2. Minimal-Implementierung → Test wird grün (GREEN)
3. Code aufräumen ohne Tests zu brechen (REFACTOR)
```

### Sections (Reihenfolge = visuelle Flow der One-Pager-Page)

| #   | Section              | Besonderheit                                               | TDD-Fokus                                          |
| --- | -------------------- | ---------------------------------------------------------- | -------------------------------------------------- |
| 1   | **HeroSection**      | Name + Claim + CTA „Projekt anfragen" — erster Eindruck    | `scrollToSection()` wird gecallt, CTA-Text korrekt |
| 2   | **AboutSection**     | Kurzvorstellung, Standort, Verfügbarkeit-Badge             | i18n-Keys vorhanden, Portrait-Alt-Text             |
| 3   | **ServicesSection**  | Cards: Angular Dev, TypeScript, Consulting, CI/CD          | Anzahl Cards korrekt, Card-Content gerendert       |
| 4   | **TechStackSection** | Icon-Grid: Angular, TS, SCSS, Firebase, Git, Linux, Docker | Alle Icons gerendert, keine broken links           |
| 5   | **ProjectsSection**  | Projekt-Karten (siehe unten)                               | Karten-Anzahl, Links vorhanden                     |
| 6   | **ContactSection**   | Reactive Form + direkte Kontaktdaten                       | Formular-Validierung, Submit-Handler               |

### Projekt-Karten (ProjectsSection)

| Karte                  | Beschreibung                                                                          | Link                                 |
| ---------------------- | ------------------------------------------------------------------------------------- | ------------------------------------ |
| **dev2k.org**          | Diese Website — Angular SPA, scss-library, TDD                                        | github.com/KosMaster87               |
| **Portfolio.dev2k**    | Angular 21 PWA, i18n, Dark/Light, Firebase                                            | portfolio.dev2k.org                  |
| **KI Coding Mastery**  | 30-Tage Build-in-Public: Link-Shortener mit Node.js + Claude Code (mitmario.dev Kurs) | mitmario.dev/kurse/ai-coding-mastery |
| **Developer Akademie** | Kurs-Projekt / Learning Journey — TypeScript, Angular, moderne Webentwicklung         | developerakademie.de                 |

> **Social-Media Content:** Unter `social-media/posts/` (Tag-00 bis Tag-05) sind LinkedIn-Posts
> aus dem KI Coding Mastery Kurs dokumentiert. Diese Inhalte können für die Projekt-Karte
> als Beschreibungstext genutzt werden.

---

## Phase 4 — Styling & Design System

**Ziel:** Visuell starke, konsistente, responsive UI.

- `@dev2k/scss-library` als Basis (Mixins: `tablet`, `desktop`, `flex-center`, `flex-between`)
- BEM strikt nach `.github/prompts/angular/04-styling-bem.md`
- CSS Custom Properties only — keine hardcoded Werte
- **Animationen:** CSS fade-in on scroll via `@defer` + `IntersectionObserver`
- **Mobile-first:** alle Sections zuerst für 375px, dann `tablet`, dann `desktop`
- Dark/Light Theme: Farben via Custom Properties, toggle per `ThemeService`
- Schriftarten: Entscheidung + `@font-face` in `_typography.scss`

---

## Phase 5 — Inhalte & SEO

- Texte für alle Sections (DE Primärsprache, EN-Toggle optional via i18n)
- CV-Daten aus `social-media/CV Konstantin Aksenov.odt` extrahieren
- `SeoService.updateMetadata()` für jede Section (Title, Description, OG-Image, OG-URL)
- `sitemap.xml` + `robots.txt` in `public/`
- Favicon, Apple-Touch-Icon, OG-Image (1200×630px)
- LinkedIn-Post für Launch vorbereiten (Template: `social-media/posts/_template.md`)

---

## Phase 6 — CI/CD & Deployment

### Vercel (Option A — empfohlen)

```json
// vercel.json
{
  "rewrites": [{ "source": "/(.*)", "destination": "/index.html" }],
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        { "key": "X-Content-Type-Options", "value": "nosniff" },
        { "key": "X-Frame-Options", "value": "DENY" },
        { "key": "Referrer-Policy", "value": "strict-origin-when-cross-origin" }
      ]
    }
  ]
}
```

### GitHub Actions Pipeline

```
Pipeline: main branch push
  ├── Lint (ESLint + Prettier check)
  ├── Test (ng test --no-watch --code-coverage --browsers=ChromeHeadless)
  ├── Build (ng build --configuration production)
  └── Deploy → Vercel (via vercel-action)
```

Datei: `.github/workflows/ci-cd.yml`

### Custom Domain

- `dev2k.org` → Vercel DNS (A-Record + CNAME)
- HTTPS automatisch via Vercel / Let's Encrypt
- `www.dev2k.org` → Redirect auf `dev2k.org`

---

## Projektstatus

| Phase | Beschreibung                            | Status                  |
| ----- | --------------------------------------- | ----------------------- |
| 1     | Angular Project Setup                   | ✅ Fertig               |
| 2     | Core Infrastructure (Services + Layout) | ✅ Fertig — 64/64 Tests |
| 3     | Feature Sections (TDD)                  | ⬜ Offen                |
| 4     | Styling & Design System                 | ⬜ Offen                |
| 5     | Inhalte & SEO                           | ⬜ Offen                |
| 6     | CI/CD & Deployment                      | ⬜ Offen                |

---

## Entwickler

**Konstantin Aksenov** — Freiberuflicher Software Developer · Angular / TypeScript / SCSS
GitHub: [KosMaster87](https://github.com/KosMaster87) · Mail: Konstantin.Aksenov@dev2k.org · Web: dev2k.org
