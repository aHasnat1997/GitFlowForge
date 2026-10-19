# Security policy

## Reporting

Do not open a public issue for a vulnerability. Contact the repository owner privately and include:

- What is affected
- How to reproduce it
- Impact, if you know it

## What CI checks

Every pull request runs:

- Secret scanning (Gitleaks) so tokens and keys are not merged
- Static analysis (Semgrep, default security rules)
- Filesystem and dependency CVE scan (Trivy)
- Dependency review on pull requests (blocks known vulnerable dependencies when GitHub Dependency Review is available)

These checks reduce risk. They do not replace review of business logic.
