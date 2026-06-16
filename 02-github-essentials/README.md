# Module 2: GitHub Essentials 🌐

Learn how to work with GitHub and collaborate with others.

## 🎯 Learning Objectives

By the end of this module, you will:
- ✅ Understand GitHub and remote repositories
- ✅ Clone repositories
- ✅ Push and pull changes
- ✅ Set up SSH authentication
- ✅ Manage multiple remotes
- ✅ Understand forking and contribution workflow

## 📖 Concepts

### 1. What is GitHub?
GitHub is a cloud platform for hosting Git repositories with added collaboration features.

**Key Features:**
- Host repositories online
- Collaboration tools
- Issue tracking
- Pull requests for code review
- Community and open source

### 2. Remote Repository
A copy of your repository stored on a server (GitHub).

```
Local Machine                GitHub Server
┌─────────────┐            ┌──────────────┐
│ Repository  │ ──push──→  │ Remote Repo  │
│             │ ←──pull──  │              │
└─────────────┘            └──────────────┘
```

### 3. SSH vs HTTPS Authentication

**HTTPS**: Uses username/password (simpler, less secure)
**SSH**: Uses key pairs (more secure, no password needed)

### 4. Common Workflows
- **Clone**: Copy remote repo locally
- **Push**: Send commits to remote
- **Pull**: Get changes from remote
- **Fetch**: Download without merging

## 🔧 Hands-On Exercises

### Exercise 1: Create GitHub Repository
**Goal**: Set up your first GitHub repository

**Tasks:**
1. Go to [github.com/new](https://github.com/new)
2. Repository name: `my-first-github-repo`
3. Description: "My first GitHub repository for learning"
4. Choose Public
5. Initialize with README: Yes
6. Create repository
7. Copy the repository URL

**Questions:**
- What URL did GitHub provide (HTTPS vs SSH)?
- What default files were created?

---

### Exercise 2: Clone a Repository
**Goal**: Copy a repository to your local machine

**Tasks:**
1. Clone your repository:
   ```bash
   git clone <your-repo-url>
   cd my-first-github-repo
   ```

2. List contents:
   ```bash
   ls -la
   ```

3. Check remotes:
   ```bash
   git remote -v
   ```

4. View branch:
   ```bash
   git branch -a
   ```

5. Check the log:
   ```bash
   git log --oneline
   ```

**Expected Output:**
- You see the README.md file
- `origin` remote points to GitHub
- You're on the `main` branch
- One commit (the GitHub-created README)

**Questions:**
- What is `origin`?
- Why are there two branches shown?
- What's the difference between local and remote branches?

---

### Exercise 3: Make and Push Changes
**Goal**: Modify code locally and push to GitHub

**Tasks:**
1. Edit README.md locally:
   ```bash
   echo "\n## About This Project\nLearning Git and GitHub" >> README.md
   ```

2. Check status:
   ```bash
   git status
   ```

3. Stage and commit:
   ```bash
   git add README.md
   git commit -m "Update README with project description"
   ```

4. Push to GitHub:
   ```bash
   git push
   ```
   Or: `git push origin main`

5. Go to GitHub and refresh to see your changes

6. View the commit on GitHub

**Questions:**
- What command did you use to push?
- What appeared in GitHub?
- How does the commit on GitHub compare to local?

---

### Exercise 4: Pull Changes from GitHub
**Goal**: Get changes made on GitHub into your local repo

**Tasks:**
1. Go to GitHub and edit README.md directly
2. Add some content
3. Commit the change (via GitHub UI)
4. In your terminal, pull the changes:
   ```bash
   git pull
   ```

5. View the updated file:
   ```bash
   cat README.md
   ```

6. Check log:
   ```bash
   git log --oneline
   ```

**Questions:**
- Where did that commit come from?
- What command could you use instead to see changes without merging?
- Why is `pull` = `fetch` + `merge`?

---

### Exercise 5: Working with Branches on GitHub
**Goal**: Collaborate using branches

**Tasks:**
1. Create a local feature branch:
   ```bash
   git checkout -b feature/add-license
   ```

2. Create a LICENSE file:
   ```bash
   echo "MIT License" > LICENSE
   ```

3. Commit it:
   ```bash
   git add LICENSE
   git commit -m "Add MIT license"
   ```

4. Push the branch to GitHub:
   ```bash
   git push -u origin feature/add-license
   ```

5. Go to GitHub and see your new branch

6. Go back to main locally:
   ```bash
   git checkout main
   ```

7. Pull to get any updates:
   ```bash
   git pull
   ```

8. Merge your feature:
   ```bash
   git merge feature/add-license
   ```

9. Push main to GitHub:
   ```bash
   git push
   ```

10. On GitHub, delete the feature branch (optional cleanup)

**Questions:**
- What's the difference between local and remote tracking branches?
- What does `-u` flag do in `git push -u`?
- How do branches appear on GitHub?

---

### Exercise 6: Forking a Repository (Open Source)
**Goal**: Contribute to open source

**Tasks:**
1. Find a simple GitHub repository to fork
   - Try: https://github.com/firstcontributions/first-contributions

2. Click "Fork" button (top right)

3. You now have your own copy

4. Clone YOUR fork (not the original):
   ```bash
   git clone <your-fork-url>
   ```

5. Create a feature branch:
   ```bash
   git checkout -b feature/my-contribution
   ```

6. Make some changes

7. Commit and push to your fork:
   ```bash
   git add .
   git commit -m "Add my contribution"
   git push origin feature/my-contribution
   ```

8. Go to your fork on GitHub

9. You'll see a "Compare & pull request" button

10. Click it to create a Pull Request to the original repository

**Questions:**
- What's the difference between fork and clone?
- Why create a fork vs just cloning?
- What's an "upstream" repository?

---

## 🎓 Practice Scenario

### Scenario: Team Collaboration

**Setup:**
1. Partner up with someone (or use two local clones)
2. Create one shared GitHub repository
3. Both clone it locally
4. Create different feature branches:
   - Person A: `feature/authentication`
   - Person B: `feature/database`
5. Each person makes changes on their branch
6. Both push their branches
7. Both pull latest main
8. Both merge their feature locally
9. Both push main
10. Verify both features are on GitHub

---

## ✅ Self-Assessment

Before moving to Module 3, ensure you can:
- [ ] Create a GitHub repository
- [ ] Clone a repository
- [ ] Push changes to GitHub
- [ ] Pull changes from GitHub
- [ ] Create and manage branches on GitHub
- [ ] Fork a repository
- [ ] Use remotes (`git remote`)
- [ ] Understand the difference between local and remote branches
- [ ] Create a pull request (basic)

---

## 🔗 Resources

- [GitHub Getting Started](https://docs.github.com/en/get-started)
- [About Remote Repositories](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)
- [GitHub Hello World](https://guides.github.com/activities/hello-world/)
- [Forking a Repository](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

---

## 📝 Next Steps

✅ **Completed Module 2?** Move to [Module 3: Advanced Workflows](../03-advanced-workflows/README.md)
