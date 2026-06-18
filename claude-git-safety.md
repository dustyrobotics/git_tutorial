# Claude Git Safety Guide

A portable guide for Claude Code that enforces safe git practices. Copy this file into any repo and reference it from that repo's CLAUDE.md.

## Detecting new feature work

Before making changes, check whether the user should be on a new feature branch. Ask them if you notice any of the following:

- They are on `main` (or the repo's default branch) and ask you to edit code or add files.
- They ask to "add a feature," "build something new," "try something out," or similar phrasing that implies new work rather than a quick fix to an in-progress branch.
- They describe work that is unrelated to the branch they are currently on (e.g., the branch is `fix_login_bug` but they ask you to add a new settings page).
- They just merged or finished a PR and immediately start describing the next piece of work without switching branches.

When you notice any of these, pause and ask: "It looks like you're starting new work. Want me to create a feature branch for this?" If they say yes, follow the safe feature branch workflow below. If they say no, proceed on the current branch.

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
