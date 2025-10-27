---
title: Git Branching1-Getting Started
date: '2025-10-27T14:06:50+08:00'
tags:
  - git
  - branching
---
>**Objective:** Understand the basics of creating and switching branches.   
## 1. **List All Branches** 
```bash
git branch 
```
	
---
## 2. **Create a New Branch**   
```bash
git branch <branch-name>
```
- Example:   
```bash
git branch feature-branch
```

---
## 3. **Switch to a Branch**   
```bash
git checkout <branch-name>
```
- Example:   
```bash
git checkout feature-branch
```
   
---
## **Quiz**
### Scenario: Implementing a New Feature Based on the Latest Development Branch:
You need to implement a new feature but must ensure that it is developed based on the latest `development` branch. How do you create a new branch named `new-feature`?   
### Solution   

To create a new branch named `new-feature`, first ensure you are on the latest development branch by using `git checkout main`
(assuming `main` is your main development branch), then create the new branch using `git branch new-feature`