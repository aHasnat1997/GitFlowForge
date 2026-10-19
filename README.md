# GitFlowForge

Industry-standard Git template for starting production-ready projects.

GitFlowForge is a language-agnostic foundation: protected promotion path (`development` → `staging` → `main`), required reviews, and automated quality and security checks on every pull request.

## Branches

| Branch | Purpose | Who merges |
| --- | --- | --- |
| `main` | Production | Repo owner only (via PR) |
| `staging` | Pre-production / UAT | Repo owner only (via PR) |
| `development` | Integration of finished work | Repo owner (via PR) |
| `feature/<name>` | A developer's work | Anyone with write access opens the PR |

Direct pushes to `main`, `staging`, and `development` are blocked. Developers branch from `development` and open a pull request back into `development`.

## Workflow

1. Update local `development` and branch from it: `git checkout -b feature/short-name origin/development`
2. Commit and push the feature branch.
3. Open a pull request into `development`. CI must pass. The owner reviews and merges.
4. When a release candidate is ready, open a pull request from `development` into `staging`.
5. After staging is accepted, open a pull request from `staging` into `main`.

Hotfixes branch from `main` (`hotfix/<name>`), merge to `main` through a reviewed PR, then merge `main` back into `staging` and `development`.

## What this template includes

- Pull request template and issue templates
- `CODEOWNERS` so the owner is requested on every change
- Language-agnostic CI: secrets, SAST, dependency CVEs, lockfile review
- Optional language jobs that run only when that stack is present
- Conventional commit and branch-name checks
- Docs for branch protection, which GitHub does not copy from a template

## Use this template

1. On GitHub, open this repository and choose **Use this template**.
2. Create `main`, `staging`, and `development` if they are not already there (they are in this repo).
3. Apply the rules in [docs/BRANCH_PROTECTION.md](docs/BRANCH_PROTECTION.md). They cannot travel inside the template; they are repository settings.
4. Replace `@OWNER` in `.github/CODEOWNERS` with your GitHub username.
5. Add your application source. CI detects the stack from files in the repo.

## Stack detection

| If the repo contains | Extra checks |
| --- | --- |
| `package.json` | npm ci, `lint` if present, `test` if present |
| `pyproject.toml` or `requirements.txt` | Ruff if installed, pytest if configured |
| `artisan` (Laravel) | Composer install, Pint if present, `php artisan test` |
| Anything | Gitleaks, Semgrep, Trivy filesystem, dependency review |

Language jobs for Node, Python, and Laravel run on every pull request and skip themselves when that stack is not in the repo. Add another job in `.github/workflows/ci.yml` when you adopt a new language.

## License

MIT. See [LICENSE](LICENSE).
