---
title: Git Branching7-Rebasing Branches
date: '2025-10-27T12:06:50+08:00'
tags:
  - git
  - branching
---
 >**Objective:** Understand how to rebase branches to integrate changes and maintain a cleaner commit history.

>**Intro**: Rebasing in Git is a process that allows you to move or combine a sequence of commits to a new base commit.   
## 1. **Rebase a Branch onto Another Branch**   
- Switch to the branch you want to rebase:   
	```bash
	git checkout <branch-to-rebase>
	```
- Example:   
	```bash
	git checkout feature-branch	
	```
- Rebase the current branch onto another branch (e.g., `main`):   
	```bash
	git rebase <target-branch>
	```
- Example:   
	```bash
	git rebase main
	```
- This moves the entire branch to start from the tip of `<target-branch>`, replaying your commits on top of it.   

---
## 2. **Resolve Conflicts During Rebase**   
- If conflicts arise during the rebase, Git will pause and prompt you to resolve them.   
- Resolve conflicts manually, then add the resolved files:   
	```bash
	git add <file-with-conflicts>
	```
- Continue the rebase process:   
	```bash
	git rebase --continue
	```

---
## 3. **Abort a Rebase (if necessary)**   
- If you want to stop the rebase process and return to the original state, use:   
	```bash
	git rebase --abort

	```
- This will cancel the rebase and restore your branch to its previous state.   

---
## 4. **Interactive Rebase**   
- For advanced manipulation of commits, you can use interactive rebase:   
	```bash
	git rebase -i <base-commit>
	```
- Example:   
	```bash
	git rebase -i HEAD~3
	```
- This opens an editor where you can reorder, squash, or edit commits. Follow the instructions in the editor to modify commits.   

---
## 5. **Rebasing vs. Merging**   
- Rebasing rewrites history by applying your changes on top of another branch, resulting in a linear commit history.   
- Merging combines changes from different branches without rewriting history, which can create a merge commit.   

---
## **Scenario**
### **Problem:**
You need to rebase `feature-branch` onto the latest `main` branch. During the rebase, you encounter multiple conflicts. After resolving conflicts, you also want to squash the last two commits in `feature-branch` into a single commit before finalizing the rebase. How do you proceed?   
## More About Rebase   
[Ex. Deep Dive into Rebase](Ex.%20Deep%20Dive%20into%20Rebase.md)    
