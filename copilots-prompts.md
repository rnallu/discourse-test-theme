# VS Code Copilot workflow and prompt recipes

Use Copilot Agent mode from the Discourse theme repository root so it can read the entire project. Attach design PNGs or PDFs directly to chat by paste, drag-and-drop, or Add Context on current VS Code versions.

Keep one chat per vertical slice. Ask for analysis before edits, review the plan, then start a fresh implementation message with the approved scope.

## Pass 1: map the design

```text
Use the implement-discourse-ui skill. Analyze the attached desktop and mobile designs for <route>. Do not edit code. Inspect this repository and the target Discourse version, map each design region to a native Discourse surface, list missing states, and return a design-to-surface table plus questions that could change architecture.
```

## Pass 2: discover reusable components

```text
Use the implement-discourse-ui skill. For the approved <route> map, inspect core, this theme, official Discourse Meta theme components, and Discourse-owned GitHub sources. Do not code. Return only verified candidates with source links, compatibility evidence, coverage, and a reuse/adapt/build recommendation. Do not invent component or outlet names.
```

If work-network browsing is unavailable, perform repository and installed-component discovery, mark external discovery incomplete, and ask a human to supply candidate URLs or run the official searches.

## Pass 3: propose a vertical slice

```text
Use the implement-discourse-ui skill. Plan the smallest vertical slice for <specific region and behavior>. Use the extension ladder and existing repository architecture. Name exact files, APIs/outlets/transformers verified in source, tokens, settings, states, tests, and risks. Do not edit until I approve the plan.
```

## Pass 4: implement

```text
Implement the approved slice only. Preserve native Discourse behavior and existing unrelated changes. Use modern .gjs and supported theme APIs for our target version. Reuse project tokens and existing structure. Run the relevant format, lint, and tests, then summarize changed files, verification, remaining visual differences, and assumptions.
```

## Pass 5: visual and upgrade review

```text
Review the implementation against the attached design at the same viewport sizes. Also review the diff for Discourse upgrade risk, accessibility regressions, deep selectors, deprecated APIs, duplicated native behavior, and missing system tests. Do not change code. Return findings ordered by severity with file locations and a minimal fix plan.
```

## Helpful operating rules

- Name the exact route and frame; avoid â€œbuild the whole Figma.â€
- Attach only the relevant images and documents to preserve context.
- Ask Copilot to cite source files or official URLs for extension claims.
- Review diffs after each slice and commit human-reviewed checkpoints.
- Do not accept â€œtests should passâ€; require commands and results.
- Start a new chat when context becomes noisy, and restate the approved decision record.

Current official VS Code references:

- [Agent Skills](https://code.visualstudio.com/docs/agent-customization/agent-skills)
- [Custom instructions and AGENTS.md](https://code.visualstudio.com/docs/agent-customization/custom-instructions)
- [VS Code 1.128 release notes](https://code.visualstudio.com/updates/v1_128)