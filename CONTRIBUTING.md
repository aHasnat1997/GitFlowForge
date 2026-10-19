# Contributing

## Branches

- Do not commit on `main`, `staging`, or `development`.
- Create `feature/<short-name>` from an up-to-date `development`.
- Use `hotfix/<short-name>` only for production fixes, branched from `main`.

## Commits

Use [Conventional Commits](https://www.conventionalcommits.org/):

```
feat: add invoice export
fix: correct timezone on due dates
chore: bump lockfile
docs: describe staging deploy
```

## Pull requests

- Target `development` for normal work.
- Fill in the pull request template.
- Wait for the required checks: `secrets`, `sast`, `dependencies`, and any language job that applies.
- The repository owner reviews and merges protected branches.

## After you clone a project made from this template

```bash
git fetch origin
git checkout development
git checkout -b feature/your-change
```
