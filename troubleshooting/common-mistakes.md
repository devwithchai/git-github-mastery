# Troubleshooting: Common Mistakes

Common Git mistakes and how to prevent them.

## Mistake 1: Committing to Wrong Branch

**What Happened:**
```bash
# You're on main, make changes, then commit
git status
# On branch main
git commit -m "Work on feature"
# Oops! This should have been on a feature branch!
```

**Solution:**
```bash
# Create a feature branch from current state
git branch feature/my-work

# Reset main to where it was
git reset --hard origin/main

# Switch to your feature branch
git checkout feature/my-work

# Now your work is on the right branch
```

**Prevention:**
```bash
# Always check which branch you're on
git status
# or
git branch

# Get in the habit of creating branches first
git checkout -b feature/descriptive-name
# THEN make changes
```

---

## Mistake 2: Using `git push -f` on Shared Branch

**What Happened:**
```bash
# You rebase your branch
git rebase main

# Git says: "Your branch is behind"
# You force push without thinking
git push -f origin main

# DISASTER: You've overwritten everyone's work!
```

**Solution:**
```bash
# If this just happened and no one has pulled yet
# Contact team immediately
# Have everyone pull latest

# DO NOT use force push on shared branches
# Only use on your own feature branches
```

**Prevention:**
```bash
# NEVER force push main or develop
# Only safe on personal feature branches
git push -f origin feature/my-work  # OK
git push -f origin main             # NEVER!

# If push is rejected, pull first
git pull origin main
# Resolve conflicts if needed
git push
```

---

## Mistake 3: Accidentally Committing .env or Secrets

**What Happened:**
```bash
echo "DATABASE_PASSWORD=secret123" > .env
echo "API_KEY=abcdef" >> .env

git add .
git commit -m "Setup"
git push

# OH NO! Credentials are now in GitHub!
```

**Immediate Actions:**
1. Rotate all exposed credentials NOW
2. Tell your team
3. Notify your hosting provider

**Solution:**
```bash
# Remove from history
git filter-branch --tree-filter 'rm -f .env' HEAD

# Force push to GitHub
git push -f origin main

# Add to .gitignore
echo ".env" >> .gitignore
git add .gitignore
git commit -m "Add .env to gitignore"
git push
```

**Prevention:**
```bash
# Create .gitignore BEFORE committing secrets
cat > .gitignore << 'EOF'
.env
.env.local
*.pem
secrets/
*.key
EOF

git add .gitignore
git commit -m "Add .gitignore"
# NOW start working, never before

# Use environment variables instead
echo "DATABASE_PASSWORD=${DB_PASSWORD}" # Get from env
```

---

## Mistake 4: Large Files in Git

**What Happened:**
```bash
# You commit a large video file
cp ~/Videos/demo.mp4 .
git add demo.mp4
git commit -m "Add demo"
git push  # Takes forever!

# Now everyone has to download huge repos
```

**Solution:**
```bash
# Option 1: Remove from history
git filter-branch --tree-filter 'rm -f demo.mp4' HEAD
git push -f origin main

# Option 2: Use Git LFS (Large File Storage)
git lfs install
git lfs track "*.mp4"
git add .gitattributes demo.mp4
git commit -m "Add demo video with LFS"
```

**Prevention:**
```bash
# Add to .gitignore
echo "*.mp4" >> .gitignore
echo "*.zip" >> .gitignore
echo "*.tar.gz" >> .gitignore

# For large files, use:
# - Cloud storage (Google Drive, Dropbox)
# - Git LFS (Git Large File Storage)
# - Separate documentation repo
```

---

## Mistake 5: Messy Commit History

**What Happened:**
```bash
echo "feature" > feature.txt
git add . && git commit -m "wip"

echo "fix typo" >> feature.txt
git add . && git commit -m "fix"

echo "forgot this" >> feature.txt
git add . && git commit -m "oops"

echo "actually this too" >> feature.txt
git add . && git commit -m "also"

# History is a mess of incomplete commits
```

**Solution:**
```bash
# Use interactive rebase to clean up
git rebase -i HEAD~4

# In the editor, squash related commits
pick abc123 wip
squash def456 fix
squash ghi789 oops
squash jkl012 also

# Save, edit message
# Result: One clean commit
```

**Prevention:**
```bash
# Before committing, think about logic
# One commit = one feature/fix

# Use "git add <file>" instead of "git add ."
# Commit related changes together

# Write meaningful messages
git commit -m "Add login functionality"
# Not: git commit -m "stuff"
```

---

## Mistake 6: Merge Conflicts You Can't Resolve

**What Happened:**
```bash
git merge feature/new-ui
# CONFLICT (content): Merge conflict in index.html

# File is filled with conflict markers
# You don't know which version to keep
```

**Solution:**
```bash
# Option 1: Abort the merge
git merge --abort

# Option 2: Resolve manually
# Edit the file, remove conflict markers
# Keep the code you want

cat index.html
# Remove lines between <<<<<<< and =======
# Or between ======= and >>>>>>>
# Or keep parts of both

# Mark as resolved
git add index.html
git commit -m "Merge feature/new-ui - resolved conflict"

# Option 3: Take theirs or ours
git checkout --ours index.html  # Keep our version
git checkout --theirs index.html  # Keep their version
```

**Prevention:**
```bash
# Communicate with teammates
# Don't both edit the same files simultaneously

# Pull regularly from main
git pull origin main

# Merge feature branches frequently
# Small merges = fewer conflicts

# Use branches for different areas:
# - Person A: Frontend
# - Person B: Backend
# - Person C: Database
```

---

## Mistake 7: Pushing Incomplete/Broken Code

**What Happened:**
```bash
# You're tired, push untested code
git push

# CI/CD tests fail
# Everyone's blocked waiting for you to fix
# You look bad
```

**Solution:**
```bash
# Revert the broken push
git revert <commit>
git push

# Fix the issue locally
# Test thoroughly

git commit -m "Fix: Actually working version"
git push
```

**Prevention:**
```bash
# ALWAYS test before pushing
python -m pytest     # Run tests
npm run build        # Build project
npm run lint         # Check code style

# Verify manually
# Run the application
# Test the feature you changed

# Only THEN push
```

---

## Mistake 8: Losing Work Because Forgot to Push

**What Happened:**
```bash
# Made commits on local branch
git commit -m "Important feature"

# Computer crashes
# Hard drive dies
# You lose everything

# The commits were only local, never pushed
```

**Solution:**
```bash
# If computer still works
git push origin feature/important-feature

# If data is lost
# Hopefully you have backups
```

**Prevention:**
```bash
# ALWAYS push after committing
git push  # Make it a habit

# Use the rule:
# Commit → Push (not "commit whenever")

# Set up automatic syncing
# Use tools that auto-push

# Always backup important work
```

---

## Mistake 9: Rewriting Public History

**What Happened:**
```bash
# You amend a commit that people already pulled
git commit --amend
git push -f

# Now others have conflicts
# They don't know what happened
```

**Solution:**
```bash
# Tell your team what you did
# They need to:

# 1. Reset their local branch
git fetch origin
git reset --hard origin/main

# 2. Continue working
```

**Prevention:**
```bash
# DON'T rewrite public history
# Only amend if:
# - Not pushed yet
# - Pushing to your personal branch
# - Everyone knows and agrees

# For shared branches:
# Make a NEW commit to fix instead
git revert <bad-commit>
git commit -m "Fix previous issue"
git push
```

---

## Mistake 10: Wrong Branch for PR

**What Happened:**
```bash
# You created a PR from feature → main
# But you should have done feature → develop

# PR shows too many changes
# Includes other people's work
```

**Solution:**
```bash
# If not merged yet:
# 1. Close the PR
# 2. Create new one with correct branches

# To prevent:
git checkout main
git pull

# Create from correct base
git checkout -b feature/my-work develop
# Not from main!
```

**Prevention:**
```bash
# Before creating PR:
# 1. Verify you're on the right branch
git branch

# 2. Check your base branch
git log --oneline -n 1 origin/develop

# 3. GitHub shows you the branches
# Double-check before creating PR
```

---

## Quick Reference: Mistakes & Fixes

| Mistake | Cause | Fix | Prevention |
|---------|-------|-----|------------|
| Committed to wrong branch | Didn't check branch | Create branch from commit, reset original | Always check `git status` |
| Force pushed to main | Tried to solve merge conflict | Have team pull latest | Never force push shared branches |
| Committed secrets | Forgot .gitignore | Filter history, rotate credentials | Create .gitignore first |
| Large files in repo | No LFS setup | Remove or use LFS | Add to .gitignore |
| Messy commits | Too many tiny commits | Rebase and squash | Think before committing |
| Merge conflicts | Parallel edits | Resolve manually | Communicate with team |
| Pushed broken code | Didn't test | Revert, fix, push again | Test before pushing |
| Lost work | Only local, no push | Recover from backup | Always push after commit |
| Rewrote history | Amended then pushed | Tell team to reset | Don't amend public commits |
| Wrong PR branch | Checked out wrong base | Close PR, create new one | Verify branches before PR |

---

## Golden Rules

1. **Always `git status` before acting**
2. **Think before `git push -f`**
3. **Never commit secrets**
4. **Test before pushing**
5. **Communicate with your team**
6. **When in doubt, ask for help**

**You're going to make mistakes. Everyone does. The key is learning from them.** 🚀
