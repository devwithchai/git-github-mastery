# Exercise 2: Staging and Committing

## Objective
Understand the staging area and create your first meaningful commits.

## Prerequisites
Complete Exercise 1 first.

## Steps

### Step 1: Create More Files
```bash
echo "print('Hello Git')" > app.py
echo "*.pyc" > .gitignore
echo "DATABASE_URL=localhost" > .env
```

### Step 2: Check Status
```bash
git status
```

You should see 4 untracked files.

### Step 3: Add Files Selectively
Add only README and .gitignore:
```bash
git add README.md .gitignore
```

### Step 4: View Staging Area
```bash
git status
```

Notice:
- README.md and .gitignore are "Changes to be committed" (green)
- app.py and .env are still "Untracked files" (red)

### Step 5: Create First Commit
```bash
git commit -m "Initial commit: Add README and gitignore"
```

### Step 6: View Commit History
```bash
git log
git log --oneline
```

### Step 7: Add and Commit Remaining Files
```bash
git add app.py .env
git commit -m "Add application files"
```

### Step 8: View Complete History
```bash
git log --oneline
```

## Verification Checklist
- [ ] Two commits appear in log
- [ ] Commit messages are descriptive
- [ ] All files are committed
- [ ] `git status` shows "working tree clean"

## Useful Commands

```bash
# See what's staged
git diff --staged

# See what's modified but not staged
git diff

# See specific commit
git show <commit-hash>

# One-line format is easier to read
git log --oneline

# See commits with their changes
git log -p
```

## Practice

Modify files and practice:
1. Edit README.md
2. Stage with `git add`
3. Commit with descriptive message
4. Repeat 3-4 times
5. View history with `git log --oneline`
