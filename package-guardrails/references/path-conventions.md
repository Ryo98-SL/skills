# Path Conventions

## Directory Layout

Pending issues:

```text
<target_package>/issues/<sender>/{bugs|features}/<priority>-<timestamp>.md
```

Resolved issues:

```text
<target_package>/issues-resolved/<sender>/{bugs|features}/<priority>-<timestamp>.md
<target_package>/issues-resolved/<sender>/{bugs|features}/<priority>-<timestamp>.log.md
<target_package>/issues-resolved/<sender>/{bugs|features}/<priority>-<timestamp>.reason.md
```

Sender-side tracking:

```text
<sender_package>/sent-issues/<target>/{bugs|features}/<priority>-<timestamp>.sent.md
<sender_package>/sent-issues/<target>/{bugs|features}/<priority>-<timestamp>.resolved.sent.md
<sender_package>/sent-issues/<target>/{bugs|features}/<priority>-<timestamp>.r<n>.md
```

Use the real package path for `<target_package>` and `<sender_package>`, such as `packages/shared-logger`, `libs/logger`, or `apps/web`.

## Filename Rules

- Use `0`, `1`, `2`, or `3` as the filename prefix.
- Use a timestamp formatted like `YYYY-M-D-H-m-s`.
- Use `.md` for the issue itself.
- Use `.log.md` for resolution notes.
- Use `.reason.md` for approved refusals.
- Use `.sent.md` for sender-side validation plans before verification.
- Use `.resolved.sent.md` after sender-side validation succeeds and the target package resolution is confirmed.
- Use `.r<n>.md` for sender-side reopen receipts.

## Issue Template

```md
0 Short issue title

## Sender Package
shared-ui

## Summary
Describe the missing feature or bug.

## Impact
Describe what is blocked or degraded.

## Expected Result
Describe the minimum acceptable outcome.
```

## Sent Template

```md
Validation plan for 0-2025-4-19-12-41-33.md

## Related Issue
0-2025-4-19-12-41-33.md

## Validation Steps
1. Open the entry point that depends on the target package.
2. Exercise the changed behavior.

## Required Tests
- Run the unit tests that cover the dependency boundary.

## Pass Criteria
Document the exact observable behavior or passing test state.

## Reopen Conditions
Document when to create a `.r<n>.md` file.
```

After verification succeeds, rename the file to `0-2025-4-19-12-41-33.resolved.sent.md` and keep the validated contents intact as the sender-side receipt.

## Resolution Log Template

```md
Resolution log for 0-2025-4-19-12-41-33.md

## Resolution Summary
Describe how the issue was addressed.

## Key Changes
List the relevant code or behavior changes.

## Follow-up Debugging
Describe how to continue quickly if the fix is incomplete.
```

## Refusal Reason Template

```md
Refusal reason for 0-2025-4-19-12-41-33.md

## Reason
Explain why the owner agent is refusing the issue.

## Current Blockers
List the concrete blockers.

## Needs From User
Describe the approval, scope change, or resource that is needed.

## Fastest Restart Path
Describe the shortest path to resume work later.
```

## Reopen Receipt Template

```md
Reopen receipt for 0-2025-4-19-12-41-33.md

## Previous Issues
- 0-2025-4-19-12-41-33.md

## Failed Validation Cases
- Validation step 2 still fails because the API returns the old shape.

## Observed Behavior
Describe the actual behavior after retesting the resolved issue.

## Retest Notes
Describe what was rerun and why a new receipt is required.
```

For `r2`, list both `0-...md` and `0-...r1.md`. Keep extending that sequence for later rounds.
