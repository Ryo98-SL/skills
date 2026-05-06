# Module Index Template

Use this template for a module folder `index.md` or for a direct child directory `index.md`.

## Purpose

- What this module or directory is responsible for
- What it does not own

## Structure

```text
module-name/
|- index.md
|- ComponentA.tsx
|- useSomething.ts
|- helpers.ts
`- child-module/
   `- index.md
```

## Key files

- `ComponentA.tsx`: main UI entry or core component
- `useSomething.ts`: state or side-effect logic
- `helpers.ts`: pure helper logic

## Behavior

- Main user-visible flows handled here
- Important internal state or data flow notes
- Integration points with other modules or packages

## Change guide

- Where to extend the module for new behavior
- Which files usually change together
- What to check first when debugging

## Notes

- Known constraints
- Follow-up cleanup ideas
- Links to child directory `index.md` files when useful
