# Troubleshooting Guide

Common Git problems and their solutions.

## 🔴 Critical Issues (Data Loss Risk)

### "I accidentally deleted my branch!"

**Symptom**: Branch is gone, panic!

**Solution**:
```bash
# Use reflog to find it
git reflog

# Find the commit hash from the deleted branch
# Create branch from that commit
git branch recovered-branch <commit-hash>

# Your work is safe!
git log recovered-branch
```

---

### "I did a hard reset and lost commits!"

**Symptom**: Ran `git reset --hard` and commits disappeared

**Solution**:
```bash
# Use reflog
git reflog

# Find the previous HEAD
# Reset to it
git reset --hard <commit-hash>

# Your commits are back!
```

**Prevention**:
Always think twice before using `--hard`. Use `--soft` or `--mixed` first.

---

### "I committed sensitive data (API keys, passwords)!"

**Symptom**: Accidentally committed passwords or API keys

**Solution**:
```bash
# SHORT TERM: Rotate the credentials immediately!
# Contact your team and hosting provider

# Remove from git history
git filter-branch --tree-filter 'rm -f .env' HEAD

# Force push (only if you own the repo)
git push -f origin main

# Long term: Add to .gitignore
echo ".env" >> .gitignore
git add .gitignore
git commit -m "Add .env to gitignore"
```

**Prevention**:
- Always add sensitive files to `.gitignore` FIRST
- Use environment variables, not committed secrets
- Use tools like `git-secrets` to scan for patterns

---

## 🟡 Major Issues (Can't Push/Pull)

### "fatal: not a git repository"

**Symptom**: Getting this error on any git command

**Solution**:
```bash
# Verify you're in a git repository
ls -la
# You should see `.git` directory

# If not, navigate to the right directory
cd /path/to/repo

# Or initialize a new repo
git init
```

---

### "Permission denied (publickey)"

**Symptom**: Can't push or pull, permission error

**Solution**:
```bash
# Check SSH connection
ssh -T git@github.com
# Should show: Hi username! You've successfully authenticated...

# If failed, generate SSH key
ssh-keygen -t ed25519 -C "your@email.com"

# Add key to GitHub:
# Settings > SSH and GPG keys > New SSH key
# Paste your public key

# Test again
ssh -T git@github.com

# If using HTTPS instead of SSH
git config --global url.git@github.com:.insteadOf https://github.com/
```

---

### "Please tell me who you are"

**Symptom**: Error when trying to commit

**Solution**:
```bash
# Configure globally (all repositories)
git config --global user.name "Your Name"
git config --global user.email "your@email.com"

# Or just for this repository
git config user.name "Your Name"
git config user.email "your@email.com"

# Verify
git config --list
```

---

### "Detached HEAD state"

**Symptom**: You're not on any branch

**Solution**:
```bash
# See current state
git status
# Shows: HEAD detached at <commit>

# Go back to main
git checkout main

# Or create a new branch from where you are
git checkout -b feature/my-feature
```

---

## 🟡 Merge Issues

### "Merge conflict - can't auto-merge"

**Symptom**: Conflict markers in files (`<<<<<<<`, `=======`, >>>>>>>`)

**Solution**:
```bash
# Identify conflicted files
git status
# Shows: both modified

# Open the file and resolve:
# Look for:
# <<<<<<<< HEAD
# Your changes
# =======
# Their changes
# >>>>>>>>>> branch-name

# Edit to keep what you want

# Mark as resolved
git add <filename>

# Complete merge
git commit -m "Merge: Resolve conflicts"
```

**Prevention**:
- Communicate with team about who's editing what
- Merge frequently from main into feature branches
- Keep commits focused and small

---

### "Your branch has diverged from origin"

**Symptom**: Branch history has split

**Solution**:
```bash
# See the divergence
git log --oneline --all --graph

# Option 1: Rebase (cleaner history)
git fetch origin
git rebase origin/main

# Option 2: Merge (keeps both histories)
git fetch origin
git merge origin/main

# Resolve any conflicts if they occur
```

---

### "Can't merge - unrelated histories"

**Symptom**: When merging unrelated repositories

**Solution**:
```bash
# Force merge if you know what you're doing
git merge --allow-unrelated-histories <branch>

# Then resolve any conflicts
```

---

## 🟡 Push/Pull Issues

### "Rejected push - non-fast forward"

**Symptom**: Can't push because remote is ahead

**Solution**:
```bash
# Pull latest first
git pull

# This fetches and merges
# Resolve any conflicts

# Then push
git push
```

**Don't do:**
```bash
git push -f  # Force push can overwrite others' work!
```

---

### "Pull shows: "Already up to date"

**Symptom**: Nothing happens when you pull

**Solution**:
This is normal! Your local branch is already synchronized.

```bash
# Verify you're tracking the right remote branch
git branch -vv

# Set upstream if needed
git branch --set-upstream-to=origin/main
```

---

### "I pushed to the wrong branch!"

**Symptom**: Commits went to main instead of feature branch

**Solution**:
```bash
# Don't panic! Commits aren't lost

# See what happened
git log --oneline -n 5

# Option 1: Revert the commits on main
git revert <commit-hash>
git push

# Option 2: Reset main (only if not pushed to others)
git reset --hard HEAD~1
git push -f origin main

# Create the feature branch with those commits
git checkout -b feature/my-feature
git log
```

---

## 🟡 History Issues

### "I need to fix the last commit message"

**Symptom**: Typo in commit message

**Solution**:
```bash
# If not pushed yet
git commit --amend -m "Correct message"

# If already pushed (and not shared)
git commit --amend -m "Correct message"
git push -f origin branch-name

# If already shared - DON'T amend!
# Instead, make a new commit
git commit -m "Correct previous message typo"
```

---

### "I want to undo the last commit but keep changes"

**Symptom**: Committed too early

**Solution**:
```bash
# Undo commit, keep changes staged
git reset --soft HEAD~1

# Or unstaged
git reset --mixed HEAD~1

# Files are back in working directory
git status

# Make more changes, then recommit
git add .
git commit -m "Complete feature"
```

---

### "How do I find when a bug was introduced?"

**Symptom**: Bug exists but don't know which commit caused it

**Solution**:
```bash
# Use bisect for binary search
git bisect start
git bisect bad          # Current commit has bug
git bisect good <old>   # Old commit was fine

# Git checks out commits, you test each
# Mark as good/bad
git bisect good
# or
git bisect bad

# Repeat until found
git bisect reset

# Git tells you the exact commit that broke it
```

---

## 🟢 Minor Issues (Annoyances)

### "I have untracked files I want to clean up"

**Solution**:
```bash
# See what would be deleted
git clean -fd --dry-run

# Actually delete
git clean -fd

# Also remove ignored files
git clean -fdx
```

---

### "Stashed changes getting lost"

**Solution**:
```bash
# List all stashes
git stash list

# See stash contents
git stash show -p stash@{0}

# Apply a specific stash
git stash apply stash@{0}

# For safety, create a branch from stash
git stash branch my-stash-branch
```

---

### "Can't remember what I changed"

**Solution**:
```bash
# See unstaged changes
git diff

# See staged changes
git diff --staged

# See what changed in specific file
git log -p <filename>

# See who changed what (blame)
git blame <filename>
```

---

### "Too many merge commits making history messy"

**Solution**:
```bash
# Rebase instead of merge for cleaner history
git fetch origin
git rebase origin/main

# Or squash commits when merging
git merge --squash feature/branch
git commit -m "Feature description"
```

---

## 🟢 Workflow Questions

### "When should I commit?"

✅ **Good times to commit:**
- Feature is complete
- Bug fix is complete and tested
- One logical unit of work
- Code is tested and working

❌ **Bad times to commit:**
- Half-finished feature
- Code is broken
- Random collection of changes

---

### "How detailed should commit messages be?"

✅ **Good commit message:**
```
feat: Add user authentication

Implemented login/logout functionality with JWT tokens.
Added password hashing and session management.

Fixes #123
```

❌ **Bad commit message:**
```
update
fixed stuff
wip
```

---

### "How many branches should I have?"

✅ **Healthy branching:**
- One main/master branch (production)
- One develop branch (integration)
- Short-lived feature branches (1-2 weeks max)
- Hotfix branches when needed

❌ **Bad branching:**
- Too many old branches
- Branches that never merge back
- Confusion about what each branch is for

---

## When to Ask for Help

🆘 **Ask a senior developer when:**
- You're about to force-push to a shared branch
- You lost commits and can't find them with reflog
- You have merge conflicts you can't resolve
- You accidentally committed sensitive data
- You're unsure about the right workflow

---

## Resources for More Help

- [Git Official Documentation](https://git-scm.com/doc)
- [GitHub Help](https://docs.github.com)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/git)
- Your team's Git wiki/documentation
- Your mentor or senior developer

---

## Remember

✅ **Git is forgiving** - Most mistakes can be recovered  
✅ **Communicate** - Tell your team if something went wrong  
✅ **Learn slowly** - Master basic commands before advanced ones  
✅ **Practice safely** - Experiment on test repositories  
✅ **Don't panic** - Take a breath and think through solutions  

**You've got this! 🚀**
