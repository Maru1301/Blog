---
title: Git Branching3-Merging and Deleting Branches
date: '2025-10-27T15:06:50+08:00'
tags:
  - git
  - branching
---
 >**Objective:** Learn how to merge changes from one branch into another and manage branches.   
## 1. **Merge a Branch into the Current Branch**   
```bash
git merge <branch-name>
```
- Example:   
	```bash
	git merge new-feature
	```

---
## 2. **Delete a Branch Locally**   
```bash
git branch -d <branch-name>
```
- Example:   
	```bash
	git branch -d new-feature
	```

---
## **Scenario**
### **Problem 1:**
You’ve made several changes in the `feature-update` branch and committed them. Now, you realize that the changes also need to be tested in a separate branch called `qa-test`. How do you ensure the `qa-test` branch has the latest changes from `feature-update` without losing any commits, and then switch back to the `main` branch?   
### **Problem 2:**
You need to merge `bugfix-2024` into `release` and then delete the `bugfix-2024` branch, but `bugfix-2024` has some unmerged commits. How do you handle this situation?   

---
## More About Merge   
[Ex. Squash Merge vs Base Merge](/posts/git-branching/git-branching-ex-squash-merge-vs-base-merge/)    
   
