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

## Repository Layout

```text
.
├── README.md
├── README.zh-CN.md
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
npx skills add ./package-guardrails -a codex
```

Install it globally for Codex if you want the skill available across projects:

```bash
npx skills add ./package-guardrails -a codex -g
```

After publishing this repository, it can also be installed from GitHub:

```bash
npx skills add https://github.com/<owner>/<repo>/tree/main/package-guardrails -a codex
```

After installation, Codex can use `package-guardrails` when a task involves implementation, review, bug fixes, feature work, or cross-package handoffs inside a package-based repository.
