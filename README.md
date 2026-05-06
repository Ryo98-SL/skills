# Ryo98's Skills

Personal Codex skills for keeping AI coding agents focused, bounded, and easier to coordinate in larger repositories.

[简体中文](README.zh-CN.md)

## Available Skills

### package-guardrails

`package-guardrails` enforces package-scoped development rules for package-based repositories and monorepos.

Its main goals are to:

- reduce unnecessary context by requiring an explicit `owner_package` before work begins;
- keep each agent inside a single writable package boundary;
- require the right package documentation before coding;
- prevent agents from accidentally modifying packages they do not own;
- use issue handoffs when one package needs another package to add a feature or fix a bug;
- preserve package-level knowledge through `README.md` and `README.deep.md`.

The skill is especially useful when multiple agents are working in parallel. Each agent owns one package, treats other packages as read-only, and creates structured issues instead of directly changing code outside its boundary.

For the full workflow, see [`package-guardrails/SKILL.md`](package-guardrails/SKILL.md).

### code-style-guardrails

`code-style-guardrails` enforces repository-local structure, styling, and documentation-sync rules for implementation and refactoring work.

Its main goals are to:

- make agents identify the target package, app, module, feature folder, or component folder before editing;
- require nearby repository documentation and conventions to be read before coding;
- keep TypeScript and TSX changes split by responsibility instead of growing oversized mixed-concern files;
- make frontend styling follow the target project's existing system, whether that is Tailwind, CSS modules, CSS-in-JS, design-system props, or plain CSS;
- keep user-facing and implementation documentation synchronized when behavior, setup, commands, or structure changes;
- encourage focused validation with the repository's own lint, typecheck, test, or style guard commands.

The skill is useful for general TypeScript and React projects, including monorepos, app folders, package folders, and feature-oriented codebases. It does not assume a specific product, framework, or styling stack; local conventions take priority.

For the full workflow, see [`code-style-guardrails/SKILL.md`](code-style-guardrails/SKILL.md).

## Repository Layout

```text
.
├── README.md
├── README.zh-CN.md
├── code-style-guardrails/
│   ├── SKILL.md
│   └── references/
│       └── index-md-template.md
└── package-guardrails/
    ├── SKILL.md
    └── references/
        ├── issue-workflow.md
        ├── path-conventions.md
        └── role-rules.md
```

## Installation

This repository follows the open agent skills ecosystem supported by Vercel Labs' `skills` CLI.

```bash
npx skills add https://github.com/Ryo98-SL/skills/tree/main/package-guardrails -a codex
```

```bash
npx skills add https://github.com/Ryo98-SL/skills/tree/main/code-style-guardrails -a codex
```

After installation, Codex can use `package-guardrails` when a task involves implementation, review, bug fixes, feature work, or cross-package handoffs inside a package-based repository. Codex can use `code-style-guardrails` when a task involves TypeScript, TSX, React, module structure, styling consistency, or documentation synchronization in a codebase.
