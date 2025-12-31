# Common Git Errors & Fixes (Practical Guide)

This guide covers the most common Git errors beginners face and how to fix them.
Each issue includes the exact command you need. No guesswork.

---

## Error: `nothing to commit, working tree clean`

### What it means
There are no new changes to commit.

### Fix
Make changes to a file first, then run: git add .
git commit -m "your message"


---

## Error: `src refspec main does not match any`

### What it means
You are trying to push a branch that does not exist locally.

### Fix
Check your branch: git branch

If it shows `master`, push using: git push -u origin master


If it shows `main`, push using: git push -u origin main


---

## Error: `remote origin already exists`

### What it means
The remote repository is already added.

### Fix
Check existing remotes: git remote -v


If correct, do nothing and continue.

If wrong, remove and add again:



