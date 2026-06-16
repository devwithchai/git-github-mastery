# Exercise 1: Repository Setup

## Objective
Set up your first Git repository and understand the basic configuration.

## Steps

### Step 1: Create a Project Directory
```bash
mkdir git-practice-1
cd git-practice-1
```

### Step 2: Initialize Git Repository
```bash
git init
```

You should see: `Initialized empty Git repository in /path/to/git-practice-1/.git/`

### Step 3: Configure Git (Local to this repo)
```bash
git config user.name "Your Name"
git config user.email "your.email@example.com"
```

### Step 4: Verify Configuration
```bash
git config --list
```

Look for your name and email in the output.

### Step 5: Create Initial Files
```bash
echo "# My First Git Project" > README.md
echo "# TODO:" > TODO.md
```

### Step 6: Check Repository Status
```bash
git status
```

Expected output shows both files as "Untracked files".

## Verification Checklist
- [ ] `.git` directory exists in your project folder
- [ ] Git is initialized
- [ ] User name and email are configured
- [ ] Files appear in `git status` as untracked

## Common Issues

**Q: I see "fatal: not a git repository"**
A: Make sure you're in the correct directory and ran `git init`

**Q: Git says "Please tell me who you are"**
A: Run the config commands with your name and email

**Q: I want to configure globally (all repositories)**
A: Add `--global` flag:
```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```
