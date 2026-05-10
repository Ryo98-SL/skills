# Task Chain Planner Reference

Use this reference only after the main workflow needs more detail. Keep the chain durable, concise, and executable without chat history.

## Splitting Heuristics

- Start with the contract before adapters. Example: define a shared API before Web, VSCode, or JetBrains layers.
- Put range/encoding/fixture work in its own task when editors or protocols use different coordinate systems.
- Put adapter contracts before real adapter implementation when multiple platforms are involved.
- Put the final acceptance suite last, after all upstream handoff documents exist.
- Separate documentation closure when it verifies the whole chain rather than one implementation task.
- Prefer five or fewer tasks for a focused feature; split further only when verification or ownership boundaries demand it.

## Document Requirements

Each document should be concise, durable, and readable without chat context.

- Task briefs describe work to be done.
- Handoff documents describe work that was completed.
- Acceptance documents describe how to verify completion.
- Adapt section labels to the repo's language when a local convention exists.

## Task Brief Template

```markdown
# NN Task Name

## Goal

Describe the outcome in one or two sentences.

## Preconditions

- Upstream task handoff documents.
- Existing APIs, docs, or fixtures the implementer must trust.

## Scope

- Required behavior or documentation changes.
- Public interfaces or artifacts this task owns.

## Non-Goals

- Adjacent work explicitly deferred.

## Outputs

- Concrete files, APIs, fixtures, tests, or docs.

## Handoff Document

Update `NN-task-name-handoff.md` when complete.

## Acceptance Document

Reviewer follows `NN-task-name-acceptance.md`.
```

## Handoff Template

```markdown
# NN Task Name Handoff

Status: Not started.

## Completion Summary

Fill after implementation.

## Public Interfaces

List APIs, schemas, commands, paths, fixtures, or contracts changed by this task.

## Test Results

Record commands run and outcomes.

## Known Limits

State intentional limits and deferred work.

## Next Task Entry

Explain exactly what the next task can assume and where to begin.
```

## Acceptance Template

```markdown
# NN Task Name Acceptance

## Validation Commands

- Add deterministic commands that a reviewer can run.

## Manual Checks

- Check public interface shape.
- Check non-goals were not implemented.
- Check documentation and downstream handoff consistency.

## Acceptance Result

Status: Not reviewed.

Record reviewer, date, command results, and manual review conclusion.
```
