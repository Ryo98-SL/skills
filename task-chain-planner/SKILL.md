---
name: task-chain-planner
description: Decompose a feature, refactor, research effort, or project into an ordered task chain with explicit dependencies, handoff documents, acceptance documents, and completion gates. Use when Codex needs to turn a high-level plan into multiple implementable tasks, especially when each task must be independently reviewable, resumable, and safe to hand to another engineer or agent.
---

# Task Chain Planner

## Purpose

Create a task chain that another engineer or agent can execute without relying on chat history. Each task must have a clear purpose, concrete outputs, a handoff document, and an acceptance document.

Use this skill to turn a feature design into durable project documentation, not to implement the feature itself.

## Progressive Workflow

Follow this short path first. Read `references/templates.md` only when you need the detailed splitting heuristics, document requirements, or markdown templates.

1. Inspect existing project planning conventions before inventing a structure.
2. Identify the smallest sequential chain.
3. Create a chain index.
4. Create one task brief, one handoff document, and one acceptance document for each task.
5. Validate that the chain can be executed from documents alone.

Stop after the documentation is complete unless the user separately asks for implementation.

## 1. Inspect Planning Conventions

Look only as far as needed to understand the repository's planning style.

- Check for `docs/tasks`, specs, ADRs, project READMEs, issue templates, or previous handoff notes.
- Reuse existing naming, status language, validation style, and directory layout when they exist.
- If the repo has no planning convention, use the structure in `references/templates.md`.

## 2. Identify The Smallest Sequential Chain

Split by dependency boundaries, not by file list.

- Each task should produce something a downstream task can trust.
- Avoid parallel tasks unless their inputs and outputs are independent.
- Keep external integrations, UI wiring, acceptance suites, and documentation closure as separate tasks when they have different verification needs.
- Prefer five or fewer tasks for a focused feature; split further only when verification or ownership boundaries demand it.

If a boundary is unclear, read the splitting heuristics in `references/templates.md`.

## 3. Create The Chain Index

The index is the entry point for future implementers.

Include:

- Task order.
- Dependency graph.
- Completion definition for the whole chain.
- Handoff and acceptance document update rules.
- Link from the nearest existing planning index so the task chain is discoverable.

## 4. Define Each Task

For each task, define only what an implementer or reviewer needs to proceed.

- Goal: the durable outcome.
- Preconditions: upstream outputs and documents the implementer must read.
- Scope: what must be built or written.
- Non-goals: what must not be pulled into this task.
- Outputs: code, APIs, fixtures, docs, tests, or generated artifacts.
- Handoff document path.
- Acceptance document path.

Create three documents per task unless the repo already has a better equivalent:

- `NN-topic.md`: task brief.
- `NN-topic-handoff.md`: filled by the implementer after completion.
- `NN-topic-acceptance.md`: used by the reviewer to verify the task.

Use `references/templates.md` when creating those documents.

## 5. Validate The Plan As Documentation

Before finishing, check the chain as if you were a new implementer with no chat history.

- Every task has exactly one handoff document and one acceptance document.
- Downstream tasks depend on handoff documents, not chat context.
- Acceptance documents contain deterministic commands plus human review points.
- The final task closes the loop and names the next possible task chains.

## Quality Bar

The result is good when a new implementer can:

- Read the chain index and know the execution order.
- Start task 1 without asking what to build.
- Start any later task by reading only its brief plus upstream handoff documents.
- Verify each task by following its acceptance document.
- Understand what is intentionally deferred.
