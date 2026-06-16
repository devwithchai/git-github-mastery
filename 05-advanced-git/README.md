# Module 5: Advanced Git 🎯

Master professional Git techniques for expert-level development.

## 🎯 Learning Objectives

By the end of this module, you will:
- ✅ Use reflog to recover lost commits
- ✅ Understand and use Git hooks
- ✅ Work with submodules
- ✅ Use worktrees for parallel work
- ✅ Bisect to find bugs
- ✅ Perform advanced rebasing
- ✅ Understand Git internals

## 📖 Concepts

### 1. Reflog (Reference Log)
Track all changes to HEAD, not just commits.

**Use Case**: Recover deleted branches, lost commits

### 2. Git Hooks
Automated scripts that run at Git events.

**Types:**
- Pre-commit: Before committing
- Pre-push: Before pushing
- Post-checkout: After switching branches

### 3. Submodules
Nest one Git repository inside another.

**Use Case**: Manage dependencies, shared libraries

### 4. Worktrees
Multiple working directories for the same repository.

**Use Case**: Work on multiple branches simultaneously

### 5. Bisect
Binary search to find which commit introduced a bug.

### 6. Git Internals
Understanding how Git stores data (objects, refs, etc.)

## 🔧 Hands-On Exercises

### Exercise 1: Using Reflog to Recover Lost Commits
**Goal**: Recover accidentally deleted work

**Tasks:**
1. Create some commits:
   ```bash
   git checkout -b temp-branch
   echo "work" > file.txt
   git add . && git commit -m "Work on feature"
   echo "more work" >> file.txt
   git add . && git commit -m "Continue feature"
   ```

2. Check current HEAD:
   ```bash
   git log --oneline -n 2
   ```

3. Note the latest commit hash

4. Switch to main and delete the branch:
   ```bash
   git checkout main
   git branch -D temp-branch
   ```

5. Realize you lost important work!

6. Use reflog to find it:
   ```bash
   git reflog
   ```

7. You'll see entries showing where HEAD was

8. Recover the branch:
   ```bash
   git branch temp-branch <hash-from-reflog>
   ```

9. Verify your commits are back:
   ```bash
   git log temp-branch --oneline -n 2
   ```

**Questions:**
- What does reflog show?
- How is reflog different from git log?
- Can you recover deleted branches?

---

### Exercise 2: Setting Up Git Hooks
**Goal**: Automate tasks with hooks

**Tasks:**
1. Navigate to hooks directory:
   ```bash
   cd .git/hooks
   ls
   ```

2. Create a pre-commit hook:
   ```bash
   cat > pre-commit << 'EOF'
   #!/bin/bash
   echo "Running pre-commit checks..."
   
   # Check for debugging code
   if git diff --cached | grep -q "console.log\|debugger\|pdb.set_trace"; then
       echo "Error: Debugging code detected!"
       exit 1
   fi
   
   echo "Pre-commit checks passed!"
   exit 0
   EOF
   ```

3. Make it executable:
   ```bash
   chmod +x pre-commit
   ```

4. Go back to repo:
   ```bash
   cd ../..
   ```

5. Test the hook:
   ```bash
   echo "console.log('test')" > debug.js
   git add debug.js
   git commit -m "Test"
   ```
   Should fail with "Debugging code detected!"

6. Remove debug code and commit again:
   ```bash
   echo "// normal code" > debug.js
   git add debug.js
   git commit -m "Add normal code"
   ```
   Should succeed!

**Questions:**
- Why use hooks instead of manual checks?
- What other hooks could be useful?
- How do you skip hooks when needed?

---

### Exercise 3: Working with Submodules
**Goal**: Manage nested repositories

**Tasks:**
1. Create a "dependency" repository first (simulated):
   ```bash
   mkdir utils-lib
   cd utils-lib
   git init
   echo "# Utils Library" > README.md
   git add . && git commit -m "Initial commit"
   cd ..
   ```

2. In your main repo, add the submodule:
   ```bash
   git submodule add ./utils-lib utilities
   ```

3. Check what was created:
   ```bash
   ls -la
   cat .gitmodules
   ```

4. Commit the changes:
   ```bash
   git add .
   git commit -m "Add utilities submodule"
   ```

5. When cloning, remember to initialize submodules:
   ```bash
   git clone --recurse-submodules <repo-url>
   # Or if already cloned:
   git submodule init
   git submodule update
   ```

**Questions:**
- What does .gitmodules contain?
- How do submodules differ from dependencies in package managers?
- When would you use submodules vs copying code?

---

### Exercise 4: Using Worktrees
**Goal**: Work on multiple branches simultaneously

**Tasks:**
1. List current worktrees:
   ```bash
   git worktree list
   ```

2. Create a new worktree for a different branch:
   ```bash
   git worktree add ../my-repo-feature feature/new-feature
   ```

3. You now have two working directories:
   ```bash
   ls ..  # See both directories
   ```

4. In the new worktree, make changes:
   ```bash
   cd ../my-repo-feature
   echo "feature code" > feature.txt
   git add . && git commit -m "Add feature"
   ```

5. Go back to main worktree:
   ```bash
   cd ../my-repo
   ```

6. Make different changes:
   ```bash
   echo "main code" > main.txt
   git add . && git commit -m "Add to main"
   ```

7. Both changes exist simultaneously!

8. Remove worktree when done:
   ```bash
   git worktree remove ../my-repo-feature
   ```

**Questions:**
- Why is this useful vs just switching branches?
- Can you have the same branch in multiple worktrees?
- How does this improve workflow?

---

### Exercise 5: Using Bisect to Find Bugs
**Goal**: Locate the commit that introduced a bug

**Tasks:**
1. Create a repo with a bug introduced partway through:
   ```bash
   # Commit 1: Good
   echo "version = 1" > version.txt
   git add . && git commit -m "v1"
   
   # Commit 2: Good
   echo "version = 2" > version.txt
   git add . && git commit -m "v2"
   
   # Commit 3: BAD BUG
   echo "version = 3 BUG" > version.txt
   git add . && git commit -m "v3"
   
   # Commit 4: Still has bug
   echo "version = 4 BUG" > version.txt
   git add . && git commit -m "v4"
   
   # Commit 5: Bug fixed
   echo "version = 5" > version.txt
   git add . && git commit -m "v5"
   ```

2. Start bisect:
   ```bash
   git bisect start
   ```

3. Mark current as bad:
   ```bash
   git bisect bad
   ```

4. Mark a known good commit:
   ```bash
   git bisect good HEAD~5
   ```

5. Git checks out a commit in the middle

6. Test if this commit has the bug

7. Mark as good or bad:
   ```bash
   git bisect good  # if no bug
   # or
   git bisect bad   # if bug exists
   ```

8. Repeat until bisect finds the exact commit

9. Exit bisect:
   ```bash
   git bisect reset
   ```

**Questions:**
- How many commits did bisect check?
- Could you do this manually faster?
- How does binary search help here?

---

## 🎓 Practice Scenario

### Scenario: Professional Workflow

**Tasks:**
1. Create hooks for code quality
2. Add a submodule to your repository
3. Use worktrees to work on multiple features
4. Create a commit with a bug (intentional)
5. Use bisect to find it
6. Fix and test
7. Use reflog to see your entire history

---

## ✅ Self-Assessment

Before considering yourself proficient, ensure you can:
- [ ] Use reflog to recover lost commits
- [ ] Create and test Git hooks
- [ ] Add and manage submodules
- [ ] Create and use worktrees
- [ ] Use bisect to find bugs
- [ ] Understand Git objects (blobs, trees, commits)
- [ ] Perform complex rebases
- [ ] Recover from any Git disaster

---

## 🔗 Resources

- [Git Internals](https://git-scm.com/book/en/v2/Git-Internals-Plumbing-and-Porcelain)
- [Git Hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)
- [Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)
- [Worktrees](https://git-scm.com/docs/git-worktree)
- [Bisect](https://git-scm.com/docs/git-bisect)

---

## 🎉 Congratulations!

You've completed all 5 modules! You now have professional Git and GitHub skills.

## 📝 Next: Real-World Scenarios

Move to [Real-World Scenarios](../real-world-scenarios/) to practice complete workflows.
