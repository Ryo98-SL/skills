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

### task-chain-planner

`task-chain-planner` turns a feature design, refactor, research effort, or project into an ordered chain of independently executable tasks.

Its main goals are to:

- decompose high-level work by dependency boundaries rather than file lists;
- create task chains that can be resumed by another engineer or agent without chat history;
- require each task to have a clear brief, handoff document, and acceptance document;
- make downstream tasks depend on durable handoff documents instead of implicit context;
- keep completion gates explicit through validation commands and human review points.

The skill is useful when a project is too large or risky to implement as one continuous task. It creates durable planning documentation and stops before implementation unless explicitly asked to continue.

For the full workflow, see [`task-chain-planner/SKILL.md`](task-chain-planner/SKILL.md).

### mainline-grill-me

`mainline-grill-me` interviews the user about a plan or design by resolving the main decision branches first and supplying best-practice defaults for smaller details.

Its main goals are to:

- reach shared understanding before implementation or detailed planning begins;
- focus each question on one major design branch at a time;
- provide a recommended answer for each major question so the user can accept, refine, or challenge it;
- inspect the codebase directly when a question can be answered from local context;
- treat trivial implementation details as accepted defaults unless the user objects;
- keep accepted decisions visible and use them to constrain later questions.

The skill is useful when a plan needs focused pressure-testing without spending time on every minor option. It keeps the conversation on the main line of the design, while still capturing enough decisions for another engineer or agent to act on.

For the full workflow, see [`mainline-grill-me/SKILL.md`](mainline-grill-me/SKILL.md).

### agents-md-template-design

`agents-md-template-design` drafts or updates `AGENTS.md` files with a compact six-section template for agent-facing repository guidance.

Its main goals are to:

- keep `AGENTS.md` readable by standardizing it to six top-level sections;
- make `Project Overview` short and factual, covering purpose, stack, and deployment environment;
- capture only the most-used runnable commands for day-to-day agent work;
- point `Architecture` at real paths instead of restating repository structure in prose;
- record only current, self-checkable conventions instead of aspirational rules;
- preserve hard constraints and hidden gotchas in a form agents can act on reliably;
- split oversized sections into focused files under `docs/` when the main guide would get too long.

The skill is useful when a repository needs a clean `AGENTS.md`, when an existing guide needs to be normalized into a consistent structure, or when project context should be turned into durable instructions another agent can follow without chat history.

For the full workflow, see [`agents-md-template-design/SKILL.md`](agents-md-template-design/SKILL.md).

## Repository Layout

```text
.
├── README.md
├── README.zh-CN.md
├── agents-md-template-design/
│   └── SKILL.md
├── code-style-guardrails/
│   ├── SKILL.md
│   └── references/
│       └── index-md-template.md
├── mainline-grill-me/
│   └── SKILL.md
├── package-guardrails/
│   ├── SKILL.md
│   └── references/
│       ├── issue-workflow.md
│       ├── path-conventions.md
│       └── role-rules.md
└── task-chain-planner/
    ├── SKILL.md
    └── references/
        └── templates.md
```

## Installation

This repository follows the open agent skills ecosystem supported by Vercel Labs' `skills` CLI.

```bash
npx skills add https://github.com/Ryo98-SL/skills/tree/main/package-guardrails -a codex
```

```bash
npx skills add https://github.com/Ryo98-SL/skills/tree/main/code-style-guardrails -a codex
```

```bash
npx skills add https://github.com/Ryo98-SL/skills/tree/main/task-chain-planner -a codex
```

```bash
npx skills add https://github.com/Ryo98-SL/skills/tree/main/mainline-grill-me -a codex
```

```bash
npx skills add https://github.com/Ryo98-SL/skills/tree/main/agents-md-template-design -a codex
```

After installation, Codex can use `package-guardrails` when a task involves implementation, review, bug fixes, feature work, or cross-package handoffs inside a package-based repository. Codex can use `code-style-guardrails` when a task involves TypeScript, TSX, React, module structure, styling consistency, or documentation synchronization in a codebase. Codex can use `task-chain-planner` when a high-level design or project needs to become a resumable sequence of task briefs, handoff documents, and acceptance checks. Codex can use `mainline-grill-me` when a plan or design needs focused questioning around the most important decisions before moving into detailed work. Codex can use `agents-md-template-design` when a repository needs a structured `AGENTS.md` drafted, revised, or normalized into a compact six-section guide for future agents.
