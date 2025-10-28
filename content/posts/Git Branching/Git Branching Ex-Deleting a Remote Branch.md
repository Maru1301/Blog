---
title: Git Branching Ex-Deleting a Remote Branch
date: '2025-09-26T10:06:50+08:00'
tags:
  - git
  - branching
categories:
  - git-branching
weight: 100
---
>**Objective**: Learn how to delete a remote branch from your repository.   
### Brief Introduction to the Command:   
- **`git push <remote-name> --delete <branch-name>`**: This command deletes a specified branch from the remote repository. The `<remote-name>` is usually `origin` for the default remote repository, and `<branch-name>` is the name of the branch you want to delete.
### Steps:   
1. **Identify the Branch to Delete:**   
    - Make sure you know the exact name of the branch you want to delete. You can list all branches, including remote ones, with the command:   
	```bash
	git branch -a
	```
2. **Delete the Remote Branch:**   
    - Use the following command to delete the branch from the remote repository:   
		```bash
		git push <remote-name> --delete <branch-name>
		```
    - For example, if you want to delete a branch named `feature-branch` from the remote repository named `origin`:   
		```bash
		git push origin --delete feature-branch
		```
    - Shortened version:   
		```bash
		git push origin -d feature-branch
		```
1. **Verify the Deletion:**   
    - Fetch the latest state of the remote repository to update your local information about the remote branches:   
		```bash
		git fetch
		```
    - List the remote branches to ensure the branch has been deleted:   
		```bash
		git branch -r
		```
### Example Workflow:   
1. **List Remote Branches:**   
    ```bash
	git branch -r
	```
    - Output might look like:   
	    ```bash
		origin/HEAD -> origin/main
		origin/development
		origin/feature-branch
		origin/hotfix
		```
2. **Delete the Remote Branch:**   
    ```bash
	git push origin -d feature-branch
	```
    - This command will delete `feature-branch` from the remote repository.   
3. **Verify the Deletion:**   
    - Fetch the latest state of the remote repository:   
		```bash
		git fetch
		```
    - List the remote branches again:   
		```bash
		git branch -r
		```
    - Output should no longer include `origin/feature-branch`:   
		```bash
		origin/HEAD -> origin/main
		origin/development
		origin/hotfix
		```
### Problem:   
You have completed a feature and merged it into the main branch. Now you need to clean up by deleting the remote branch named `old-feature`. How do you delete this branch from the remote repository?   
