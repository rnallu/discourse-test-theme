---
name: implement-discourse-ui
description: Translate Figma exports, screenshots, PDFs, design specifications, or written UI requirements into maintainable Discourse theme code. Use when Copilot must plan, implement, review, or troubleshoot Discourse UI; inventory reusable core or official theme components; or decide between theme SCSS, internal .gjs, an existing theme component, a separate custom theme component, a plugin, and a core extension.
---

# Implement Discourse UI

Implement the smallest upgrade-safe change that satisfies the approved design. Preserve native Discourse behavior and accessibility unless the requirement explicitly changes them.

Never commit, push, create branches, open pull requests, or change Git configuration unless the developer explicitly asks.

## 1. Establish the exact slice

Before editing:

1. Read `AGENTS.md` and inspect the existing theme structure, `about.json`, `settings.yml`, locales, initializers, tests, and relevant styles.
2. Record the target Discourse version or branch. Treat APIs, outlets, component names, and selectors as version-specific.
3. Identify the route, viewport, authentication state, trust level, data state, and interactions represented by each design frame.
4. Separate visual requirements from behavior changes.
5. List missing loading, empty, error, long-content, permission, hover, focus, selected, and mobile states.

Do not edit during this pass. Return a concise design-to-surface map and questions that could change architecture.

When direct Figma access is unavailable, use attached PNG, JPG, WebP, or PDF exports. Prefer one full desktop frame, one full mobile frame, close crops for dense regions, interaction notes, and original SVG/image assets. Do not infer hidden behavior from a static image.

## 2. Discover before building

For every visible region, search in this order:

1. Core site setting or existing Discourse feature.
2. Native Discourse UI and stable CSS custom properties.
3. Existing implementation in the theme repository.
4. Maintained official Discourse theme component.
5. Public transformer, modifier, plugin outlet, or documented theme API.
6. Internal theme `.gjs` component inserted through a supported API.
7. Separate custom theme component.
8. Plugin or coordinated core extension.

Inspect actual source and compatibility before recommending a candidate. Never invent an outlet, transformer, setting, component, or theme component from memory.

Search official sources first:

- [Discourse Theme Component category](https://meta.discourse.org/c/customization/theme-component/120)
- [Discourse GitHub organization](https://github.com/discourse)
- [Discourse theme authoring skill](https://github.com/discourse/discourse-theme-skills/tree/main/.claude/skills/discourse-theme-authoring)
- the target Discourse branch and theme API source

For each candidate, report ownership, last meaningful update, supported version, modern `.gjs` or public-API usage, settings, tests, accessibility, responsive behavior, conflicts, requirement coverage, and a reuse/adapt/build recommendation. Mark external discovery incomplete when the work network blocks access.

## 3. Choose the extension boundary

Use the lowest mechanism that fully satisfies the requirement:

| Mechanism | Appropriate use |
| --- | --- |
| Site setting or core feature | Behavior Discourse already supports |
| Theme CSS variables and SCSS | Tokens, typography, spacing, and responsive presentation |
| Maintained official theme component | Reusable client behavior with strong requirement coverage |
| Transformer, modifier, outlet, or public theme API | Supported rendering or client behavior changes |
| Internal theme `.gjs` component | Theme-owned markup and interaction used only by this theme |
| Separate custom theme component | Independently reusable and independently deployable client feature |
| Plugin | Server data, endpoints, permissions, persistence, or background jobs |
| Core contribution | Broadly useful capability agreed with the Discourse team |

An internal `.gjs` file is a programming component; it does not automatically need to become a separately installable Discourse theme component.

Request approval before installing or forking a third-party component, adding a separate theme component, creating a plugin, modifying core, hiding native controls, using undocumented internals, or adopting an experimental API.

Treat the Blocks API described in Discourse's June 2026 project update as experimental until current official documentation and the Discourse team confirm a production contract for the target version.

## 4. Plan the vertical slice

Return:

- route and design frame;
- native surface being adapted;
- chosen extension mechanism and supporting evidence;
- exact files to change;
- reused and new tokens, settings, and locales;
- states and breakpoints to verify;
- automated and manual tests;
- questions for the Discourse team;
- upgrade and compatibility risks.

Implement one surface or behavior at a time. Avoid page-wide rewrites unless the approved design replaces the page and a supported extension contract allows it.

## 5. Implement in the Discourse style

- Preserve the repository's established architecture and entry points.
- Use modern `.gjs`, `apiInitializer`, documented APIs, outlets, transformers, modifiers, and settings supported by the target version.
- Prefer core CSS custom properties before creating Hercules tokens; put Hercules-specific values behind `--hercules-*`.
- Keep selectors shallow and narrowly scoped. Use BEM-like classes for theme-owned markup.
- Use `@use "lib/viewport"` and viewport helpers instead of duplicating breakpoint numbers when supported by the target version.
- Put user-facing text in locale files and administrator-tunable behavior in `settings.yml`.
- Add settings only for real administrator choices, not every design value.
- Preserve semantic HTML, keyboard navigation, visible focus, reduced motion, contrast, RTL-friendly layout, and native responsive behavior.
- Add `.discourse-compatibility` constraints when relying on version-specific APIs.

Do not introduce React, MUI, a parallel router, a global reset, fixed page heights, hard-coded multi-column layouts, hidden native controls, broad `!important`, deep DOM selectors, deprecated `.hbs` overrides, `modifyClass`, template replacement, or direct DOM manipulation without a documented and approved exception.

## 6. Verify before completion

Run the repository's actual commands; never invent package scripts. At minimum:

- format and lint changed SCSS, JS, GJS, YAML, and JSON;
- run existing theme unit and system tests;
- add a system spec for new user-visible behavior when practical;
- test relevant settings on and off;
- test anonymous and authenticated or permission-sensitive states;
- inspect the browser console for errors and deprecations;
- compare implementation and design screenshots at matching viewport sizes;
- verify desktop, tablet, mobile, loading, empty, error, overflow, long-content, keyboard, focus, and configured color-scheme states;
- verify coexistence with enabled theme components.

Do not claim completion when tests or visual checks were not run. Report intentional differences, assumptions, unverified states, and residual upgrade risk.

## 7. Ask the Discourse team precise questions

Ask only when the answer affects the extension contract:

- Is the proposed outlet, transformer, modifier, or CSS variable supported for the target release channel?
- Is a first-party component or planned core feature intended to cover this requirement?
- Should this become a reusable theme component, plugin, or core contribution?
- What compatibility range and migration path should be expected?
- Is an experimental API approved for production, and who owns upgrade breakage?

Record confirmed answers in the implementation plan so later work reuses the decision.

## Starter interaction

Begin design work with:

```text
Use implement-discourse-ui. Analyze the attached desktop and mobile designs for <route>. Do not edit code. Inspect this repository and the target Discourse version, map each region to a native Discourse surface, find reusable core or official components, identify missing states, and propose the smallest vertical-slice plan. Do not commit or push anything.
```

After the plan is approved, implement only the named slice, run relevant checks, and return changed files, actual results, remaining design differences, assumptions, and risks.
