---
title: Git Branching2-Working with Branches
date: '2025-10-27T13:06:50+08:00'
tags:
  - git
  - branching
---
>**Objective:** Make changes in branches and understand basic workflows.   
## 1. **Create and Switch to a New Branch**   
```bash
git checkout -b <branch-name>
```
- Example:   
	```bash
	git checkout -b new-feature
	```

---
## 2. **Make Changes and Commit**   
- Make some changes to files in your working directory.   
- Add changes to the staging area:   
	```bash
	git add .
	```
- Commit the changes:   
	```bash
	git commit -m "Add new feature"
	```

---
## 3. **Switch Back to the Main Branch**   
```bash
git checkout main
```
