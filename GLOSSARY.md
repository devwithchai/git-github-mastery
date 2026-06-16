# Git & GitHub Glossary

Essential terms and concepts explained simply.

## Core Concepts

### Repository (Repo)
A directory containing your project files and the complete history of changes. Every project has a `.git` directory that stores all version control information.

**Example**: Your project folder with all code and history.

### Commit
A snapshot of your project at a specific point in time. Each commit includes changes, metadata (author, date), and a unique ID (SHA hash).

**Example**: "Added login feature" - this is one commit.

### Branch
A parallel version of your repository. Allows multiple people to work on different features simultaneously without interfering with each other.

**Example**: `main` (production), `develop` (development), `feature/new-ui` (feature).

### Remote
A version of your repository hosted on a server (like GitHub). You can push changes to and pull changes from remotes.

**Example**: `origin` (GitHub), `upstream` (original repo you forked from).

### HEAD
A pointer to the current commit you're working on. It usually points to the current branch.

**Example**: If you're on `main`, HEAD points to the latest commit in `main`.

## Working Directory States

### Untracked Files
Files in your repository that Git doesn't know about. They're not in version control yet.

**Example**: A new file you just created.

### Modified (Unstaged)
Files you've changed but haven't added to the staging area yet.

**Example**: You edited `config.py` but didn't run `git add`.

### Staged (Indexed)
Changes ready to be committed. Added to the staging area with `git add`.

**Example**: You ran `git add config.py` and it's now ready to commit.

### Committed
Changes permanently saved to the repository history.

**Example**: You ran `git commit` and the changes are now in history.

## Common Operations

### Staging Area (Index)
A preparation area between working directory and repository. You stage changes here before committing.

**Workflow**: Edit files → Stage changes → Commit

### Merge
Combining changes from one branch into another, typically creating a "merge commit."

**Example**: Merging `feature/login` into `main` when the feature is complete.

### Rebase
Moving or reordering commits. Advanced merging that rewrites history.

**Example**: Moving your feature commits on top of the latest `main` commits.

### Conflict
When changes in different branches affect the same lines of code, Git can't automatically merge them.

**Example**: You changed line 10, and someone else also changed line 10 differently.

### Cherry-pick
Applying a specific commit from one branch to another.

**Example**: "I want this bug fix from the develop branch on my feature branch."

### Stash
Temporarily saving changes without committing them.

**Example**: You're working on something, need to switch branches, but don't want to commit yet.

## GitHub-Specific Terms

### Pull Request (PR)
A proposal to merge your branch into another branch. It's where code review happens.

**Example**: "I've added a new feature, here's my PR for review."

### Fork
Creating your own copy of someone else's repository.

**Example**: You fork an open-source project to contribute to it.

### Clone
Creating a local copy of a remote repository.

**Example**: `git clone https://github.com/user/repo.git` downloads the entire project.

### Push
Sending your commits to a remote repository.

**Example**: `git push origin main` sends your commits to GitHub.

### Pull
Fetching and merging changes from a remote repository.

**Example**: `git pull origin main` gets the latest changes from GitHub's main branch.

### Fetch
Downloading changes from a remote repository without merging them.

**Example**: `git fetch` checks what's new on GitHub but doesn't change your files.

### Upstream
The original repository you forked from or the main project repository.

**Example**: In an open-source contribution, the original project is "upstream."

### Collaborator
Someone who has write access to your repository.

**Example**: You can push directly to a repository where you're a collaborator.

### Contributor
Someone who has made changes to a project, usually through pull requests.

**Example**: Open-source contributors submit PRs to projects.

## Commit-Related Terms

### Commit Hash (SHA)
A unique 40-character identifier for each commit, generated from the commit's content.

**Example**: `a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0`

### Commit Message
Text describing what changes were made in a commit. Should be clear and concise.

**Example**: "Fix login button alignment on mobile devices"

### Amend
Modifying the last commit (before pushing).

**Example**: `git commit --amend` to fix a typo in the last commit.

### Revert
Creating a new commit that undoes the changes of a previous commit.

**Example**: Creating a new commit to undo a bug introduced earlier.

### Reset
Moving HEAD to a different commit, optionally discarding changes.

**Example**: `git reset --hard HEAD~1` undoes the last commit and discards changes.

## Branching Terms

### Main/Master Branch
The primary branch, usually representing production-ready code.

**Example**: `main` (modern standard) or `master` (older convention).

### Feature Branch
A branch created to develop a new feature.

**Example**: `feature/user-authentication`, `feature/payment-system`.

### Release Branch
A branch prepared for a new release.

**Example**: `release/v1.2.0`.

### Hotfix Branch
A branch for urgent bug fixes in production.

**Example**: `hotfix/critical-security-issue`.

### Detached HEAD State
When HEAD points directly to a commit instead of a branch.

**Example**: After checking out a specific commit or tag.

## Advanced Terms

### Reflog
Reference log - history of all your local Git actions, even deleted commits.

**Example**: `git reflog` shows everything you've done, useful for recovery.

### Hook
An automated script that runs at specific Git events.

**Example**: Pre-commit hook runs tests before allowing a commit.

### Submodule
A Git repository nested inside another Git repository.

**Example**: Including a library as a submodule in your project.

### Bisect
A binary search technique to find which commit introduced a bug.

**Example**: Git automatically narrows down which commit broke the code.

### Worktree
Multiple working directories for the same repository.

**Example**: Working on two branches simultaneously in different directories.

### Squash
Combining multiple commits into one during merge or rebase.

**Example**: Before merging, squashing 5 commits into 1 clean commit.

## File States Diagram

```
┌─────────────────────────────────────────────────────────┐
│                   WORKING DIRECTORY                      │
│                  (Local Files)                           │
└────────────────────┬────────────────────────────────────┘
                     │ git add
                     ▼
┌─────────────────────────────────────────────────────────┐
│                   STAGING AREA                           │
│                   (Index)                                │
└────────────────────┬────────────────────────────────────┘
                     │ git commit
                     ▼
┌─────────────────────────────────────────────────────────┐
│              LOCAL REPOSITORY                            │
│              (.git Directory)                            │
└────────────────────┬────────────────────────────────────┘
                     │ git push
                     ▼
┌─────────────────────────────────────────────────────────┐
│              REMOTE REPOSITORY                           │
│              (GitHub/GitLab)                             │
└─────────────────────────────────────────────────────────┘
```

## Common Workflow Terms

### Feature Branch Workflow
1. Create feature branch from main
2. Make commits on feature branch
3. Create pull request
4. Code review and discussion
5. Merge to main

### Gitflow Workflow
Multiple long-lived branches: `main`, `develop`, `feature/*`, `release/*`, `hotfix/*`

### Forking Workflow
Fork → Clone → Branch → Push → PR workflow for open-source projects

### Trunk-Based Development
Most work happens on main branch with short-lived feature branches

---

**Master this glossary and you'll understand Git conversations easily!**
