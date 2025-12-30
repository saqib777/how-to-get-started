# Create a GitHub Repository (Step-by-Step)

This guide shows how to create a GitHub repository and push your local project to it from scratch.

No theory. Just steps that work.

---

## Step 1: Create a repository on GitHub

1. Go to https://github.com
2. Click **New repository**
3. Enter a repository name  
   Example: my-first-repo
4. Keep it **Public** (recommended for learning/portfolio)
5. Do NOT check:
- Add README
- Add .gitignore
- Choose a license
6. Click **Create repository**

GitHub will now show you an empty repo page with commands.

---

## Step 2: Initialize Git locally

Open terminal / command prompt inside your project folder.

Run: it init

This initializes Git in your project.

---

## Step 3: Add files and commit

Add all files: git add .

Create your first commit: git commit -m "initial commit"


If you see *nothing to commit*, it means files were already committed.

---

## Step 4: Add GitHub as remote

Copy the HTTPS URL from GitHub (looks like this): https://github.com/your-username/my-first-repo.git 


Add it as origin: git remote add origin https://github.com/your-username/my-first-repo.git


If you see `remote origin already exists`, that is OK. It means it was already added.

---

## Step 5: Push code to GitHub

Check your current branch: git branch

If it shows `master`, run: git push -u origin master

If it shows `main`, run: git push -u origin main


After this, refresh your GitHub repo page. Your files should be visible.

---

## Common Errors & Fixes

### Error: `src refspec main does not match any`

Cause: Your branch is named `master`, not `main`.

Fix: git push -u origin master


---

### Error: `remote origin already exists`

Cause: Remote was already added.

Fix:  
Ignore it and continue.

---

### Error: `nothing to commit, working tree clean`

Cause: No new changes to commit.

Fix:  
Make changes first, then commit again.

---

## Final Check

Run:





