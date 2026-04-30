---
name: package-guardrails
description: Enforce package-scoped development guardrails, documentation reading gates, and issue handoff workflows for the Portfolio Lab monorepo. Use when Codex is asked to implement, review, fix bugs, add features, create cross-package requests, or resolve handoff issues inside packages/* and must stay within a single owner package.
---

# Package Guardrails

Require explicit ownership before doing any work.

- Require `owner_package` in the task context before planning edits or running package-specific checks.
- Default `sender_package` to `owner_package` when the task does not name a separate sender.
- Refuse to guess ownership from cwd, touched files, or issue paths. Pause and ask when ownership is missing.

Read the correct documentation before coding.

- Read `<owner_package>/README.deep.md` before changing the owner package.
- Read another package's `README.md` when depending on it.
- Avoid reading another package's `README.deep.md` unless the user explicitly transfers ownership of that package.

Protect write boundaries.

- Edit only files inside `owner_package` by default.
- Treat every other `packages/*` directory as read-only.
- Treat every path outside `packages/*` as read-only unless the user explicitly approves the change.
- Stop and ask before changing a second package, root config, app code, or shared tooling.

Follow the issue handoff workflow when another package blocks progress.

- Create an issue in the target package instead of editing that package directly.
- Create the matching `.sent.md` file in the sender package at the same time.
- After sender-side validation succeeds, rename the tracking file to `.resolved.sent.md` to mark that the target package resolution has been verified.
- Check the owner package's `P0` issues before starting normal development work.
- Move a resolved issue into `issues-resolved/` and create the matching `.log.md`.
- Ask for user approval before refusing a `P0` or `P1` issue, then create the matching `.reason.md`.
- Reopen with `.r<n>.md` only after a resolved issue exists and the `.sent.md` validation steps fail.

Use the validation scripts instead of manually eyeballing paths and file contents.

```bash
node scripts/issue-guard/validate-issue.mjs --target packages/shared-logger --sender packages/shared-ui --kind bugs --file packages/shared-logger/issues/shared-ui/bugs/0-2025-4-19-12-41-33.md
node scripts/issue-guard/validate-resolution.mjs --target packages/shared-logger --file packages/shared-logger/issues-resolved/shared-ui/bugs/0-2025-4-19-12-41-33.md
node scripts/issue-guard/validate-resolution.mjs --target packages/shared-logger --file packages/shared-logger/issues-resolved/shared-ui/bugs/0-2025-4-19-12-41-33.md --rejected
node scripts/issue-guard/validate-reopen.mjs --sender packages/shared-ui --target packages/shared-logger --file packages/shared-ui/sent-issues/shared-logger/bugs/0-2025-4-19-12-41-33.sent.md
node scripts/issue-guard/validate-reopen.mjs --sender packages/shared-ui --target packages/shared-logger --file packages/shared-ui/sent-issues/shared-logger/bugs/0-2025-4-19-12-41-33.r1.md --verification failed
```

Read the reference files only when needed.

- Read [references/role-rules.md](references/role-rules.md) to enforce owner, caller, and refusal behavior.
- Read [references/path-conventions.md](references/path-conventions.md) to format filenames, directories, and markdown templates.
- Read [references/issue-workflow.md](references/issue-workflow.md) to execute the send, resolve, refuse, verify, and reopen flows in order.
