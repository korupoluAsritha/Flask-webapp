# 🚀 Git & GitHub Troubleshooting Journey

This document captures all the issues I faced while setting up and using Git & GitHub on my local machine, along with how I debugged and resolved them.  

This helped me understand real-world problems like authentication, branch mismatch, and repository configuration.

---

# ✅ 1. Wrong `git pull` Command

## ❌ Issue
I ran:
git pull remote origin

## ❗ Error

fatal: 'remote' does not appear to be a git repository

## 🔍 Root Cause
- Git expects syntax:

git pull  
- I mistakenly placed arguments in the wrong order

## ✅ Fix

git pull origin master

---

# ✅ 2. Branch Not Found (`master` vs `main`)

## ❌ Issue

git pull origin master

## ❗ Error

fatal: couldn't find remote ref master

## 🔍 Root Cause
- GitHub now uses `main` as default branch
- My local branch was `master`
- Remote branch was `main`

## ✅ Fix

### Check remote branches:

git branch -r

### Pull correct branch:

git pull origin main

### Rename local branch (best practice):

git branch -m master main
git branch --set-upstream-to=origin/main main

---

# ✅ 3. Push Error: `refspec main does not match any`

## ❌ Issue

git push origin main

## ❗ Error

error: src refspec main does not match any

## 🔍 Root Cause
- No commits were made yet
- OR branch `main` did not exist locally

## ✅ Fix

### Make first commit:

git add .
git commit -m "initial commit"

### Rename branch:

git branch -m master main

### Push:

git push -u origin main

---

# ✅ 4. Permission Denied (403 Error)

## ❌ Issue

git push origin main

## ❗ Error

Permission to korupoluAsritha/Flask-webapp.git denied to asritha_snps

## 🔍 Root Cause
- I was logged in with **office GitHub account (`asritha_snps`)**
- Repo belongs to **personal account (`korupoluAsritha`)**

👉 Authentication mismatch

## ✅ Fix

### Clear stored GitHub credentials
- Open **Credential Manager**
- Remove:

github.com
git:https://github.com

### Push again:

git push origin main

### Login with correct account:

korupoluAsritha

---

# ✅ 5. SSH Authentication Prompt

## ❌ Issue

The authenticity of host 'github.com' can't be established
Are you sure you want to continue connecting?

## 🔍 Root Cause
- First-time SSH connection
- Git doesn’t recognize GitHub server yet

## ✅ Fix

yes

👉 This adds GitHub fingerprint to known hosts

---

# ✅ 6. SSH Setup (if push still fails)

## 🔹 Step 1: Generate SSH key

ssh-keygen -t ed25519 -C "your-email@gmail.com"

## 🔹 Step 2: Start SSH agent

eval "$(ssh-agent -s)"

## 🔹 Step 3: Add key

ssh-add ~/.ssh/id_ed25519

## 🔹 Step 4: Copy public key

cat ~/.ssh/id_ed25519.pub

## 🔹 Step 5: Add to GitHub
- Go to → GitHub Settings → SSH Keys
- Paste key

## 🔹 Step 6: Test connection

ssh -T git@github.com

✅ Expected output:

Hi ! You've successfully authenticated.

---

# 🎯 Key Learnings

✅ Git commands must follow exact syntax  
✅ Branch mismatch (`main` vs `master`) is very common  
✅ GitHub authentication depends on stored credentials  
✅ SSH setup avoids repeated login issues  
✅ Debugging errors improves real DevOps skills  

---

# 🚀 DevOps Takeaway

These Git issues are not just beginner mistakes — they reflect real-world DevOps problems:

- CI/CD pipeline failures  
- Authentication issues  
- Permission errors  
- Environment misconfiguration  

👉 Solving these builds the mindset needed for DevOps engineering.

---

# ✅ Final Workflow I Follow Now


git add .
git commit -m "message"
git push

---

# 💡 Future Improvement

- Use SSH instead of HTTPS
- Maintain separate configs for personal & office GitHub
- Keep daily commits for learning consistency

---

# ✅ Conclusion

This troubleshooting experience helped me:
- Understand Git deeply
- Fix real-world errors
- Improve debugging skills

👉 Every error improved my DevOps understanding.