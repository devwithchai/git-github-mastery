# Module 4: Collaboration & Pull Requests 🤝

Master collaborative development with pull requests and code review.

## 🎯 Learning Objectives

By the end of this module, you will:
- ✅ Create and submit pull requests
- ✅ Review code professionally
- ✅ Request changes and suggest improvements
- ✅ Resolve merge conflicts in PRs
- ✅ Use PR discussions effectively
- ✅ Understand CI/CD in PRs
- ✅ Merge strategies

## 📖 Concepts

### 1. Pull Request (PR) Workflow

```
Local Branch          GitHub                Main
  ↓                    ↓                     ↓
Create Branch → Push Branch → Create PR → Review → Approve → Merge
```

### 2. PR Components
- **Title**: Brief description of changes
- **Description**: Detailed explanation
- **Commits**: All commits from the branch
- **Files Changed**: Diff view
- **Comments**: Discussion thread

### 3. Code Review Best Practices
- Review for correctness
- Check code style and conventions
- Suggest improvements
- Ask questions
- Be respectful and constructive

### 4. Handling Conflicts
When main has changed since you created your branch.

### 5. Merge Strategies
- **Create a merge commit**: Full history
- **Squash and merge**: Single commit
- **Rebase and merge**: Linear history

## 🔧 Hands-On Exercises

### Exercise 1: Creating Your First PR
**Goal**: Create and submit a pull request

**Prerequisites:** GitHub repository from Module 2

**Tasks:**
1. Create a feature branch:
   ```bash
   git checkout -b feature/documentation
   ```

2. Create or edit a file:
   ```bash
   echo "# Contributing\nWe welcome contributions!" > CONTRIBUTING.md
   ```

3. Commit:
   ```bash
   git add CONTRIBUTING.md
   git commit -m "Add contributing guidelines"
   ```

4. Push to GitHub:
   ```bash
   git push -u origin feature/documentation
   ```

5. Go to GitHub, you'll see a "Compare & pull request" button

6. Click it

7. Fill in PR details:
   - Title: "Add contributing guidelines"
   - Description: "Added CONTRIBUTING.md to help new contributors"

8. Create Pull Request

9. On GitHub, review your own PR (see the changes)

10. If it looks good, merge it (click "Merge pull request")

**Questions:**
- What information appears in the PR?
- How does GitHub show the diff?
- What happened to the branch after merging?

---

### Exercise 2: Reviewing a PR
**Goal**: Learn code review process

**Tasks:**
1. Ask a friend/partner to create a PR (or create another one yourself)

2. Go to the PR on GitHub

3. Click "Files changed" tab

4. Review the changes:
   - Hover over a line
   - Click the "+" button that appears
   - Leave a comment

5. Make a few comments:
   - Praise something good
   - Ask a question about the logic
   - Suggest an improvement

6. Go to "Conversation" tab

7. Request changes:
   - Click "Review changes"
   - Select "Request changes"
   - Add summary
   - Submit review

8. The author will see your review and respond

9. They make changes and push new commits

10. Review again and approve:
    - "Review changes" → "Approve"

11. After approval, merge the PR

**Questions:**
- How does GitHub track conversations?
- What's the difference between comments and requested changes?
- Can you approve PRs you wrote?

---

### Exercise 3: Resolving Merge Conflicts in PR
**Goal**: Handle conflicts in pull requests

**Prerequisites:** Two people or two branches

**Tasks:**
1. Have both branches modify the same file in the same place

2. Person A: Merge their PR first

3. Person B: Try to merge their PR

4. GitHub shows "Can't automatically merge"

5. Options to resolve:
   **Option A: Resolve on GitHub**
   - Click "Resolve conflicts"
   - Edit the file directly
   - Mark as resolved
   - Commit merge

   **Option B: Resolve locally**
   - In terminal:
   ```bash
   git fetch origin
   git merge origin/main
   ```
   - You'll see conflicts
   - Edit files to resolve
   - Commit the merge
   - Push

6. Merge the PR

**Questions:**
- When do merge conflicts occur?
- Is it easier to resolve on GitHub or locally?
- How do you know when a conflict is fully resolved?

---

### Exercise 4: Fixing a PR After Feedback
**Goal**: Respond to review feedback

**Tasks:**
1. Create a PR with some intentional "issues":
   ```bash
   git checkout -b feature/needs-review
   echo "var x = 1" > code.js  # Bad variable name
   git add . && git commit -m "Add code"
   git push -u origin feature/needs-review
   ```

2. Create the PR on GitHub

3. Review your own PR and request changes (or have someone else do it)

4. Make the requested changes locally:
   ```bash
   echo "var count = 1" > code.js
   git add . && git commit -m "Improve variable naming"
   git push
   ```

5. New commit automatically appears in PR

6. Respond to the review comments

7. Once satisfied, request approval

8. Merge when approved

**Questions:**
- Did new commits automatically update the PR?
- Can you edit old commits in a PR?
- How do you mark review comments as resolved?

---

### Exercise 5: PR Templates and Discussions
**Goal**: Professional PR practices

**Tasks:**
1. In your repo, create PR template:
   ```bash
   mkdir -p .github
   cat > .github/pull_request_template.md << 'EOF'
   ## Description
   Brief description of changes

   ## Type of Change
   - [ ] Bug fix
   - [ ] New feature
   - [ ] Documentation

   ## Testing
   How was this tested?

   ## Checklist
   - [ ] Code reviewed
   - [ ] Tests pass
   - [ ] Documentation updated
   EOF
   ```

2. Commit and push:
   ```bash
   git add .github/pull_request_template.md
   git commit -m "Add PR template"
   git push origin main
   ```

3. Now when you create a new PR, the template appears automatically

4. Create a PR using the template

5. Use PR for discussion:
   - Discuss approach
   - Explain decisions
   - Link to related issues

**Questions:**
- Why are PR templates useful?
- How does template make PRs clearer?
- What other GitHub templates exist?

---

## 🎓 Practice Scenario

### Scenario: Team Code Review

**Setup:**
1. Create a shared repository
2. Set up branch protection:
   - Settings → Branches → Add rule
   - Require PR reviews before merge
   - Require status checks to pass

3. Create branches for different features

4. Each person:
   - Creates PR
   - Reviews others' PRs
   - Requests changes
   - Responds to feedback
   - Merges when approved

5. Practice professional communication in PRs

---

## ✅ Self-Assessment

Before moving to Module 5, ensure you can:
- [ ] Create pull requests
- [ ] Write clear PR descriptions
- [ ] Review code professionally
- [ ] Request changes
- [ ] Approve PRs
- [ ] Resolve merge conflicts in PRs
- [ ] Respond to feedback
- [ ] Use PR discussions
- [ ] Set up branch protection rules
- [ ] Use PR templates

---

## 🔗 Resources

- [About Pull Requests](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests)
- [Creating a PR](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)
- [Reviewing PRs](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests)
- [Resolving Conflicts](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts)

---

## 📝 Next Steps

✅ **Completed Module 4?** Move to [Module 5: Advanced Git](../05-advanced-git/README.md)
