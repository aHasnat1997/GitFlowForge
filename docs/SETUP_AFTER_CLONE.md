# After the repository already exists

You already created `main`, `staging`, and `development`. Add these files on `development` (or `main` if that is your default), then merge through the normal path.

```bash
# on your machine, inside the clone
git checkout development
# copy the GitFlowForge files in (keep your remote)
git add .
git commit -m "chore: add GitFlowForge template"
git push origin development
```

Then:

1. Edit `.github/CODEOWNERS` and replace `@OWNER` with your GitHub login.
2. Push that commit.
3. Open Settings → Actions → General and allow actions to run.
4. Follow [BRANCH_PROTECTION.md](BRANCH_PROTECTION.md) after the first workflow run, so the check names exist.
5. Invite developers as collaborators with the Write role. They push `feature/*` branches only.

Do not give developers the Admin role if you want merge control to stay with you.
