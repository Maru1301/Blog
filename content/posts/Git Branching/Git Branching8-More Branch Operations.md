---
title: Git Branching8-More Branch Operations
date: '2025-10-27T11:06:50+08:00'
tags:
  - git
  - branching
---
>**Objective:** Gain confidence in more complex branch operations.   
## 1. **Rename a Branch**   
```bash
git branch -m <new-branch-name>
```
- Example:   
	```bash
	git branch -m renamed-branch
	```

---
## 2. **Delete a Remote Branch**   
```bash
git push origin --delete <branch-name>
```
- Example:   
	```bash
	git push origin --delete feature-branch
	```

---
## 3. **List Remote Branches**   
```bash
git branch -r
```
   
   
