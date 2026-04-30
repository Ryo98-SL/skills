# Role Rules

## Owner Agent

- Treat `owner_package` as the only writable package.
- Read `README.deep.md` in `owner_package` before changing code.
- Scan `owner_package/issues/*/*/0-*.md` before starting normal work.
- Resolve, refuse, or explicitly defer blocking `P0` work before moving on.
- Ask for user approval before refusing any `P0` or `P1` issue.
- Create `.reason.md` after every approved `P0` or `P1` refusal.

## Non-Owner Or Caller Agent

- Treat every non-owned package as read-only.
- Read only the target package `README.md` before depending on it.
- Create an issue when the target package is missing a feature or has a bug that blocks progress.
- Create the matching `.sent.md` file in `sender_package/sent-issues/`.
- After sender-side verification succeeds, rename the tracking file to `.resolved.sent.md`.
- Reopen only after the target package publishes a resolved issue file and the sender-side validation fails.

## Boundary Escalation

- Stop before editing any path outside `owner_package`.
- Stop before editing a second package or workspace directory.
- Stop before changing shared tooling, repo metadata, or another package's issue files unless the user explicitly approves the change.

## Refusal Rules

- Treat `P0` as blocking work that cannot be ignored without user approval.
- Treat `P1` as urgent enough that refusal also requires user approval.
- Allow `P2` and `P3` refusals without approval, but prefer documenting the reason when refusing them.
