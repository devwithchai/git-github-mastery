# Module 3: Advanced Workflows 🚀

Master advanced Git techniques for professional development.

## 🎯 Learning Objectives

By the end of this module, you will:
- ✅ Use rebase instead of merge
- ✅ Perform interactive rebasing
- ✅ Cherry-pick specific commits
- ✅ Stash and apply changes
- ✅ Create and manage tags
- ✅ Use bisect to find bugs
- ✅ Understand squashing commits

## 📖 Concepts

### 1. Rebasing vs Merging

**Merge**: Creates a merge commit, keeps history intact
```
feature          merge commit
  \               /
   ◄─────────────┐
                main
```

**Rebase**: Replays commits on top, cleaner history
```
        feature
          ◄──┐
feature commits
          ───┘
              main
```

### 2. Interactive Rebase
Rewrite, reorder, or squash commits before merging.

### 3. Cherry-picking
Apply a specific commit from one branch to another.

### 4. Stashing
Temporarily save changes without committing.

### 5. Tags
Mark specific points in history (e.g., releases).

## 🔧 Hands-On Exercises

### Exercise 1: Rebasing Instead of Merging
**Goal**: Create a clean, linear history

**Tasks:**
1. Create and switch to a feature branch:
   ```bash
   git checkout -b feature/rebase-demo
   ```

2. Make 3 commits:
   ```bash
   echo "feature 1" > feature1.txt
   git add . && git commit -m "Add feature 1"
   
   echo "feature 2" > feature2.txt
   git add . && git commit -m "Add feature 2"
   
   echo "feature 3" > feature3.txt
   git add . && git commit -m "Add feature 3"
   ```

3. Switch back to main:
   ```bash
   git checkout main
   ```

4. Make a commit on main:
   ```bash
   echo "main update" > main-file.txt
   git add . && git commit -m "Update main"
   ```

5. Switch back to feature:
   ```bash
   git checkout feature/rebase-demo
   ```

6. Rebase onto main:
   ```bash
   git rebase main
   ```

7. View the log:
   ```bash
   git log --oneline --graph --all
   ```

**Questions:**
- What changed in the commit history?
- Are the feature commits on top of main now?
- What are the new commit hashes?

---

### Exercise 2: Interactive Rebase and Squashing
**Goal**: Clean up commits before merging

**Tasks:**
1. Create a branch with messy commits:
   ```bash
   git checkout -b feature/messy
   
   echo "initial" > messy.txt && git add . && git commit -m "initial"
   echo "fix typo" >> messy.txt && git add . && git commit -m "fix typo"
   echo "add more" >> messy.txt && git add . && git commit -m "add more"
   echo "forgot this" >> messy.txt && git add . && git commit -m "forgot this"
   ```

2. Start interactive rebase:
   ```bash
   git rebase -i HEAD~4
   ```

3. Your editor opens. Change it to:
   ```
   pick <hash1> initial
   squash <hash2> fix typo
   squash <hash3> add more
   squash <hash4> forgot this
   ```

4. Save and close (`:wq` in vim)

5. Edit the commit message to:
   ```
   Add messy feature with all fixes
   ```

6. Verify you have one commit:
   ```bash
   git log --oneline -n 5
   ```

**Questions:**
- How many commits do you have now?
- What happened to the original commits?
- Why is this useful before merging?

---

### Exercise 3: Cherry-picking
**Goal**: Apply specific commits to another branch

**Tasks:**
1. Create a branch with several commits:
   ```bash
   git checkout -b feature/cherry-source
   
   echo "fix" > fix1.txt && git add . && git commit -m "Fix bug #1"
   echo "feature" > feature4.txt && git add . && git commit -m "Add feature 4"
   echo "fix" > fix2.txt && git add . && git commit -m "Fix bug #2"
   ```

2. Note the hashes:
   ```bash
   git log --oneline -n 3
   ```

3. Switch to main:
   ```bash
   git checkout main
   ```

4. Cherry-pick only the bug fixes:
   ```bash
   git cherry-pick <hash-of-fix-bug-1>
   git cherry-pick <hash-of-fix-bug-2>
   ```

5. View main branch:
   ```bash
   git log --oneline -n 5
   ```

**Questions:**
- Which commits were applied to main?
- Why wasn't the feature commit included?
- When would cherry-picking be useful?

---

### Exercise 4: Stashing Changes
**Goal**: Temporarily save work without committing

**Tasks:**
1. Make some changes without committing:
   ```bash
   echo "work in progress" > wip.txt
   echo "more changes" >> README.md
   ```

2. Check status:
   ```bash
   git status
   ```

3. Stash the changes:
   ```bash
   git stash
   ```

4. Verify working directory is clean:
   ```bash
   git status
   ```

5. List stashes:
   ```bash
   git stash list
   ```

6. Apply the stash:
   ```bash
   git stash pop
   ```

7. Verify your changes are back:
   ```bash
   git status
   ```

**Questions:**
- What happened to your changes?
- When would stashing be useful?
- How is stashing different from committing?

---

### Exercise 5: Using Tags
**Goal**: Mark important points in history

**Tasks:**
1. Create a lightweight tag:
   ```bash
   git tag v1.0.0
   ```

2. Create an annotated tag:
   ```bash
   git tag -a v1.0.1 -m "Version 1.0.1 - Bug fixes"
   ```

3. List tags:
   ```bash
   git tag
   ```

4. Show tag info:
   ```bash
   git show v1.0.1
   ```

5. Push tags to GitHub:
   ```bash
   git push origin v1.0.0 v1.0.1
   ```
   Or push all tags:
   ```bash
   git push origin --tags
   ```

6. Checkout a tag (detached HEAD):
   ```bash
   git checkout v1.0.0
   ```

7. Go back to main:
   ```bash
   git checkout main
   ```

**Questions:**
- What's the difference between lightweight and annotated tags?
- How are tags useful for releases?
- Can you modify a tag after creation?

---

## 🎓 Practice Scenario

### Scenario: Preparing for Release

**Tasks:**
1. Create a feature branch: `feature/release-prep`
2. Make 5-6 small commits (testing, fixes, updates)
3. Use interactive rebase to squash related commits
4. Rebase onto main (practice clean merge)
5. Create an annotated tag: `v1.0.0`
6. Cherry-pick a bug fix from another branch
7. Create another tag: `v1.0.1`
8. Push everything to GitHub

---

## ✅ Self-Assessment

Before moving to Module 4, ensure you can:
- [ ] Rebase a branch onto another
- [ ] Perform interactive rebase
- [ ] Squash multiple commits
- [ ] Cherry-pick specific commits
- [ ] Stash and pop changes
- [ ] Create lightweight and annotated tags
- [ ] Push tags to remote
- [ ] Checkout specific tags

---

## 🔗 Resources

- [Git Rebasing](https://git-scm.com/book/en/v2/Git-Branching-Rebasing)
- [Interactive Rebasing](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
- [Cherry-picking](https://git-scm.com/docs/git-cherry-pick)
- [Git Tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging)

---

## 📝 Next Steps

✅ **Completed Module 3?** Move to [Module 4: Collaboration & PRs](../04-collaboration-prs/README.md)
