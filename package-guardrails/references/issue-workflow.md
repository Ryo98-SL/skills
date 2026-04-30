# Issue Workflow

## 1. Start As The Owner Agent

- Read `<owner_package>/README.deep.md`.
- Scan the owner package `P0` issues before starting normal development.
- Stay inside `owner_package` unless the user explicitly broadens the scope.

## 2. Send A Cross-Package Issue

- Read the target package `README.md`.
- Create the target issue file in `<target_package>/issues/<sender>/<kind>/`.
- Create the matching sender-side `.sent.md` file in `<sender_package>/sent-issues/<target>/<kind>/`.
- Run:

```bash
node scripts/issue-guard/validate-issue.mjs --target <target_package> --sender <sender_package> --kind <bugs|features> --file <target_package>/issues/<sender>/<kind>/<priority>-<timestamp>.md
node scripts/issue-guard/validate-reopen.mjs --sender <sender_package> --target <target_package> --file <sender_package>/sent-issues/<target>/<kind>/<priority>-<timestamp>.sent.md
```

## 3. Resolve Or Refuse An Issue

- Move the issue into `issues-resolved/` after completing the work.
- Create the matching `.log.md`.
- Ask the user before refusing `P0` or `P1`.
- Create `.reason.md` after every approved `P0` or `P1` refusal.
- Run:

```bash
node scripts/issue-guard/validate-resolution.mjs --target <target_package> --file <target_package>/issues-resolved/<sender>/<kind>/<priority>-<timestamp>.md
node scripts/issue-guard/validate-resolution.mjs --target <target_package> --file <target_package>/issues-resolved/<sender>/<kind>/<priority>-<timestamp>.md --rejected
```

Use the `--rejected` form only when the owner agent refused the issue.

## 4. Mark Successful Sender-Side Verification

- Check that the resolved issue file exists in the target package.
- Re-run the sender-side validation steps from `.sent.md`.
- When those validation steps pass, rename `<priority>-<timestamp>.sent.md` to `<priority>-<timestamp>.resolved.sent.md`.
- Keep the validated contents intact so the renamed file acts as the sender-side proof that the target package resolution was verified.

## 5. Reopen After Sender-Side Validation Fails

- Check that the resolved issue file exists in the target package.
- Re-run the sender-side validation steps from `.sent.md`.
- Create `.r<n>.md` only when those validation steps still fail.
- Run:

```bash
node scripts/issue-guard/validate-reopen.mjs --sender <sender_package> --target <target_package> --file <sender_package>/sent-issues/<target>/<kind>/<priority>-<timestamp>.r1.md --verification failed
```

Pass `--verification failed` only after actually rerunning the `.sent.md` validation steps and confirming that the result still fails.
