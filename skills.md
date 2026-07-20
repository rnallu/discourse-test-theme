---
name: implement-discourse-ui
description: Translate Figma exports, screenshots, PDFs, design specifications, or written UI requirements into maintainable Discourse theme code. Use when an agent must plan, implement, review, or troubleshoot Discourse UI; decide between core behavior, theme SCSS, an internal .gjs component, an existing official theme component, a separate custom theme component, a plugin, or a core extension; inventory reusable Discourse components; or verify a design implementation against current Discourse practices.
---

# Implement Discourse UI

Implement the smallest upgrade-safe change that satisfies the approved design. Preserve native Discourse behavior and accessibility unless the design explicitly changes them.

## Load the relevant references

- Read [figma-to-surface.md](references/figma-to-surface.md) before interpreting screenshots, PDFs, or Figma exports.
- Read [component-discovery.md](references/component-discovery.md) before creating a new visible component or recommending a theme component.
- Read [extension-boundaries.md](references/extension-boundaries.md) before selecting an extension mechanism.
- Read [implementation-and-testing.md](references/implementation-and-testing.md) while changing SCSS, `.gjs`, settings, locales, compatibility metadata, or tests.
- Read [copilot-prompts.md](references/copilot-prompts.md) when guiding a developer through VS Code Copilot or structuring a multi-pass agent workflow.

## Follow this workflow

### 1. Establish the exact slice

1. Inspect `AGENTS.md`, existing theme structure, `about.json`, `settings.yml`, locale files, initializers, tests, and relevant styles before proposing files.
2. Record the Discourse version or branch the site runs. Treat APIs, outlets, component names, and DOM selectors as version-specific.
3. Identify the route, viewport, authentication state, trust level, data state, and interactions represented by every design frame.
4. List missing states: loading, empty, error, long text, permissions, hover, focus, selected, and mobile.
5. Separate visual requirements from behavior changes. Do not infer hidden behavior from a static image.

Do not edit code during this pass. Produce a short design-to-surface map and unresolved questions first.

### 2. Discover before building

For every visible region, search in this order:

1. Core site setting or existing feature.
2. Native core UI and stable CSS custom properties.
3. Existing theme code already in the repository.
4. Maintained official Discourse theme component.
5. Public theme API, transformer, plugin outlet, or documented modifier.
6. Internal theme `.gjs` component inserted through a supported API.
7. Separate custom theme component.
8. Plugin or coordinated core extension.

Inspect the actual candidate source and compatibility before selecting it. Never invent an outlet, transformer, setting, component, or theme component from memory.

### 3. Select the extension boundary

Choose one owner for each requirement. Prefer configuration and composition over replacement.

- Use SCSS and CSS custom properties for presentation-only changes.
- Use an internal `.gjs` component for theme-specific markup or interaction that belongs only to this theme.
- Use an existing theme component when it covers most of the requirement, is maintained, and composes cleanly with the theme.
- Use a separate custom theme component only for an independently reusable or independently deployable feature.
- Use a plugin for server data, permissions, jobs, persistence, new endpoints, or site-wide behavior that cannot safely live in a theme.
- Coordinate a core extension when the capability is broadly useful and Discourse agrees on the contract.

Request explicit approval before installing a third-party component, creating a plugin, patching core, using experimental APIs, or relying on invasive overrides.

### 4. Plan the smallest vertical slice

Define:

- the route and design frame;
- the native surface being adapted;
- the selected extension mechanism and evidence;
- exact files to change;
- reusable tokens and settings;
- states and breakpoints to verify;
- automated and manual tests;
- any question for the Discourse team.

Implement one reviewable surface or behavior at a time. Avoid page-wide rewrites unless the design truly replaces the page and the extension contract supports it.

### 5. Implement in the Discourse style

1. Preserve the repository architecture; do not scaffold a replacement theme.
2. Use modern `.gjs` components, `apiInitializer`, documented APIs, outlets, transformers, modifiers, and settings supported by the target version.
3. Keep `common.scss` as an import entry point when that is the repository convention. Organize rules by tokens/foundation, components, and surfaces.
4. Prefer stable CSS custom properties and shallow selectors. Use the project's token namespace, such as `--hercules-*`, for brand and design values.
5. Use `@use "lib/viewport"` with viewport helpers instead of hand-maintained breakpoint numbers when supported by the target version.
6. Put user-facing strings in locale files and configurable values in `settings.yml`.
7. Preserve keyboard navigation, semantic HTML, focus visibility, reduced motion, contrast, and native responsive behavior.
8. Add `.discourse-compatibility` constraints when the implementation depends on a minimum or maximum Discourse version.

Do not introduce React, MUI, a parallel router, a global reset, hard-coded desktop columns, hidden native controls, broad `!important`, deep DOM selectors, `modifyClass`, template replacement, or direct DOM mutation unless a documented, reviewed exception requires it.

### 6. Verify before claiming completion

Run repository lint, formatting, and theme tests. Add or update system specs for behavior, especially when using `core_features` pages. Manually verify:

- the exact target route and neighboring native routes;
- anonymous and authenticated states when applicable;
- desktop, tablet, and mobile widths;
- loading, empty, error, overflow, and long-content states;
- keyboard-only operation and visible focus;
- light/dark or configured color schemes;
- coexistence with enabled theme components;
- browser console errors and deprecations.

Compare implementation screenshots with the design at matching viewport dimensions. Report intentional differences, assumptions, and unverified states.

## Escalate useful questions to the Discourse team

Ask focused contract questions, not general implementation questions:

- Is the proposed outlet, transformer, modifier, or CSS variable supported for the site's target release channel?
- Is a first-party component or upcoming core feature intended to cover this requirement?
- Should the behavior become a reusable theme component, a plugin, or a core contribution?
- What compatibility range and migration path should be expected?
- Is an experimental API approved for this production project, and who owns breakage during upgrades?

Record their answer beside the extension decision so later agents do not re-litigate it.

## Output expectations

For planning, return a design-to-surface map, component reuse findings, extension decisions, open questions, and a vertical-slice plan.

For implementation, return changed files, the Discourse extension points used, verification performed, remaining design gaps, and upgrade risks. Do not describe a change as complete when it has not been run or visually checked.