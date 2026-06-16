# Real-World Scenario 1: Team Project Development

## Scenario Overview

You're joining a team of 3 developers working on a web application. The project uses Git for version control and GitHub for collaboration.

**Team Setup:**
- Main repository on GitHub
- `main` branch: Production code (protected)
- `develop` branch: Integration branch
- Feature branches: Individual features
- CI/CD: Tests run on every PR

## Your Task

Implement a new "User Authentication" feature for the application.

## Step-by-Step Workflow

### Step 1: Set Up Local Environment

```bash
# Clone the repository
git clone https://github.com/team/web-app.git
cd web-app

# Configure your identity (if not done globally)
git config user.name "Your Name"
git config user.email "your@email.com"

# Verify remotes
git remote -v
# Should show:
# origin  https://github.com/team/web-app.git (fetch)
# origin  https://github.com/team/web-app.git (push)
```

### Step 2: Sync with Latest Code

```bash
# Fetch latest from GitHub
git fetch origin

# Check current branch
git branch -a

# Switch to develop (integration branch)
git checkout develop

# Pull latest changes
git pull origin develop
```

### Step 3: Create Feature Branch

```bash
# Create a branch from develop
git checkout -b feature/user-authentication

# Verify you're on new branch
git branch
# Should show: * feature/user-authentication
```

### Step 4: Implement the Feature

Make multiple commits as you develop:

```bash
# First commit: Set up authentication module
echo "# Authentication module" > auth.py
git add auth.py
git commit -m "feat: Create authentication module structure"

# Second commit: Add login functionality
echo "def login(username, password): pass" >> auth.py
git add auth.py
git commit -m "feat: Add login function"

# Third commit: Add logout functionality
echo "def logout(): pass" >> auth.py
git add auth.py
git commit -m "feat: Add logout function"

# Fourth commit: Add tests
echo "# Tests" > test_auth.py
git add test_auth.py
git commit -m "test: Add authentication tests"
```

### Step 5: Push to GitHub

```bash
# Push branch to GitHub (first time)
git push -u origin feature/user-authentication

# On subsequent pushes, just:
git push
```

### Step 6: Create Pull Request

1. Go to GitHub
2. You'll see "Compare & pull request" button
3. Click it
4. Fill in PR details:
   - **Title**: "Add User Authentication System"
   - **Description**:
     ```
     ## Description
     Implements user authentication system with login/logout functionality.
     
     ## Changes
     - Create auth module
     - Add login functionality
     - Add logout functionality
     - Add comprehensive tests
     
     ## Related Issues
     Closes #42
     
     ## Testing
     - All tests pass locally
     - Manual testing completed
     ```
5. Request reviewers (team members)
6. Create PR

### Step 7: Address Code Review

Team members review and suggest changes:

```bash
# They comment: "Add docstrings to functions"

# You make the changes
echo "def login(username, password):\n    \"\"\"Authenticate user\"\"\"\n    pass" > auth.py

# Commit and push
git add auth.py
git commit -m "docs: Add docstrings to auth functions"
git push

# The new commit automatically appears in the PR
```

### Step 8: Handle Merge Conflict

While you were working, someone merged another feature that modified the same file:

```bash
# GitHub says: "Can't automatically merge"

# Option 1: Resolve on GitHub
# Click "Resolve conflicts" button, edit, mark resolved

# Option 2: Resolve locally
git fetch origin
git merge origin/develop
# CONFLICT indicators appear

# Edit the conflicted files
# Keep your changes + their changes where appropriate

# Mark as resolved
git add .
git commit -m "merge: Resolve conflicts with develop"
git push
```

### Step 9: Final Approval and Merge

Once all reviews approve:

```bash
# On GitHub, click "Merge pull request"
# Choose merge strategy: "Create a merge commit"
# Confirm merge
```

### Step 10: Cleanup

```bash
# Delete the feature branch locally
git branch -d feature/user-authentication

# Delete on GitHub (can do via GitHub UI or:
git push origin --delete feature/user-authentication

# Switch back to develop
git checkout develop

# Pull the merged changes
git pull origin develop

# You now have the merged feature in develop
```

## Common Issues and Solutions

### Issue 1: "Your branch has diverged"

```bash
# Your local branch is out of sync
git pull origin feature/user-authentication
# or
git fetch origin
git rebase origin/feature/user-authentication
```

### Issue 2: "Permission denied (publickey)"

You need to set up SSH:
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your@email.com"

# Add to GitHub:
# Settings > SSH and GPG keys > New SSH key
# Paste public key

# Test connection
ssh -T git@github.com
```

### Issue 3: "Merge conflict can't be automatically resolved"

See Step 8 above for resolution strategies.

### Issue 4: "Accidentally committed to main"

```bash
# Create new branch from current state
git branch feature/oops

# Reset main to previous state
git reset --hard origin/main

# Switch to feature branch
git checkout feature/oops
```

## Key Takeaways

✅ Always work on feature branches, never directly on main/develop  
✅ Write clear commit messages  
✅ Make small, focused commits  
✅ Pull latest before starting work  
✅ Respond to code review feedback promptly  
✅ Test before pushing  
✅ Keep PRs focused on one feature  
✅ Communicate with your team

## Next Scenario

👉 [Scenario 2: Open Source Contribution](./scenario-2-open-source.md)
