---
title: Git Branching4-Pushing and Pulling Branches
date: '2025-10-27T16:06:50+08:00'
tags:
  - git
  - branching
---
>**Objective:** Understand how to push branches to a remote repository and manage remote branches.   
## 1. **Push a Branch to Remote**   
```bash
git push origin <branch-name>
```
- Example:   
	```bash
	git push origin feature-branch
	```
    - Practice pushing your branch to a remote repository.   

---
## 2. **Track a Remote Branch Locally**   
```bash
git checkout --track origin/<branch-name>
```
- Example:   
	```bash
	git checkout --track origin/feature-branch
	```

---
## 3. **Pull Remote Changes into a Local Branch**   
```bash
git pull origin <branch-name>
```
- Example:   
	```bash
	git pull origin main
	```

---
## 4. **Pull Changes from One Remote Branch into Another Local Branch**   
```bash
git pull origin <source>:<destination>
```
- This command pulls changes from the `main` branch in the remote repository into the local `feature` branch.   
- Example:   
	```bash
	git pull origin main:feature
	```

---
## 5. **Push Changes from One Local Branch into Another Remote Branch**   
```bash
git push origin <source>:<destination>
```
- This command pushes changes from the local `main` branch to the `feature` branch in the remote repository.   
- Example:   
	```bash
	git push origin main:feature
	```
   
---
## **Scenario**
### **Problem:**
You need to update your local `qa-test` branch with the latest changes from the remote `main` branch. After updating, you also want to push any new commits from `qa-test` back to a remote branch named `qa-test`. How do you accomplish this?   
## More About Push   
[Ex. Deleting a Remote Branch]({{< ref "/posts/git-branching/git-branching-ex-deleting-a-remote-branch" >}})    
