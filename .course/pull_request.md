# Phase 3: Submit Your Pull Request

Package your fix into a clean pull request and get automated feedback.

## Step: Create a feature branch

If you haven't already, create a branch for your fix:

```bash
git checkout -b fix/validation-status-code
```

## Step: Stage and commit your changes

Review what you changed:

```bash
git diff
```

Stage only the files you intentionally modified:

```bash
git add <files-you-changed>
```

Write a clear commit message:

```bash
git commit -m "Fix: <brief description of what was wrong and what you changed>"
```

> **Good commit messages** explain *what* changed and *why*:
> - ✅ `Fix: <specific description of the problem and solution>`
> - ❌ `fixed bug`

## Step: Push to your fork

```bash
git push origin fix/validation-status-code
```

## Step: Open the pull request

1. Go to your fork on GitHub
2. Click the **"Compare & pull request"** banner
3. Set the base repository to the original FastAPI repo, branch `main`
4. Fill in the description:

```markdown
## What was broken
<Describe the symptom — what did the user see?>

## What I changed
<Which file, which line, what was wrong and what you fixed>

## How I verified
<Which tests you ran, what the result was>
```

## Step: Review CI results

After opening the PR, automated checks run. While you wait, you can verify locally that everything passes:

```bash
# Run the full test suite
uv run bash scripts/test.sh

# Run lint checks
uv run bash scripts/lint.sh
```

All checks should be green before considering your PR ready for review.

If a check fails:

1. Read the output to understand what failed
2. Fix the issue locally
3. Commit and push again — the PR automatically picks up the new commit

```bash
git add <files-you-changed>
git commit -m "Fix: <what you changed>"
git push origin fix/validation-status-code
```

- [ ] Feature branch created
- [ ] Changes committed with a descriptive message
- [ ] Pushed to your fork
- [ ] Pull request opened against `main`
- [ ] PR description includes what was broken, what changed, how verified
- [ ] `uv run bash scripts/test.sh` passes locally
- [ ] `uv run bash scripts/lint.sh` passes locally

## Footer

- [FastAPI Contributing Guide](https://fastapi.tiangolo.com/contributing/)
- [GitHub Pull Request Guide](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)
