# Exercise 1: Solution

## Expected Output

### After `git init`
```
Initialized empty Git repository in /path/to/git-practice-1/.git/
```

### After `git config user.name "Your Name"`
```
(No output - it's just setting configuration)
```

### After `git config --list`
```
user.name=Your Name
user.email=your.email@example.com
... (other configurations)
```

### After `git status`
```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md
        TODO.md

nothing added to commit but untracked files present (tracking what will be committed)
```

## Key Concepts

1. **Repository Initialization**: `git init` creates the `.git` directory
2. **Configuration**: Git needs to know who you are for commits
3. **Untracked Files**: Git sees them but isn't tracking changes yet
4. **Current Branch**: "main" is the default branch

## Next Steps

Continue to Exercise 2 to stage and commit these files.
