---
title: Git Branching6-Cherry-Picking Commits
date: '2025-10-27T12:07:50+08:00'
tags:
  - git
  - branching
---
 >**Objective:** Learn how to apply specific commits from one branch to another using cherry-picking.   
## 1. **Find the Commit Hash to Cherry-Pick**   
- Use `git log` to find the hash of the commit you want to cherry-pick.   
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
## 2. **Cherry-Pick the Commit**   
```bash
git cherry-pick <commit-hash>
```
- Example:   
	```bash
	git cherry-pick abcdef1234567890abcdef1234567890abcdef12
	```
    - You can also use a shortened version of the hash (usually the first 7 characters), as long as it is unique enough to identify the commit.   
	- Example of shortened hash:   
		```bash
		git cherry-pick abcdef1
		```
    - This command applies the changes from the specified commit to your current branch.   

---
## 3. **Resolve Conflicts (if any)**   
- If conflicts arise during the cherry-pick, Git will notify you. Resolve conflicts manually, then add and commit the resolved changes.   
```bash
git add <file-with-conflicts>
git cherry-pick --continue
```
---
## **Scenario**
### **Problem:**
You need to apply a specific commit from `feature-branch` to your `release` branch. The commit hash is `abcdef1234567890abcdef1234567890abcdef12`, but you encounter conflicts. How do you resolve this?   
