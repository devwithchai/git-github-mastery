# Real-World Scenario 3: Emergency Hotfix

## Scenario Overview

A critical bug has been found in production code. You need to:
1. Fix it immediately
2. Deploy to production
3. Merge back to all branches
4. Maintain code consistency

**Situation:**
- Bug discovered: Payment processing returns wrong amount
- Impact: High (production issue)
- Timeline: Must be fixed NOW
- User base: Thousands affected

## Step-by-Step Workflow

### Step 1: Create Hotfix Branch from Main

```bash
# Make sure you're up to date
git fetch origin

# Create hotfix branch from main (production)
git checkout -b hotfix/payment-calculation main

# Verify you're on the hotfix branch
git branch
# Should show: * hotfix/payment-calculation
```

### Step 2: Identify and Fix the Bug

```bash
# Find the bug
cat src/payment.py

# Bug found: Wrong multiplication formula
# Before: amount = price * quantity / 100  (WRONG!)
# After: amount = price * quantity / 100.0 (CORRECT!)

# Make the minimal fix (ONLY the bug, nothing else)
sed -i 's/\/ 100 / \/ 100.0 /' src/payment.py

# Verify the fix
cat src/payment.py
```

### Step 3: Test Thoroughly

```bash
# Run the full test suite
python -m pytest tests/ -v

# Run specific payment tests
python -m pytest tests/test_payment.py -v

# Manual testing
python -c "from src.payment import calculate; print(calculate(10.50, 2))"

# All tests MUST pass
```

### Step 4: Commit with Clear Message

```bash
# Commit with urgent, clear message
git add src/payment.py
git commit -m "hotfix: Fix critical payment calculation bug

Payment amounts were being incorrectly calculated due to
integer division. This fix ensures floating-point division
for accurate payment calculations.

This is a critical production fix that must be deployed
immediately.

Impact: All payment transactions
Severity: Critical"
```

### Step 5: Push to GitHub

```bash
# Push the hotfix branch
git push -u origin hotfix/payment-calculation
```

### Step 6: Create Urgent PR

1. Go to GitHub
2. Create PR with:
   ```
   ## 🚨 CRITICAL HOTFIX 🚨
   
   **Issue**: Payment calculation bug in production
   **Impact**: All payments are calculated incorrectly
   **Severity**: CRITICAL
   **Action Required**: Immediate approval and merge
   
   ## What's Fixed
   - Fixed integer division bug in payment calculation
   - Verified with full test suite
   - Ready for immediate production deployment
   
   ## Deployment
   Deploy to production immediately after merge.
   ```

3. Tag as urgent
4. Notify team in Slack/Discord
5. Request immediate review

### Step 7: Fast-Track Approval

```bash
# In emergency situations:
# - Request immediate review from on-call engineer
# - May bypass some normal review processes
# - Ensure at least one approval
# - Test in staging if possible
```

### Step 8: Merge to Main

```bash
# On GitHub, merge the PR immediately
# (Team lead or authorized person)

# After merge, verify
git checkout main
git pull origin main
git log --oneline -n 3
```

### Step 9: Deploy to Production

```bash
# Create deployment (your process may differ)
# 1. Build
# 2. Test in staging
# 3. Deploy to production
# 4. Monitor for issues
# 5. Verify fix worked

# In your CI/CD system:
# Push to main → Automatic build → Deploy to production
```

### Step 10: Merge Back to Develop

```bash
# Hotfix must also go to develop branch
git checkout develop
git pull origin develop

# Merge the hotfix
git merge hotfix/payment-calculation

# Push back
git push origin develop

# Or create a PR so team knows about the fix
```

### Step 11: Document and Communicate

```bash
# Create a post-mortem documentation
cat > INCIDENT_REPORT.md << 'EOF'
# Payment Bug Incident Report

## Timeline
- 2024-06-16 14:30 - Bug discovered
- 2024-06-16 14:45 - Fix implemented
- 2024-06-16 15:00 - Merged to main
- 2024-06-16 15:15 - Deployed to production
- 2024-06-16 15:30 - Verified fix working

## Root Cause
Integer division in payment calculation causing rounding errors.

## Solution
Changed to floating-point division for accurate calculations.

## Prevention
Add unit tests for edge cases in payment calculations.

## Follow-up
1. Review all payment-related code for similar issues
2. Add integration tests for payment processing
3. Implement automated monitoring for payment anomalies
EOF

# Commit this documentation
git add INCIDENT_REPORT.md
git commit -m "docs: Add incident report for payment bug hotfix"
git push origin main
```

### Step 12: Cleanup

```bash
# Delete the hotfix branch locally
git branch -d hotfix/payment-calculation

# Delete on GitHub
git push origin --delete hotfix/payment-calculation

# All branches now have the fix
```

## Emergency Hotfix Checklist

- [ ] Created hotfix branch from main
- [ ] Fixed ONLY the bug (no other changes)
- [ ] All tests pass
- [ ] Clear, urgent commit message
- [ ] Pushed to GitHub
- [ ] Created urgent PR
- [ ] Notified team
- [ ] Approved and merged to main
- [ ] Deployed to production
- [ ] Verified fix working in production
- [ ] Merged back to develop
- [ ] Created incident report
- [ ] Planned follow-up improvements
- [ ] Cleaned up hotfix branch

## Key Principles for Hotfixes

✅ **Speed**: Fix it fast, communication happens in parallel  
✅ **Minimalism**: Only fix the bug, don't refactor  
✅ **Testing**: Verify the fix works (fast, targeted tests)  
✅ **Communication**: Notify team immediately  
✅ **Deployment**: Push to production as soon as approved  
✅ **Verification**: Confirm fix actually works  
✅ **Merge Back**: Get fix into all branches  
✅ **Documentation**: Record what happened and why  
✅ **Prevention**: Learn and improve processes  
✅ **Post-Mortem**: Discuss how to prevent similar issues  

## Common Pitfalls to Avoid

❌ Don't add unrelated changes to hotfixes  
❌ Don't skip testing, even under pressure  
❌ Don't forget to merge back to develop  
❌ Don't make hotfixes without team knowledge  
❌ Don't deploy without verification  

## Learning from Incidents

After handling the emergency:

1. **Blameless Post-Mortem**: Discuss what happened without blame
2. **Root Cause Analysis**: Why did this bug exist?
3. **Process Improvements**: How to prevent next time?
4. **Code Review**: Could this have been caught earlier?
5. **Testing**: What tests would have caught this?
6. **Monitoring**: How can we detect this faster?

---

## Congratulations!

You've now seen practical real-world Git workflows:
- ✅ Scenario 1: Team development
- ✅ Scenario 2: Open source contribution
- ✅ Scenario 3: Emergency response

You're ready for production Git usage!
