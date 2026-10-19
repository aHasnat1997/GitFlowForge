# Day-to-day workflow

```text
feature/*  -->  development  -->  staging  -->  main
                   ^                ^           |
                   |                |           hotfix/*
                   +----------------+-----------+
```

## Developer

```bash
git fetch origin
git checkout development
git pull
git checkout -b feature/add-export
# work, commit
git push -u origin feature/add-export
gh pr create --base development --title "feat: add export" --fill
```

## Owner — promote

```bash
gh pr create --base staging --head development --title "promote: development to staging"
gh pr create --base main --head staging --title "release: staging to main"
```

Merge only after the environment has been checked. Deploys, if you add them later, should trigger on push to `staging` and `main`, not from feature branches.

## Scaling

- One owner today: `CODEOWNERS` is `* @you`.
- Several reviewers later: change `CODEOWNERS` to a team (`* @org/maintainers`) and keep the required review count at 1 or 2.
- The workflows currently run Node, Python, and Laravel jobs, and skip any stack that is not in the repo. Add a job in `.github/workflows/ci.yml` when you adopt another language.
