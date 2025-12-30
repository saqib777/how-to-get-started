
# Git Basic Commands (Practical Guide)

This guide lists the most commonly used Git commands with clear explanations and real usage.
No theory. No deep internals. Just what you actually need.

---

## Check Git Version

Verify Git is installed: git --version


If this works, Git is installed correctly.

---

## Initialize a Repository

Create a Git repository in the current folder: git init


Run this **once per project**.

---

## Check Repository Status

See the current state of your files: git status


Shows:
- modified files
- staged files
- untracked files

Use this command frequently.

---

## Add Files to Staging Area

Add all files: git add .

Add a specific file: git add filename.txt


Files must be added before committing.

---

## Commit Changes

Create a commit with a message: git commit -m "your message here"


Good commit messages are short and meaningful.

Example: git commit -m "add login test"


---

## View Commit History

See commit history: git log

Short version: git log --oneline

---

## Check Current Branch

See which branch you are on: git branch


---

## Create a New Branch

Create and switch to a new branch: git checkout -b feature-login


---

## Switch Branches

Switch to an existing branch: git checkout branch-name


---

## Add Remote Repository

Link local repo to GitHub: git remote add origin https://github.com/username/repo-name.git


Check remote: git remote -v




