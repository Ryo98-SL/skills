---
name: agents-md-template-design
description: Draft or update AGENTS.md files with a six-section project template. Use when the user asks to generate, create, fill, revise, or review an AGENTS.md, or provides project information and wants it shaped into an agent-facing repository guide.
---

# AGENTS.md Template Design

## Core Workflow

Produce an `AGENTS.md` draft with exactly these six top-level sections:

```markdown
# AGENTS.md

## 1. Project Overview
## 2. Commands
## 3. Architecture
## 4. Conventions
## 5. Hard Constraints
## 6. Gotchas
```

Keep the main file around 50 lines when the project allows it. Treat this as a readability target, not as a reason to omit important constraints or gotchas.

## Length And Reference Rules

- Keep `Project Overview` to 2-3 lines: project purpose, technical stack, and deployment environment.
- Do not enforce a hard line limit on `Commands`, `Architecture`, `Conventions`, `Hard Constraints`, or `Gotchas`.
- If any non-overview section would exceed 10 lines, move that section's detailed content to a separate file and place the path in the matching `AGENTS.md` section.
- Prefer paths under `docs/` for extracted guidance, such as `docs/commands.md`, `docs/architecture.md`, `docs/conventions.md`, `docs/hard-constraints.md`, or `docs/gotchas.md`.
- Keep a short summary or pointer in `AGENTS.md` after extracting details. Do not duplicate the same detailed content in both files.

Example pointer:

```markdown
## 6. Gotchas
Detailed gotchas: docs/gotchas.md
```

## Section Guidance

### Project Overview

State what the system is in one sentence. Then list the stack and deployment environment. Do not include background story, company history, or roadmap context.

### Commands

List only the high-frequency commands an agent can run directly: install, start, test, typecheck, and lint. Do not add parameter explanations unless the command is ambiguous without them.

### Architecture

Point to paths instead of restating the architecture. Use this line format:

```markdown
path/ -> purpose
```

End the section with a path to detailed architecture, usually:

```markdown
Detailed architecture: docs/architecture.md
```

### Conventions

List only conventions the team actually follows today. Avoid aspirational rules. Each convention must be self-checkable after code is written.

### Hard Constraints

Every constraint must explain why. Use this format:

```markdown
Forbidden action (reason)
```

The reason should help an agent choose correctly in edge cases.

### Gotchas

Record hidden knowledge that cannot be inferred reliably from the code, especially problems new contributors have already hit. Prefer concrete, lived issues over generic advice.

## Information Gathering Order

If the user has not provided enough information, ask for missing details in this order:

1. Technical stack and deployment environment for `Project Overview`
2. Most-used CLI commands for `Commands`
3. Key directory paths for `Architecture`
4. Naming or formatting conventions for `Conventions`
5. Untouchable areas for `Hard Constraints`, including reasons
6. New-contributor traps or past incidents for `Gotchas`

Ask only for the next missing block when possible. If enough repository context is available, inspect the project and draft with reasonable assumptions instead of blocking on questions.
