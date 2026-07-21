# Hercules Discourse theme agent instructions

Use `.github/skills/implement-discourse-ui/SKILL.md` whenever a task translates a design, screenshot, PDF, or UI requirement into Discourse theme code, discovers reusable Discourse components, or chooses between theme code, a theme component, a plugin, and a core extension.

## Non-negotiable rules

- Treat the existing repository and its architecture as the source of truth. Never scaffold or replace the theme.
- Confirm the site's Discourse version or branch before choosing APIs, outlets, transformers, modifiers, components, or selectors.
- Preserve native Discourse behavior, permissions, data flow, accessibility, and responsive behavior unless an approved requirement explicitly changes them.
- Prefer core settings and native UI before CSS, existing theme code, maintained official theme components, public APIs, internal `.gjs`, a separate theme component, a plugin, or a core contribution—in that order.
- Verify component and API names in the target source or current official Discourse documentation. Never invent them from memory.
- Preserve the existing stylesheet organization and `--hercules-*` design-token namespace.
- Use modern `.gjs`, `apiInitializer`, documented outlets and transformers, locale strings, theme settings, viewport helpers, and `.discourse-compatibility` where applicable.
- Do not add React, MUI, a parallel router, global resets, hard-coded page columns, hidden native controls, broad `!important`, deep selectors, deprecated `.hbs` overrides, `modifyClass`, direct DOM mutation, or core patches without an approved and documented exception.
- Treat experimental APIs, including the changing Blocks API, as unavailable until the Discourse team approves them for the target version.
- Preserve unrelated local changes. Work on one reviewable vertical slice at a time.
- Never create branches, commit, push, open pull requests, or change Git configuration unless the developer explicitly asks.

## Required working pattern

1. Inspect the repository and attached design inputs.
2. Produce a design-to-surface map and component reuse findings before editing.
3. Select and explain the smallest supported Discourse extension boundary.
4. Plan exact files, states, breakpoints, and tests; pause for approval when the choice adds a dependency or changes architecture.
5. Implement only the approved slice.
6. Run the repository's relevant formatting, lint, tests, and matching-viewport visual checks.
7. Report changed files, actual verification results, assumptions, remaining design gaps, and upgrade risks.
