# Git Basics — Complete Beginner Guide

Everything you need to start using Git on a real project.
No theory — just commands, what they do, and when to use them.

---

## What is Git?

Git is a version control system. It tracks every change you make
to your code so you can go back to any previous state, collaborate
with others, and maintain a clear history of your project.

---

## First-Time Setup

Run these once on any new machine:

```bash
git config --global user.name "Mohammed Saqib"
git config --global user.email "mohammedsaqibukn@gmail.com"
git config --global core.editor "code --wait"   # VS Code as default editor
```

---

## Starting a Repository

### Option A — Start from scratch

```bash
mkdir my-project
cd my-project
git init
```

### Option B — Clone an existing repo

```bash
git clone https://github.com/saqib777/dsa-journal.git
cd dsa-journal
```

---

## The Three States

Every file in Git is in one of three states:

| State | Meaning |
|-------|---------|
| Modified | Changed but not staged |
| Staged | Marked to go into the next commit |
| Committed | Saved permanently in the repo |

---

## Daily Workflow

```bash
# 1. Check what has changed
git status

# 2. See the actual changes
git diff

# 3. Stage files for commit
git add filename.py          # one file
git add solutions/           # one folder
git add .                    # everything changed

# 4. Commit with a message
git commit -m "add: two_sum solution using hash map O(n)"

# 5. Push to GitHub
git push origin main
```

---

## Viewing History

```bash
git log                    # full history
git log --oneline          # compact one-line view
git log --oneline --graph  # visual branch graph
git show abc1234           # details of a specific commit
```

---

## Undoing Things

```bash
# Unstage a file (keep changes)
git reset HEAD filename.py

# Discard changes in working directory (PERMANENT)
git checkout -- filename.py

# Undo last commit (keep changes staged)
git reset --soft HEAD~1

# Undo last commit (discard changes — PERMANENT)
git reset --hard HEAD~1
```

---

## Commit Message Convention

Good commit messages make history readable:
