# 🚀 Git & GitHub Troubleshooting Journey

This document captures the issues faced while working with Git & GitHub, along with debugging steps, root causes, and resolutions.

It reflects real-world troubleshooting experience and understanding of Git workflows.

---

# ✅ 1. Incorrect `git pull` Syntax

## ❌ Issue
git pull remote origin

## ❗ Error

fatal: 'remote' does not appear to be a git repository

## 🔍 Root Cause
Incorrect argument order. Git expects:

git pull  

## ✅ Fix

git pull origin main

---

# ✅ 2. Branch Not Found (`master` vs `main`)

## ❌ Issue

git pull origin master

## ❗ Error

fatal: couldn't find remote ref master

## 🔍 Root Cause
- Local branch: `master`
- Remote branch: `main` (GitHub default)

## ✅ Fix

### Check remote branches

git branch -r

### Pull correct branch

git pull origin main

### Rename local branch (recommended)

git branch -m master main
git branch --set-upstream-to=origin/main main

---

# ✅ 3. Push Error: `refspec main does not match any`

## ❌ Issue

git push origin main

## ❗ Error

error: src refspec main does not match any

## 🔍 Root Cause
- No local commit exists
- OR branch does not exist locally

## ✅ Fix

### Create first commit

git add .
git commit -m "initial commit"

### Rename branch

git branch -m master main

### Push

git push -u origin main

---

# ✅ 4. Permission Denied (403 Error)

## ❌ Issue

git push origin main

## ❗ Error

Permission denied to another account

## 🔍 Root Cause
- Logged in with a different GitHub account
- Repository belongs to another account

## ✅ Fix

### Remove stored credentials
- Open **Credential Manager**
- Delete GitHub entries

### Push again

git push origin main

### Login with correct account

---

# ✅ 5. SSH Host Verification

## ❌ Issue

The authenticity of host 'github.com' can't be established

## 🔍 Root Cause
First-time SSH connection — host not trusted yet

## ✅ Fix

yes

👉 Adds GitHub to known hosts

---

# ✅ 6. SSH Setup (if authentication fails)

## 🔹 Generate SSH key

ssh-keygen -t ed25519 -C "your-email"

## 🔹 Start SSH agent

eval "$(ssh-agent -s)"

## 🔹 Add key

ssh-add ~/.ssh/id_ed25519

## 🔹 Copy key

cat ~/.ssh/id_ed25519.pub

## 🔹 Add to GitHub
- Settings → SSH Keys → Add new key

## 🔹 Test connection

ssh -T git@github.com

---

# ✅ 7. Understanding and Using Key Git Commands

## 🔹 Check remote repository

git remote -v

### ✅ Usage
- Shows connected remote URLs (fetch & push)
- Helps verify correct repository linkage

---

## 🔹 Add remote repository

git remote add origin https://github.com/username/repo.git

### ✅ Usage
- Connects local repo to GitHub
- `origin` = default remote name

---

## 🔹 Update remote URL (switch HTTPS → SSH)

git remote set-url origin git@github.com:username/repo.git

### ✅ Usage
- Changes repo authentication method
- Useful for SSH setup (no repeated login)

---

## 🔹 View Git configuration

git config --list

### ✅ Usage
- Displays all Git settings
- Helps debug username/email issues

---

## 🔹 Set global username

git config --global user.name "your-name"

### ✅ Usage
- Sets commit author name globally

---

## 🔹 Set global email

git config --global user.email "your-email"

### ✅ Usage
- Sets email associated with commits

---

## 🔹 Configure pull behavior

git config --global pull.rebase false

### ✅ Usage
- Ensures `git pull` uses merge instead of rebase
- Avoids confusion for beginners

---

# 🎯 Key Learnings

✅ Correct Git syntax is crucial  
✅ Branch mismatch (`main` vs `master`) is common  
✅ GitHub authentication depends on stored credentials  
✅ SSH setup provides a smoother workflow  
✅ Git debugging is an essential DevOps skill  

---

# 🚀 DevOps Takeaway

These issues are not just beginner mistakes — they reflect real-world DevOps scenarios:

- CI/CD pipeline failures  
- Authentication and access control issues  
- Incorrect configurations  
- Environment mismatches  

👉 Solving these builds strong debugging and problem-solving skills.

---

# ✅ Final Workflow
