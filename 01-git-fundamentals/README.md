# Module 1: Git Fundamentals 📚

Master the core concepts of Git - the foundation for everything else.

## 🎯 Learning Objectives

By the end of this module, you will:
- ✅ Understand Git's core concepts (repository, commits, staging)
- ✅ Initialize and configure Git repositories
- ✅ Create meaningful commits
- ✅ Navigate commit history
- ✅ Create and switch between branches
- ✅ Merge branches
- ✅ Handle basic conflicts

## 📖 Concepts Covered

### 1. What is Git?
Git is a distributed version control system that tracks changes in your code over time.

**Key Points:**
- Every developer has a complete copy of the repository
- All history is stored locally
- Changes are tracked at the line level
- Enables collaboration and version history

### 2. Repository Structure
```
Your Project/
├── .git/                    # Hidden Git directory (DO NOT EDIT)
│   ├── objects/            # Compressed file history
│   ├── refs/               # Branch and tag references
│   ├── HEAD                # Current branch pointer
│   └── config              # Repository configuration
├── file1.txt               # Your files
├── file2.py
└── ...
```

### 3. Three States of Git

```
┌──────────────────┐
│  Working Dir     │  (Your local files)
│  Modified        │
└────────┬─────────┘
         │ git add
         ▼
┌──────────────────┐
│  Staging Area    │  (Index - ready to commit)
│  Staged          │
└────────┬─────────┘
         │ git commit
         ▼
┌──────────────────┐
│  Repository      │  (Permanent history)
│  Committed       │
└──────────────────┘
```

### 4. Commits
A commit is a snapshot of your project with:
- **SHA Hash**: Unique identifier (e.g., `a1b2c3d4...`)
- **Author**: Who made the change
- **Date**: When it was made
- **Message**: What changed and why
- **Content**: The actual changes

### 5. Branches
Branches are parallel lines of development.
- **main/master**: Production-ready code
- **feature branches**: New features being developed
- **bugfix branches**: Bug fixes

Benefits:
- Multiple people can work simultaneously
- Isolate changes until ready
- Easy to switch between tasks

## 🛠️ Hands-On Exercises

### Exercise 1: Initialize and Configure
**Goal**: Set up your first Git repository

**Tasks:**
1. Create a new directory: `mkdir my-first-repo`
2. Navigate into it: `cd my-first-repo`
3. Initialize Git: `git init`
4. Configure your name and email:
   ```bash
   git config user.name "Your Name"
   git config user.email "your@email.com"
   ```
5. Create a file: `echo "Hello Git" > README.md`
6. Check status: `git status`

**Expected Output:**
You should see `README.md` listed as an untracked file.

**Questions:**
- What does the `.git` directory contain?
- Why do we need to configure name and email?

---

### Exercise 2: Staging and Committing
**Goal**: Understand the staging area

**Tasks:**
1. Stage the README: `git add README.md`
2. Check status: `git status` (should show staged changes)
3. Create another file: `echo "print('Hello')" > app.py`
4. View status again: `git status` (one staged, one untracked)
5. Stage the second file: `git add app.py`
6. Create your first commit:
   ```bash
   git commit -m "Initial commit: Add README and app.py"
   ```
7. View the log: `git log`

**Questions:**
- Why do we need both `add` and `commit`?
- What information is shown in `git log`?
- How would you see the changes in a specific commit?

---

### Exercise 3: Modifying Commits
**Goal**: Practice working with commit history

**Tasks:**
1. Modify README: `echo "Updated README" > README.md`
2. Add and commit:
   ```bash
   git add README.md
   git commit -m "Update README"
   ```
3. Make a typo in the message and add another file:
   ```bash
   echo "# Config" > config.ini
   git add config.ini
   git commit -m "Add config file"
   ```
4. Oops! Let's fix the typo with amend:
   ```bash
   git commit --amend -m "Add configuration file"
   ```
5. View log again: `git log --oneline`

**Questions:**
- What happened to the previous commit?
- Why should we only amend commits we haven't pushed yet?
- How many commits do you have now?

---

### Exercise 4: Branching Basics
**Goal**: Master branch creation and switching

**Tasks:**
1. List current branches: `git branch`
2. Create a feature branch: `git branch feature/add-logging`
3. List branches again: `git branch` (notice the `*`)
4. Switch to the new branch: `git checkout feature/add-logging`
5. View branches: `git branch` (now on feature branch)
6. Create a new file: `echo "# Logging setup" > logging.py`
7. Commit it:
   ```bash
   git add logging.py
   git commit -m "Add logging module"
   ```
8. Switch back to main: `git checkout main`
9. Check your files: `ls` (logging.py should be gone)
10. Switch back to feature: `git checkout feature/add-logging`
11. Check files again: `ls` (logging.py is back)

**Questions:**
- Why does logging.py disappear when you switch branches?
- How can you see all branches including remote ones?
- What does the `*` in `git branch` output mean?

---

### Exercise 5: Merging Branches
**Goal**: Combine work from different branches

**Tasks:**
1. Make sure you're on feature branch: `git status`
2. Make another change: `echo "logger = setup()" >> logging.py`
3. Commit it: `git add logging.py && git commit -m "Complete logging setup"`
4. Switch to main: `git checkout main`
5. Merge the feature: `git merge feature/add-logging`
6. View log: `git log --oneline --graph --all`
7. List branches: `git branch` (feature branch still exists)
8. Delete the feature branch: `git branch -d feature/add-logging`

**Questions:**
- What type of merge occurred (fast-forward or three-way)?
- Why can you still see the feature branch in the log after deleting it?
- How would you undo a merge if something went wrong?

---

### Exercise 6: Handling Conflicts
**Goal**: Resolve merge conflicts

**Tasks:**
1. Create a new branch: `git checkout -b feature/edit-readme`
2. Edit README: `echo "Feature Version" > README.md`
3. Commit: `git add README.md && git commit -m "Update README from feature"`
4. Switch to main: `git checkout main`
5. Edit README differently: `echo "Main Version" > README.md`
6. Commit: `git add README.md && git commit -m "Update README from main"`
7. Try to merge: `git merge feature/edit-readme`
8. **CONFLICT!** View the file: `cat README.md`
9. Edit README to keep both versions:
   ```
   Main Version
   Feature Version
   ```
10. Mark as resolved: `git add README.md`
11. Complete merge: `git commit -m "Merge feature/edit-readme - resolve conflict"`
12. View final log: `git log --oneline --graph --all`

**Questions:**
- What do the `<<<<<<<`, `=======`, and `>>>>>>>` markers mean?
- How do you know when a conflict is fully resolved?
- Could this conflict have been prevented?

---

## 🎓 Practice Project

### Build a Simple Project Repository

**Scenario**: You're starting a new Python project called "calculator"

**Tasks**:
1. Create and initialize a repo
2. Create initial commit with:
   - `README.md` (project description)
   - `calculator.py` (empty main file)
   - `.gitignore` (exclude `__pycache__`)

3. Create feature branches for:
   - `feature/addition` - implement addition function
   - `feature/subtraction` - implement subtraction function
   - `feature/multiplication` - implement multiplication function

4. Make commits in each branch implementing the feature

5. Merge all branches back to main

6. Create one intentional conflict and resolve it

7. View the complete history: `git log --oneline --graph --all`

---

## ✅ Self-Assessment

Before moving to Module 2, ensure you can:
- [ ] Initialize a Git repository
- [ ] Configure user information
- [ ] Stage and commit changes
- [ ] View commit history
- [ ] Create and delete branches
- [ ] Switch between branches
- [ ] Merge branches
- [ ] Resolve merge conflicts
- [ ] Amend commits
- [ ] Use .gitignore effectively

---

## 🔗 Resources

- [Git Basics - Chapter 2 of Pro Git](https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository)
- [Understanding Branches](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)
- [Merging in Git](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)

---

## 📝 Next Steps

✅ **Completed Module 1?** Move to [Module 2: GitHub Essentials](../02-github-essentials/README.md)
