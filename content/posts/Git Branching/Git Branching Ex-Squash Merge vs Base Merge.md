---
title: Git Branching Ex-Squash Merge vs Base Merge
date: '2025-09-26T11:19:50+08:00'
tags:
  - git
  - branching
---
When working with Git, merging is a crucial part of integrating changes from different branches. Two common types of merges are **squash merge** and **base (regular) merge**. Each has its own use cases and implications for your commit history.
## Base (Regular) Merge
A regular merge takes the contents of a source branch and integrates them into the target branch. This type of merge creates a merge commit that includes all the changes from the source branch, preserving the commit history.
### Characteristics:
- **Preserves Commit History:** All commits from the source branch are preserved and visible in the commit history.
- **Creates a Merge Commit:** A new commit is created to represent the merge, indicating the point where the branches were combined.
### Commands:
```bash
# Switch to the target branch
git checkout main

# Merge the feature branch into the target branch
git merge feature-branch

```
### Example:
```
main:     A---B---C-------E
              \         /
feature:       D---F---G

```
Here, `E` is the merge commit.
## Squash Merge
A squash merge combines all the changes from the source branch into a single commit and then merges that commit into the target branch. This method does not preserve the individual commit history from the source branch.
### Characteristics:
- **Combines Commits:** All commits from the source branch are combined into a single commit.   
- **Simplifies History:** The commit history is simpler and cleaner, with only one commit representing all the changes from the source branch.
### Commands:
```bash
# Switch to the target branch
git checkout main

# Squash and merge the feature branch into the target branch
git merge --squash feature-branch

# Commit the changes after squashing
git commit -m "Squashed commit from feature-branch"

```
### Example:
```
main:     A---B---C---E
              \
feature:       D---F---G

```
Here, `E` is the single commit representing all the changes from the `feature-branch`.
## Comparison

|         Aspect |                                                     Base Merge |                                                              Squash Merge |
|:---------------|:---------------------------------------------------------------|:--------------------------------------------------------------------------|
| Commit History |                               Preserves all individual commits | Combines all changes into a single commit, resulting in a simpler history |
|   Merge Commit |                                         Creates a merge commit |   No merge commit; a single squashed commit is added to the target branch |
|   Traceability | Easier to trace the development history and individual changes |       Harder to trace individual changes but results in a cleaner history |
## Use Cases
- **Base (Regular) Merge:**
    - When you want to preserve the detailed commit history.
    - Useful for large teams where individual contributions need to be tracked.
    - When you need to maintain the context of each change.
- **Squash Merge:**
    - When you prefer a clean and simplified commit history.
    - Suitable for small, well-defined features or bug fixes.
    - Ideal for repositories where keeping history concise is more important than individual commit details.
