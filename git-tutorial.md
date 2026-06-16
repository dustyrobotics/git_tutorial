# Git Tutorial for Beginners

This guide covers the git commands you need to start collaborating on code with a team. It assumes you have [git installed](#installing-git-on-windows) and a GitHub account.

## First-Time Setup

Tell git who you are. This info appears on your commits.

```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

## Getting Started

If you don't already have a repository you will be working with, create a new repo on GitHub.

Clone the relevant repo to your machine:

```
git clone https://github.com/your-org/your-repo.git
cd your-repo
```

This downloads the full repo and sets up a connection to the remote (called `origin`).

## The Core Workflow

Almost everything you do follows this loop: **pull, branch, work, commit, push, merge**.

### 1. Pull the latest changes

Before starting new work, make sure you have the latest code from the main branch:

```
git checkout main
git pull origin main
```

### 2. Create a branch

Never work directly on `main`. Create a branch for your work using the format `name_date_description`:

```
git checkout -b alice_20260616_add_login_page
```

Including your name helps teammates know whose branch it is at a glance. The date (YYYYMMDD) makes it easy to see how old a branch is. A few more examples:

```
git checkout -b alice_20260610_fix_csv_export_bug
git checkout -b bob_20260614_update_dashboard_layout
```

### 3. Do your work

Edit files, write code, make changes.

### 4. Check what changed

Before committing, see what you've modified:

```
git status
```

This shows which files are modified, staged, or untracked. For a more detailed view of the actual changes:

```
git diff
```

### 5. Stage your changes

Tell git which changes you want to include in your next commit:

```
git add file1.py file2.py
```

To stage everything you've changed:

```
git add -A
```

### 6. Commit

Save a snapshot of your staged changes with a message describing what you did:

```
git commit -m "Add validation to login form"
```

Write commit messages that explain **what** you did and **why**. Your future self will thank you.

If you want to stage all modified (already tracked) files and commit in one step:

```
git commit -am "Fix off-by-one error in pagination"
```

Note: `git commit -am` does not pick up brand new files. You need `git add` for those first.

### 7. Push to GitHub

Upload your branch to the remote so others can see it (and so you have a backup):

```
git push origin alice_20260616_add_login_page
```

The first time you push a new branch, git may suggest using `-u` to set up tracking:

```
git push -u origin alice_20260616_add_login_page
```

After that, `git push` on its own is enough for that branch.

**Repeat steps 3 through 7 often.** Small, frequent commits mean you always have a recent save point to go back to.

### 8. Open a Pull Request (PR)

When your work is ready for review, go to your repo on GitHub and open a Pull Request to merge your branch into `main`.

In the PR:
- Describe what you changed and why
- Assign yourself
- Request a reviewer

### 9. Merge

Once your PR is approved, merge it on GitHub. Most teams use **squash merge**, which collapses all your branch's commits into a single commit on `main`. This keeps the history clean.

After merging, delete the branch on GitHub (it will prompt you), and clean up locally:

```
git checkout main
git pull origin main
git branch -d alice_20260616_add_login_page
```

## Staying Up to Date

If you're working on a branch for more than a day, `main` may move ahead of you. Periodically merge `main` into your branch to keep current:

```
git checkout main
git pull origin main
git checkout alice_20260616_add_login_page
git merge main
```

This reduces the chance of painful merge conflicts later.

## Resolving Merge Conflicts

When two people edit the same part of the same file, git can't automatically combine the changes. This is a merge conflict.

### What it looks like

After running `git merge main`, git will tell you which files have conflicts. Open those files and you'll see markers like this:

```
<<<<<<< HEAD
your version of the code
=======
the other version of the code
>>>>>>> main
```

Everything between `<<<<<<< HEAD` and `=======` is your change. Everything between `=======` and `>>>>>>> main` is the incoming change from main.

### How to fix it

1. Open each conflicted file
2. Decide what the code should actually be -- keep yours, keep theirs, or combine both
3. Delete the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)
4. Stage and commit the resolved files:

```
git add file-with-conflict.py
git commit -m "Resolve merge conflict in file-with-conflict.py"
```

Most code editors (VS Code, PyCharm, etc.) have built-in tools that make this easier by showing the two versions side-by-side and letting you click to accept one or both.

### Tips for avoiding conflicts

- Pull from `main` frequently so you're never too far behind
- Communicate with your team about who's working on which files
- Keep branches short-lived -- merge sooner rather than later

## Useful Commands Reference

| Command | What it does |
|---|---|
| `git status` | Show modified, staged, and untracked files |
| `git log --oneline` | Show commit history, one line per commit |
| `git diff` | Show unstaged changes |
| `git diff --staged` | Show staged changes (what will be committed) |
| `git stash` | Temporarily shelve uncommitted changes |
| `git stash pop` | Bring back stashed changes |
| `git branch` | List local branches |
| `git branch -a` | List all branches including remote |
| `git checkout <branch>` | Switch to an existing branch |
| `git log --oneline --graph` | Show branch and merge history visually |

## Common Mistakes and How to Fix Them

### "I committed to the wrong branch"

If you haven't pushed yet, move the commit to the right branch:

```
git log --oneline -1              # note the commit hash
git reset HEAD~1                  # undo the commit (keeps your changes)
git checkout correct-branch
git add -A
git commit -m "Your message"
```

### "I need to undo my last commit"

If you haven't pushed:

```
git reset HEAD~1                  # undo commit, keep changes as unstaged
```

If you have pushed, don't rewrite history. Instead, make a new commit that reverses the changes:

```
git revert HEAD
```

### "I want to see what a file looked like before"

```
git show HEAD~1:path/to/file.py   # one commit ago
git show abc1234:path/to/file.py  # at a specific commit
```

### "I'm lost and want to start fresh"

If your working directory is in a messy state and you want to discard all uncommitted changes:

```
git checkout .                    # discard all unstaged changes
git clean -fd                     # remove untracked files and directories
```

**Warning:** this permanently deletes uncommitted work. Make sure you really want to lose those changes.

## Glossary

- **repo (repository)** -- the project folder, including its full history of changes
- **commit** -- a saved snapshot of your staged changes
- **branch** -- a parallel line of development; keeps your work separate from others
- **main** -- the primary branch; the source of truth for the project
- **remote** -- the version of the repo hosted on GitHub (called `origin` by default)
- **clone** -- download a remote repo to your machine
- **pull** -- download and apply the latest changes from the remote
- **push** -- upload your local commits to the remote
- **merge** -- combine changes from one branch into another
- **merge conflict** -- when git can't automatically combine changes and needs your help
- **PR (Pull Request)** -- a GitHub feature for proposing and reviewing changes before merging
- **staging (adding)** -- marking specific changes to be included in the next commit
- **stash** -- temporarily hide uncommitted changes so you can switch tasks

## Installing Git on Windows

Git does not come pre-installed on Windows. Mac and Linux typically have it already. To check, open a terminal and run:

```
git --version
```

If you get a version number, you're all set. If not, follow the steps below.

### Git for Windows (recommended)

Download and install [Git for Windows](https://gitforwindows.org/). This gives you:

- **git** itself, usable from any terminal (Command Prompt, PowerShell, or the included Git Bash)
- **Git Bash** -- a lightweight terminal that supports the same commands used in this tutorial and on Mac/Linux
- A credential manager so you don't have to type your GitHub password every time

During installation, the defaults are fine for most people. The one choice worth paying attention to is the default editor -- if you don't use Vim, switch it to VS Code or Notepad.

After installing, open Git Bash (or your preferred terminal) and verify:

```
git --version
```

Then run the [First-Time Setup](#first-time-setup) commands at the top of this guide.

### Authenticating with GitHub

When you push or pull for the first time, git needs to authenticate with GitHub. The easiest approach:

1. Install the [GitHub CLI](https://cli.github.com/)
2. Run `gh auth login` and follow the prompts
3. Choose HTTPS when asked about protocol

This sets up credential storage so git remembers your login. Alternatively, Git for Windows includes Git Credential Manager which will prompt you to log in via your browser the first time you interact with GitHub.
