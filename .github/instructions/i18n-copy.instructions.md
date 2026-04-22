---
applyTo: 'src/**/*.{ts,html,json}'
---

# I18n And Copy (dev2k-page)

- This project uses `ngx-translate` with `src/assets/i18n/de.json` and `src/assets/i18n/en.json`.
- Do not introduce a second translation system unless explicitly requested.
- Keep visible copy consistent with portfolio tone: clear, concise, professional, and user-focused.
- For new user-facing text, add or update translation keys in both language files.
- Prefer translation keys over hardcoded literals in templates and component logic.
- Keep key naming stable and feature-scoped to avoid accidental regressions.
- Do not silently rename existing keys that are already used by templates or tests.
