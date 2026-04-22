---
applyTo: 'src/**/*.scss'
---

# SCSS, BEM, And Responsive Rules (dev2k-page)

- Keep BEM naming consistent: `block`, `block__element`, `block--modifier`.
- Prefer existing design tokens and CSS custom properties over one-off hardcoded values.
- Use mobile-first styling and validate behavior on at least mobile, tablet, and desktop breakpoints.
- Keep selectors component-scoped and readable; avoid deep nesting when possible.
- Avoid layout fixes that only work for one viewport size.
- Preserve legal page and header/footer responsiveness when touching shared layout styles.
- For theme-aware styles, rely on existing `data-theme` token strategy rather than per-component color constants.
