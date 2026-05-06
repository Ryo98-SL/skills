---
name: code-style-guardrails
description: Enforce repository-local code structure, frontend styling conventions, and documentation-sync rules. Use when implementing or refactoring TypeScript, TSX, React components, feature folders, or module-level code in projects that benefit from explicit structure and docs guardrails.
---

# Code Style Guardrails

Follow this skill before changing module, feature, component, or package-level code in a repository.

This skill is intentionally project-agnostic. Prefer the target repository's existing conventions over any rule here when the local codebase is more specific.

## Required workflow

1. Identify the target repository area before editing: package, app, module, feature folder, or component folder.
2. Read the closest available project documentation before coding. Prefer `README.deep.md`, then `README.md`, architecture docs, module `index.md`, or equivalent local docs.
3. Inspect nearby files to learn naming, exports, styling, testing, and documentation patterns.
4. If you are developing an existing module, read that module's `index.md` or equivalent local documentation before writing code.
5. If the module does not exist yet, read the nearest parent documentation first and create module documentation as part of the work when the repository uses module docs.
6. After implementation, update the affected documentation that the repository already uses, such as package `README.md`, `README.deep.md`, module `index.md`, docs pages, or generated reference notes.
7. If you add or change a direct child directory inside a documented module, create or update that child directory's documentation too.

Do not treat documentation updates as optional follow-up work. They are part of done.

## Structure rules

- When a single file grows beyond roughly 300 lines, stop and consider splitting it by responsibility.
- For `tsx` files, prefer one-component-one-file. Avoid stacking multiple unrelated components in one file.
- Prefer cohesive module or feature folders over loose piles of unrelated files.
- Keep exported entry points clear and aligned with nearby package or framework conventions.
- When the repository uses module docs, every module folder should have an `index.md` or equivalent document that explains structure and implemented behavior.
- When module docs are used, direct child directories under that module should also have concise docs when they contain meaningful behavior.
- Keep module docs practical: they should help a future contributor find behavior fast, not serve as marketing copy.

When splitting a large file:

- Extract presentational components, hooks, helpers, and types into separate files when they have distinct responsibilities.
- Keep file names aligned with the primary exported symbol or responsibility.
- Prefer small local modules over a single oversized file with mixed concerns.
- Keep tests, fixtures, stories, and examples close to the behavior when that matches the repository's pattern.

## Styling rules

- First identify the repository's styling system: Tailwind utilities, CSS modules, plain CSS, CSS-in-JS, design-system props, component variants, or another established approach.
- Follow the established styling system for the touched area.
- Do not introduce a new styling technology or global stylesheet pattern for a local component change.
- Prefer existing tokens, variants, composition helpers, and shared primitives over one-off visual rules.
- Avoid expanding broad global CSS unless the user explicitly asks for global styling work or the existing architecture requires it.
- Only fall back to inline styles for dynamic values or narrow cases that the local styling system cannot express cleanly.

## Documentation update rules

Before coding, gather context from:

- The nearest package, app, or project `README.md`
- Deeper architecture docs such as `README.deep.md`, `ARCHITECTURE.md`, docs pages, or local contributor notes
- The target module `index.md` or equivalent module docs when developing that module
- The nearest parent module docs when creating a new module

After coding, update:

- User-facing docs, such as `README.md`, when capabilities, setup, commands, or usage change
- Implementation docs, such as `README.deep.md`, architecture docs, or package notes, when structure or integration boundaries change
- Module docs, such as `index.md`, with the current folder structure, responsibilities, key entry points, and changed behavior
- Any direct child directory docs affected by the change

Use the template in [references/index-md-template.md](references/index-md-template.md) when creating or refreshing module docs.

## Minimum module-doc content

Each module `index.md` or equivalent module document should cover:

- Module purpose and ownership
- Current directory structure
- Key files and why they exist
- Main runtime or user-facing behaviors
- Important dependencies, extension points, or integration boundaries
- Notes that help future debugging or onboarding

Keep the document short, concrete, and synchronized with the real folder layout.

## Review checklist

Before finishing, verify all of the following:

- No touched file should remain oversized without a reasoned structure decision
- New or edited `tsx` code follows one-component-one-file
- Styling changes follow the repository's established styling system
- Module docs and any changed direct child directory docs are up to date when the repository uses them
- User-facing and implementation docs reflect the work that shipped when behavior, setup, commands, or structure changed

## Validation command

Use the repository's validation commands before wrapping up. Prefer commands already documented in `README.md`, package scripts, CI config, or local contributor docs.

Examples:

- `pnpm lint`, `npm run lint`, or `yarn lint`
- `pnpm typecheck`, `npm run typecheck`, or equivalent compiler checks
- Focused test commands for the touched package or module
- Repository-specific style guard commands when they exist
