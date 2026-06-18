# CLAUDE.md — Git Tutorial Repo

This repo teaches beginners how to use git and GitHub. When helping users here, your primary job is guiding them through the branch/commit/push/PR workflow safely.

## Repo overview

- `git-tutorial.md` — beginner guide to git and GitHub (setup, workflow, merge conflicts)
- `pull-requests-and-code-review.md` — how to create and review PRs
- `practice.md` — simple file for practicing edits and merge conflicts
- `README.md` — repo overview and getting-started steps

## Safe feature branch workflow

When a user wants to make a feature branch and get it on GitHub, follow these steps in order:

1. **Start from an up-to-date main branch.** Always `git fetch origin main`, `git checkout main`, and `git pull origin main` before creating a new branch. Never branch from a stale main.

2. **Create the feature branch.** Use `git checkout -b <branch-name>`. Branch names should be descriptive and use underscores or hyphens (e.g., `neil_add_login_page`).

3. **Make changes.** Edit files as needed.

4. **Stage specific files.** Use `git add <file1> <file2>` — never `git add .` or `git add -A`. This prevents accidentally staging secrets, environment files, or unrelated changes.

5. **Commit with a clear message.** Write a short summary of what changed and why. Follow the style of existing commits in the repo.

6. **Push with upstream tracking.** Use `git push -u origin <branch-name>` on the first push so the branch is tracked on the remote.

7. **Create a PR on GitHub.** Use `gh pr create` or direct the user to the link GitHub prints after the push.

## Things to avoid

- Never force-push (`--force`) unless the user explicitly asks and understands the consequences.
- Never commit `.env` files, credentials, API keys, or other secrets.
- Never push directly to `main`. Always use a feature branch and PR.
- Never use `git add .` — stage files by name.
- Never amend a commit that has already been pushed without the user's explicit request.
- Never run `git reset --hard` or `git clean -f` without confirming with the user first.

## Merge conflicts

If the user hits a merge conflict, walk them through it step by step. Show them the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`), explain what each side represents, and let them decide which changes to keep. After resolving, stage the file and commit.

## Who uses this repo

Beginners learning git for the first time. Keep explanations simple. Avoid jargon or explain it when you must use it. Link to the tutorial files in this repo when relevant.
