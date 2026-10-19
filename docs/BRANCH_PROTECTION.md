# Branch protection

GitHub does not copy branch protection when you use a template. Apply these rules once on the new repository (Settings → Rules → Rulesets, or classic branch protection).

Replace `OWNER` below with your user or a team such as `org/maintainers`.

## main and staging

- Restrict who can push: only `OWNER` (and still require a pull request, so even the owner goes through a PR)
- Require a pull request before merging
- Required approvals: 1
- Require review from Code Owners
- Dismiss stale approvals when new commits are pushed
- Require approval of the most recent reviewable push
- Require status checks: `secrets`, `sast`, `dependencies`, `hygiene`
- Require branches to be up to date before merging
- Block force pushes
- Block deletions
- Do not allow bypass, including for admins, unless you are handling an incident

## development

- Require a pull request before merging
- Required approvals: 1 (the owner)
- Require the same status checks
- Block force pushes and deletions

## Who can merge

Only people listed in `.github/CODEOWNERS` should be able to approve. Other collaborators get Write so they can push feature branches and open pull requests, but they cannot satisfy the code-owner review.

Suggested permission:

| Person | Repository role |
| --- | --- |
| Owner | Admin |
| Developers | Write |

Write does not override a required code-owner review.

## GitHub CLI

After `gh auth login`, from the repository:

```bash
OWNER="your-github-login"

for BRANCH in main staging development; do
  gh api --method PUT "repos/{owner}/{repo}/branches/${BRANCH}/protection" \
    --input - <<JSON
{
  "required_status_checks": {
    "strict": true,
    "contexts": ["secrets", "sast", "dependencies", "hygiene"]
  },
  "enforce_admins": true,
  "required_pull_request_reviews": {
    "dismiss_stale_reviews": true,
    "require_code_owner_reviews": true,
    "required_approving_review_count": 1,
    "require_last_push_approval": true
  },
  "restrictions": null,
  "allow_force_pushes": false,
  "allow_deletions": false,
  "block_creations": false,
  "required_conversation_resolution": true,
  "lock_branch": false,
  "allow_fork_syncing": false
}
JSON
done
```

If the API rejects `restrictions` on a personal repository, leave it null. Code owners plus "require a pull request" is what stops a developer from merging their own change.

## Checks that must exist first

Protection that names a check will block every merge until that check has run at least once. Push this template, let Actions run on `development`, then turn on the required checks.
