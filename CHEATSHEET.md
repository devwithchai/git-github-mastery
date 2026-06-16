# Git & GitHub Cheat Sheet

Quick reference for the most common Git and GitHub commands.

## 🔧 Basic Setup

```bash
# Configure git (one-time)
git config --global user.name "Your Name"
git config --global user.email "your@email.com"

# Check configuration
git config --list
```

## 📁 Local Repository

```bash
# Initialize a new repository
git init

# Clone an existing repository
git clone <url>
git clone <url> <directory>  # Clone to specific directory

# Check status
git status
git status -s  # Short format

# View changes
git diff                      # Unstaged changes
git diff --staged            # Staged changes
git diff <commit1> <commit2> # Between commits
```

## 📝 Staging & Committing

```bash
# Add files to staging area
git add <file>
git add *.py               # Add all Python files
git add .                  # Add all changes

# Remove from staging
git reset <file>
git reset                  # Unstage all

# Commit changes
git commit -m "message"
git commit -am "message"   # Stage and commit tracked files
git commit --amend         # Modify last commit

# View commit history
git log
git log --oneline          # One line per commit
git log --graph --oneline --all  # Visual graph
git log -p                 # Show changes
git log -n 5               # Last 5 commits
git log --author="name"    # By author
git log --grep="pattern"   # Search message
git log --since="2 weeks ago"
```

## 🌿 Branching

```bash
# List branches
git branch
git branch -a              # Include remote branches
git branch -v              # With last commit

# Create branch
git branch <branch-name>

# Switch branch
git checkout <branch-name>
git switch <branch-name>   # Modern syntax

# Create and switch
git checkout -b <branch-name>
git switch -c <branch-name>

# Delete branch
git branch -d <branch-name>      # Safe delete (merged only)
git branch -D <branch-name>      # Force delete

# Rename branch
git branch -m <old-name> <new-name>
git branch -m <new-name>  # Rename current branch

# Set upstream
git branch -u origin/<branch>
git branch --set-upstream-to=origin/<branch>
```

## 🔀 Merging & Rebasing

```bash
# Merge branch
git merge <branch-name>

# Abort merge
git merge --abort

# Rebase branch
git rebase <branch-name>

# Interactive rebase
git rebase -i HEAD~3       # Last 3 commits
git rebase -i <commit>     # Up to specific commit

# Abort rebase
git rebase --abort

# Continue rebase after resolving
git rebase --continue
```

## 📤 Remote Operations

```bash
# List remotes
git remote
git remote -v              # With URLs

# Add remote
git remote add <name> <url>

# Remove remote
git remote remove <name>

# Rename remote
git remote rename <old> <new>

# Show remote details
git remote show <name>

# Push to remote
git push
git push <remote> <branch>
git push -u origin <branch>      # Set upstream
git push --all                    # All branches
git push --tags                   # All tags

# Pull from remote
git pull
git pull <remote> <branch>

# Fetch from remote (no merge)
git fetch
git fetch <remote>
git fetch --all

# Push tags
git push origin <tag-name>
git push origin --tags
```

## 🔄 Undoing Changes

```bash
# Discard changes in working directory
git checkout <file>
git restore <file>         # Modern syntax

# Unstage file
git reset <file>
git restore --staged <file>

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Revert a commit (create new commit)
git revert <commit>

# See what was lost
git reflog

# Recover lost commit
git reset --hard <commit>
```

## 🏷️ Tags

```bash
# List tags
git tag
git tag -l "v*"            # Pattern matching

# Create tag
git tag <tag-name>                    # Lightweight
git tag -a <tag-name> -m "message"   # Annotated

# Delete tag
git tag -d <tag-name>
git push origin --delete <tag-name>   # Remote

# Push tag
git push origin <tag-name>
git push origin --tags

# Checkout tag
git checkout <tag-name>
```

## 🔗 Stashing

```bash
# Stash changes
git stash
git stash save "description"

# List stashes
git stash list

# Apply stash
git stash apply
git stash apply stash@{0}   # Specific stash

# Apply and remove
git stash pop

# Remove stash
git stash drop
git stash drop stash@{0}
git stash clear             # All stashes

# Show stash changes
git stash show
git stash show -p           # With diff
```

## 🎯 Cherry-picking

```bash
# Apply specific commit
git cherry-pick <commit>

# Multiple commits
git cherry-pick <commit1> <commit2>

# Range of commits
git cherry-pick <commit1>..<commit2>

# Abort cherry-pick
git cherry-pick --abort

# Continue after resolving
git cherry-pick --continue
```

## 🔍 Searching & Inspection

```bash
# Search for text in commits
git log -S "text"

# Search in specific file
git log <file>

# Show file history
git log -p <file>

# Show blame (who changed what)
git blame <file>

# Show commit info
git show <commit>
git show <commit>:<file>

# Diff between branches
git diff <branch1> <branch2>
```

## 🐛 Debugging

```bash
# Find bug with binary search
git bisect start
git bisect bad HEAD         # Current is bad
git bisect good <commit>    # Known good commit
# Test commits, mark as good/bad
git bisect reset            # Exit bisect

# See reflog (all actions)
git reflog

# See what HEAD was pointing to
git reflog show
```

## 🌐 GitHub-Specific Commands

```bash
# Fork a repository (via GitHub UI)
# Then clone YOUR fork:
git clone https://github.com/YOUR-USERNAME/repository.git

# Add upstream remote
git remote add upstream https://github.com/ORIGINAL-OWNER/repository.git

# Sync with upstream
git fetch upstream
git rebase upstream/main

# Create pull request (via GitHub UI after push)

# Fetch PR locally
git fetch origin pull/PR_NUMBER/head:branch-name
git checkout branch-name
```

## 💡 Common Workflows

### Feature Branch Workflow
```bash
git checkout -b feature/my-feature
# Make changes
git add .
git commit -m "Add feature"
git push -u origin feature/my-feature
# Create PR on GitHub
```

### Sync Fork with Upstream
```bash
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

### Rebase Instead of Merge
```bash
git fetch origin
git rebase origin/main
git push -f origin my-branch  # Force push after rebase
```

### Squash Commits Before Merge
```bash
git rebase -i HEAD~3          # Last 3 commits
# Mark commits as 'squash' or 's'
git push -f origin branch-name
```

### Undo Public Commit
```bash
git revert <commit>           # Creates new commit undoing changes
git push origin main
```

## 📋 Useful Git Aliases

Add to `.gitconfig` for shortcuts:

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual 'log --graph --oneline --all'
```

Then use: `git st`, `git co`, etc.

## 🎓 Quick Tips

- **Always pull before push**: `git pull` → make changes → `git push`
- **Use meaningful commit messages**: Good messages help future you
- **Commit frequently**: Smaller, focused commits are easier to manage
- **Create branches for features**: Keep main branch stable
- **Review before committing**: `git diff` before `git commit`
- **Use .gitignore**: Prevent committing unwanted files
- **Back up important branches**: Push to GitHub regularly

## 🔗 Next Steps

- Explore [Git Documentation](https://git-scm.com/doc)
- Try [Interactive Git Tutorial](https://learngitbranching.js.org/)
- Practice with real projects

---

**Keep this handy! Reference it often while learning.**
