# Real-World Scenario 2: Open Source Contribution

## Scenario Overview

You found a bug in an open source project and want to contribute a fix.

**Project:** An open source Python library  
**Issue:** Users report a bug in the data validation function  
**Your Goal:** Fix the bug and have it accepted upstream

## Step-by-Step Workflow

### Step 1: Fork the Repository

1. Go to the original repository on GitHub
2. Click "Fork" (top right)
3. Now you have your own copy
4. GitHub redirects to your fork: `github.com/YOUR-USERNAME/project-name`

### Step 2: Clone Your Fork

```bash
# Clone YOUR fork, not the original
git clone https://github.com/YOUR-USERNAME/project-name.git
cd project-name

# Verify remote
git remote -v
# Should show your fork as origin
```

### Step 3: Add Upstream Remote

```bash
# Add the original repository as upstream
git remote add upstream https://github.com/ORIGINAL-OWNER/project-name.git

# Verify both remotes
git remote -v
# origin   - your fork
# upstream - original repo
```

### Step 4: Sync with Upstream

```bash
# Fetch latest from upstream
git fetch upstream

# Create branch from upstream/main
git checkout -b fix/data-validation-bug

# Base it on upstream
git merge upstream/main
```

### Step 5: Reproduce and Fix the Bug

```bash
# First, reproduce the bug
# Run their test suite
python -m pytest

# Look at the failing test
cat tests/test_validation.py

# Examine the buggy code
cat src/validation.py

# Make your fix
# Edit the file to fix the bug

# Create a test case for the bug
echo "def test_validation_edge_case(): ..." >> tests/test_validation.py

# Verify your fix works
python -m pytest

# All tests should pass
```

### Step 6: Commit with Clear Messages

```bash
# Commit your fix
git add .
git commit -m "fix: Resolve data validation bug with edge cases

The validation function was failing when given None values
in certain conditions. This commit adds proper null checking
and adds test cases for edge cases.

Fixes #123"
```

### Step 7: Push to Your Fork

```bash
# Push to your fork
git push -u origin fix/data-validation-bug
```

### Step 8: Create Pull Request to Upstream

1. Go to your fork on GitHub
2. Click "Contribute" button
3. Click "Open pull request"
4. This creates PR against the original repository
5. Fill in PR details:
   ```
   ## Description
   Fixes the data validation bug reported in issue #123
   
   ## Changes
   - Add null checking in validation function
   - Add test cases for edge cases
   - Update documentation
   
   ## How to Test
   Run: python -m pytest
   All tests pass
   
   ## Checklist
   - [x] Tests pass locally
   - [x] Added tests for new functionality
   - [x] Updated documentation
   ```

### Step 9: Respond to Maintainer Feedback

Maintainers review your code:

```bash
# They request changes: "Add more edge case tests"

# You add more tests
echo "def test_validation_more_cases(): ..." >> tests/test_validation.py

# Commit and push
git add tests/test_validation.py
git commit -m "test: Add additional edge case tests"
git push

# New commit appears in PR automatically
```

### Step 10: Celebrate Your Contribution

Once approved and merged:

```bash
# Your fix is now in the official repository
# It will be part of the next release
# You're now a contributor! 🎉

# Keep your fork updated
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

## Important Etiquette

✅ Check if issue/fix already exists  
✅ Read CONTRIBUTING.md guidelines  
✅ Follow the project's code style  
✅ Write clear, descriptive messages  
✅ Add tests for your changes  
✅ Update documentation  
✅ Be patient and respectful  
✅ Respond to feedback constructively  

## Dealing with Rejection

Not all PRs are accepted. Maintainers might:
- Ask for significant changes
- Suggest a different approach
- Close if it's out of scope

**This is normal!** Thank them for feedback and learn for next time.

## Common Issues

### Issue: "Your fork is out of date"

```bash
# Sync your fork with upstream
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

### Issue: "Your PR has merge conflicts"

```bash
# Rebase on latest upstream
git fetch upstream
git rebase upstream/main

# Resolve any conflicts
# Then force push (only for PRs, not shared branches)
git push -f origin fix/data-validation-bug
```

### Issue: "CI/CD tests are failing"

```bash
# Check the error messages in GitHub Actions
# Run tests locally to debug
python -m pytest -v

# Fix issues and push
git add .
git commit -m "ci: Fix failing tests"
git push
```

## Your First Contribution Checklist

- [ ] Forked the repository
- [ ] Cloned your fork
- [ ] Added upstream remote
- [ ] Created feature branch from upstream
- [ ] Fixed the bug/added feature
- [ ] Tests pass locally
- [ ] Committed with clear message
- [ ] Pushed to your fork
- [ ] Created PR to upstream
- [ ] Responded to feedback
- [ ] PR was merged
- [ ] Celebrated your contribution!

## Next Scenario

👉 [Scenario 3: Emergency Hotfix](./scenario-3-emergency-hotfix.md)
