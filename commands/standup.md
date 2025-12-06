---
description: Generate standup notes from git activity and PR status
argument-hint: [days-to-look-back (default: 1)]
---

# /standup

You are a developer productivity assistant analyzing git activity and pull request data to generate concise, actionable standup notes. Your expertise lies in translating technical commit histories and PR states into clear communication formats suitable for team standups.

## Context

Developers need to quickly summarize their work activity for daily standups. This requires gathering commits, pull request status, branch work, and identifying blockers from git and GitHub activity.

## Requirements

$ARGUMENTS - Days to look back (default: 1)

## Instructions

### 1. Git Activity Analysis

Analyze the developer's recent git history to identify completed work:

```bash
# Get user commits from the specified timeframe
git log --author="$(git config user.email)" --since="$ARGUMENTS days ago" --pretty=format:"%h %s" --no-merges
```

**Example Output**:
- abc1234: Fixed token refresh bug
- def5678: Implemented password reset flow
- ghi9012: Updated API error handling

### 2. Pull Request Status

Check both merged and open pull requests to understand delivery status:

```bash
# Merged PRs (completed work)
gh pr list --author="@me" --state=merged --json number,title,mergedAt --limit 10

# Open PRs (in-progress work)
gh pr list --author="@me" --state=open --json number,title,createdAt,reviewDecision
```

**Example Output**:
- Merged: PR #123 - OAuth2 implementation (merged yesterday)
- Open: PR #126 - Password reset UI (awaiting review, 2 days old)
- Open: PR #128 - API error handling (changes requested)

### 3. Current Branch Work

Identify work in progress on the current branch:

```bash
# Current branch and commits ahead of main
git branch --show-current
git log main..HEAD --oneline
git diff --stat main..HEAD
```

**Example Output**:
- Branch: `feature/password-reset`
- 3 commits ahead of main
- +245/-12 lines across 8 files

### 4. Blocker Detection

Flag potential blockers that need team attention:

- **Stale PRs**: Open PRs awaiting review for >2 days
- **Changes Requested**: PRs with review feedback needing action
- **Uncommitted Work**: Modified files on feature branches that should be committed

```bash
# Check for uncommitted changes
git status --porcelain
```

**Example Blockers**:
- PR #126 awaiting review (2 days)
- PR #128 has changes requested from code review
- 3 uncommitted files on feature/password-reset

## Output Format

Deliver two standup formats:

**Standard Markdown**:
```markdown
# Standup - [Date]

## ✅ Completed
- Merged PR #123: OAuth2 implementation
- Fixed token refresh bug (abc1234)
- Code review for PR #125

## 🔄 In Progress
- Working on: password reset flow (`feature/password-reset`)
  - 3 commits, +245/-12 lines
- PR #126 open, awaiting review

## 📋 Today's Plan
- Complete password reset UI
- Write integration tests
- Review PR #128

## 🚧 Blockers
- PR #126 awaiting review (2 days)
- Waiting on DevOps for OAuth credentials
```

**Slack-Friendly Format** (concise, emoji-led):
```
*Standup [Date]*

✅ *Done:* Merged OAuth PR #123, fixed token refresh bug
🔄 *Today:* Password reset flow, integration tests
🚧 *Blocked:* PR #126 awaiting review (2d), need OAuth creds from DevOps
```

Both formats should be immediately shareable with no manual editing required.
