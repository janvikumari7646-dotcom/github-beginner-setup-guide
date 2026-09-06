# Git Commands Reference Guide

A quick reference for the most common Git commands you'll use as a beginner.

## Table of Contents
1. [Initial Setup](#initial-setup)
2. [Getting Started](#getting-started)
3. [Daily Workflow](#daily-workflow)
4. [Branching](#branching)
5. [Viewing History](#viewing-history)
6. [Undoing Changes](#undoing-changes)
7. [Remote Operations](#remote-operations)
8. [Collaboration](#collaboration)

---

## Initial Setup

### Configure Git
```bash
# Set your name (used in commits)
git config --global user.name "Your Name"

# Set your email (used in commits)
git config --global user.email "your.email@example.com"

# Set your default branch name
git config --global init.defaultBranch main

# View all settings
git config --global --list
```

### Set Up SSH
```bash
# Generate new SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"

# Test connection
ssh -T git@github.com
```

---

## Getting Started

### Create a New Repository

**Option 1: Start locally**
```bash
# Create new directory
mkdir my-project
cd my-project

# Initialize git repository
git init

# Create initial file
echo "# My Project" > README.md

# Add files to staging
git add README.md

# Create first commit
git commit -m "Initial commit"
```

**Option 2: Clone from GitHub**
```bash
# Clone a repository
git clone git@github.com:username/repository.git

# Navigate into project
cd repository
```

---

## Daily Workflow

### Check Status
```bash
# See what files changed
git status

# More concise output
git status -s
```

### Stage Changes
```bash
# Stage specific file
git add filename.txt

# Stage all changes
git add .

# Stage all Python files
git add *.py

# Interactive staging (choose what to add)
git add -i
```

### Commit Changes
```bash
# Commit with message
git commit -m "Add new feature"

# Commit all tracked files (skips staging)
git commit -am "Fix bug"

# Amend last commit (add changes without new commit)
git commit --amend

# Edit last commit message
git commit --amend -m "Better message"
```

### Push Changes
```bash
# Push to GitHub
git push origin main

# Push and set upstream (first time)
git push -u origin main

# Push all branches
git push --all

# Force push (use carefully!)
git push --force origin main
```

### Pull Changes
```bash
# Get latest changes
git pull origin main

# Fetch without merging
git fetch origin

# Merge after fetch
git merge origin/main
```

---

## Branching

### Create & Switch Branches
```bash
# Create new branch
git branch branch-name

# Create and switch to new branch
git checkout -b branch-name

# Modern syntax (Git 2.23+)
git switch -c branch-name

# Switch to existing branch
git checkout main

# Modern syntax
git switch main

# List all branches
git branch

# List branches with more info
git branch -v

# List remote branches
git branch -r
```

### Delete Branches
```bash
# Delete local branch
git branch -d branch-name

# Force delete (if not fully merged)
git branch -D branch-name

# Delete remote branch
git push origin --delete branch-name

# Delete remote branch (alternative)
git push origin :branch-name
```

### Rename Branch
```bash
# Rename current branch
git branch -m new-name

# Rename specific branch
git branch -m old-name new-name
```

### Merge Branches
```bash
# Switch to main first
git checkout main

# Merge another branch into main
git merge feature-branch

# Merge without fast-forward
git merge --no-ff feature-branch
```

---

## Viewing History

### View Commits
```bash
# See commit history
git log

# Show last 5 commits
git log -5

# Show one-line format
git log --oneline

# Show with graph (branches)
git log --graph --oneline --all

# Show commits by author
git log --author="name"

# Show commits with changes
git log -p

# Show commits on this branch but not main
git log main..current-branch
```

### View Differences
```bash
# Show unstaged changes
git diff

# Show staged changes
git diff --staged

# Show changes in specific file
git diff filename.txt

# Show changes between branches
git diff main..feature-branch

# Show changes in specific commit
git show commit-hash
```

### View Specific Commit
```bash
# Show specific commit details
git show commit-hash

# Show file at specific commit
git show commit-hash:path/to/file
```

---

## Undoing Changes

### Discard Changes
```bash
# Discard changes in working directory
git checkout -- filename.txt

# Modern syntax
git restore filename.txt

# Discard all changes
git checkout -- .

# Modern syntax for all files
git restore .
```

### Unstage Changes
```bash
# Remove file from staging
git reset filename.txt

# Remove all from staging
git reset

# Modern syntax
git restore --staged filename.txt
```

### Undo Commits
```bash
# Create new commit that undoes changes
git revert commit-hash

# Move HEAD to specific commit (keep changes)
git reset --soft commit-hash

# Move HEAD and discard changes
git reset --hard commit-hash

# Temporarily save and restore work (stash)
git stash

# List stashed changes
git stash list

# Apply stashed changes
git stash apply

# Apply and remove stashed changes
git stash pop
```

### Fix Recent Commits
```bash
# Undo last commit, keep changes staged
git reset --soft HEAD~1

# Undo last commit, keep changes unstaged
git reset HEAD~1

# Undo last commit, discard changes
git reset --hard HEAD~1

# Change last commit message
git commit --amend -m "New message"
```

---

## Remote Operations

### Manage Remotes
```bash
# Show all remotes
git remote

# Show remote URLs
git remote -v

# Add new remote
git remote add name url

# Remove remote
git remote remove name

# Rename remote
git remote rename old new

# Change remote URL
git remote set-url origin new-url

# View remote details
git remote show origin
```

### Fetch & Pull
```bash
# Download without merging
git fetch origin

# Fetch all remotes
git fetch --all

# Download and merge (combines fetch + merge)
git pull origin main

# Pull with rebase instead of merge
git pull --rebase origin main
```

### Push
```bash
# Push branch to remote
git push origin branch-name

# Push and set upstream
git push -u origin branch-name

# Push all branches
git push --all

# Push all tags
git push --tags

# Delete remote branch
git push origin --delete branch-name
```

---

## Collaboration

### Fork & Contribute
```bash
# Clone your fork
git clone git@github.com:your-username/forked-repo.git

# Add upstream (original repo)
git remote add upstream git@github.com:original-owner/repo.git

# Fetch from upstream
git fetch upstream

# Sync your fork with upstream
git checkout main
git merge upstream/main

# Push to your fork
git push origin main
```

### Create Pull Request (via GitHub website)
```bash
# Create feature branch
git checkout -b feature/my-feature

# Make changes
# git add .
# git commit -m "Add feature"

# Push branch
git push origin feature/my-feature

# Go to GitHub and click "Create Pull Request"
```

### Review Changes
```bash
# See what changed in pull request
git diff main..feature-branch

# See all files changed
git diff --name-only main..feature-branch

# View specific file changes
git diff main..feature-branch -- path/to/file
```

---

## Advanced Tips

### Search Commits
```bash
# Search for commit by message
git log --grep="keyword"

# Search for code in commits
git log -S "code snippet"

# Search by author
git log --author="name"
```

### Rebase (Advanced)
```bash
# Rebase current branch on main
git rebase main

# Interactive rebase (edit, squash commits)
git rebase -i HEAD~3

# Continue after resolving conflicts
git rebase --continue

# Abort rebase
git rebase --abort
```

### Clean Up
```bash
# Remove untracked files (dry run first)
git clean -n

# Remove untracked files
git clean -f

# Remove untracked directories
git clean -fd

# Prune deleted remote branches
git fetch --prune
```

---

## Quick Reference Cheat Sheet

| Task | Command |
|------|---------|
| Check status | `git status` |
| Stage all | `git add .` |
| Commit | `git commit -m "message"` |
| Push | `git push origin main` |
| Pull | `git pull origin main` |
| Create branch | `git checkout -b branch-name` |
| Switch branch | `git checkout branch-name` |
| View history | `git log --oneline` |
| View diff | `git diff` |
| Undo changes | `git checkout -- file` |
| Merge branch | `git merge branch-name` |
| Delete branch | `git branch -d branch-name` |
| Stash changes | `git stash` |
| Apply stash | `git stash pop` |
| View remotes | `git remote -v` |

---

## Common Mistakes & Solutions

### Committed to wrong branch?
```bash
# Create branch from current commit
git branch feature-branch
# Reset main to previous state
git reset --hard HEAD~1
# Switch to feature-branch
git checkout feature-branch
```

### Pushed sensitive data?
```bash
# Remove file from history (careful!)
git filter-branch --tree-filter 'rm -f secret.txt' HEAD
git push --force-with-lease
```

### Large file committed?
```bash
# Remove from last commit
git reset HEAD~1
# Remove file
git rm large-file.zip
# Commit again
git commit -m "Removed large file"
```

### Merge conflict?
```bash
# After seeing conflicts in editor:
git add resolved-file.txt
git commit -m "Resolve merge conflicts"
# Or abort merge
git merge --abort
```

---

## Resources

- [Git Official Documentation](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [Interactive Learning](https://learngitbranching.js.org)

---

**Master these commands and you'll be a Git pro in no time! 🚀**
