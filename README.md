# GitFlowForge

**Industry-standard Git template** for starting production-ready projects.

GitFlowForge gives you a complete, battle-tested foundation with protected branches, automated code quality & security scanning, and language-agnostic CI — so you can focus on building, not configuring.

---

## Features

- Pre-configured branches: `main`, `staging`, `development`
- Branch protection on `main` and `staging`
- Required pull request reviews (only selected members can merge)
- Automated CI pipeline (code quality, tests, linting)
- Security scanning (SAST, dependency vulnerabilities, secrets)
- Works with **any programming language or framework**
- Clean project structure + best-practice documentation
- Easy to use as a GitHub Template Repository

---

## Branch Strategy

| Branch          | Purpose                          | Protection                  |
|-----------------|----------------------------------|-----------------------------|
| `main`          | Production                       | Fully protected             |
| `staging`       | Pre-production / UAT             | Fully protected             |
| `development`   | Integration branch               | Light protection            |
| `feature/*`     | Developer work branches          | Open                        |

### Recommended Workflow

1. Create a feature branch from `development`
2. Open a Pull Request → `development`
3. After review & CI passes → merge to `development`
4. When ready for testing → PR from `development` → `staging`
5. After staging is approved → PR from `staging` → `main`

Only repository owners / selected members can approve and merge into `main` and `staging`.

---

## Getting Started

### Use as GitHub Template (Recommended)

1. Click the green **"Use this template"** button
2. Create your new repository
3. Clone it and start coding
