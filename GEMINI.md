# Gemini Project Instructions (dev2k-page)

Dieses Projekt folgt strikten Architektur- und Designvorgaben, die bereits in der `.github/` Struktur definiert sind.

## Mandatory References
Halte dich bei jeder Aufgabe an folgende Dokumente:
- **General Stack & Architecture:** `.github/copilot-instructions.md` & `.github/prompts/copilot-project.prompt.md`
- **Styling (BEM/SCSS):** `.github/instructions/scss-bem-responsive.instructions.md`
- **Internationalization:** `.github/instructions/i18n-copy.instructions.md`
- **Testing (Vitest/TDD):** `.github/instructions/testing-vitest.instructions.md`

## Workflow Priorities
1. **TDD-First:** Erstelle/aktualisiere immer zuerst den `.spec.ts` Test.
2. **Signals Only:** Nutze ausschließlich Angular Signals für State Management.
3. **Quality:** Halte die "Definition of Done" aus `.github/prompts/copilot-project.prompt.md` ein (z.B. Funktionen ≤ 14 Zeilen, JSDoc Pflicht).
4. **Commits:** Nutze Conventional Commits wie in `.github/prompts/copilot-project.prompt.md` beschrieben.
