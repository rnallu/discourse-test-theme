# Hercules Discourse theme instructions

Use `.github/skills/implement-discourse-ui/SKILL.md` for any task that translates a design, screenshot, PDF, or UI requirement into Discourse theme code, or that decides whether to use core, a theme, a theme component, a plugin, or a core extension.

## Project rules

- Treat the existing theme repository and its architecture as the source of truth. Do not scaffold or replace it.
- Confirm the site's Discourse version or branch before choosing APIs, outlets, transformers, modifiers, components, or selectors.
- Preserve native Discourse behavior, data flow, permissions, responsive behavior, and accessibility unless an approved requirement explicitly changes them.
- Prefer, in order: site settings/core features, native core UI, stable CSS variables and SCSS, existing repository code, maintained official Discourse theme components, public theme APIs/transformers/outlets, internal theme `.gjs`, a separate theme component, a plugin, then a coordinated core extension.
- Search the target source and official Discourse sources before creating a component. Never invent an API, outlet, transformer, setting, or component name.
- Keep Hercules brand and design values behind existing `--hercules-*` tokens. Preserve the current stylesheet organization and import entry points.
- Use modern `.gjs`, `apiInitializer`, supported public APIs, locale strings, theme settings, viewport helpers, and `.discourse-compatibility` metadata where applicable.
- Do not add React, MUI, a parallel router, a global reset, hard-coded page columns, hidden native controls, broad `!important`, deep selectors, deprecated `.hbs` overrides, `modifyClass`, direct DOM mutation, or core patches without an approved and documented exception.
- Treat the Blocks API announced in June 2026 as experimental until the Discourse team confirms a stable production contract for the target version.
- Preserve unrelated local changes. Keep each implementation to one reviewable vertical slice.

## Required working pattern

1. Inspect the repository and attached design inputs.
2. Produce a design-to-surface map and component reuse findings before editing.
3. Record the selected extension boundary and any contract question for the Discourse team.
4. Plan exact files, states, breakpoints, and tests; obtain approval when the choice adds a dependency or changes architecture.
5. Implement the approved slice only.
6. Run repository lint, formatting, and tests; perform matching-viewport visual and accessibility checks.
7. Report changed files, verified results, assumptions, remaining design gaps, and upgrade risks.