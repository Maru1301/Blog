---
title: Git Branching5-Moving Branches to Specific Commits
date: '2025-10-28T10:06:50+08:00'
tags:
  - git
  - branching
categories:
  - git-branching
weight: 50
---
>**Objective:** Learn how to move a branch to point to a specific commit.   
## 1. **Find the Commit Hash**   
- Use `git log` to find the hash of the commit you want to move the branch to.   
```bash
git log

```
- Example output (commit hash highlighted):   
    ```bash
	commit abcdef1234567890abcdef1234567890abcdef12
	Author: Your Name <you@example.com>
	Date:   Date
	
	    Commit message
	```

---
## 2. **Move a Branch to a Specific Commit**   
```bash
git branch -f <branch-name> <commit-hash>
```
- Example:   
	```bash
	git branch -f feature-branch abcdef1234567890abcdef1234567890abcdef12
	```
- This command forces the branch `<branch-name>` to point to `<commit-hash>`.   
- You can also use a shortened version of the hash (usually the first 7 characters), as long as it is unique enough to identify the commit.   
- Example of shortened hash:   
	```bash
	git branch -f feature-branch abcdef1
	```

---
## 3. **Checkout the Branch to Verify**   
```bash
git checkout <branch-name>
```
- Example:   
    ```bash
	git checkout feature-branch
	```
    - Verify that the branch is now pointing to the specified commit.   

---
## **Scenario**
### **Problem:**
You have a branch `hotfix` that needs to be moved to a previous commit to reapply specific fixes. After moving it, you need to ensure the branch is tested and merged back into `main`. What are the steps involved?   
