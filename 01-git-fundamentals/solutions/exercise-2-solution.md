# Exercise 2: Solution

## Expected Workflow

### Initial Status
```
Untracked files:
  app.py
  .env
  .gitignore
  README.md
  TODO.md
```

### After Staging README and .gitignore
```
Changes to be committed:
  new file:   README.md
  new file:   .gitignore

Untracked files:
  app.py
  .env
```

### After First Commit
```
log output:
commit abc123def456 (HEAD -> main)
Author: Your Name <your.email@example.com>
Date:   Mon Jun 16 10:30:00 2026 +0000

    Initial commit: Add README and gitignore
```

### After Final Commits
```
log --oneline output:
abc1234 Add application files
5678def Initial commit: Add README and gitignore
```

## Key Takeaways

1. **Selective Staging**: You don't have to commit everything at once
2. **Meaningful Commits**: Each commit should be a logical unit of work
3. **Clear Messages**: Good commit messages are crucial for history
4. **Staging Area Benefit**: Review what you're committing before finalizing

## Common Mistakes to Avoid

- ❌ Committing unrelated changes together
- ❌ Vague commit messages like "fix", "update"
- ✅ One logical feature or fix per commit
- ✅ Clear, present-tense messages

## Next Steps

Move to branching exercises to learn parallel development.
