---
title: Git Branching Ex-Deep Dive into Rebase
date: '2025-10-27T10:06:50+08:00'
draft: false
tags:
  - git
  - branching
---
# Rebase   
## What Rebase Does   
Rebasing in Git is a process that allows you to move or combine a sequence of commits to a new base commit. This is particularly useful for keeping your commit history linear and clean, which can make it easier to follow the changes in a project.   
Here's how rebasing works:   
1. **Rebase a Branch onto Another Branch:**
	When you rebase `feature-branch` onto `main`, Git first determines the common ancestor of the two branches. Then, it takes all the commits from `feature-branch` that are not in `main` and re-applies them on top of `main`.   
	```bash
	git checkout feature-branch
	git rebase main
	```
2. **Rebase Workflow:**   
    - **Rewind:** Git temporarily removes the commits from `feature-branch` that are not in `main`, making it appear as if the branch is based on `main`.   
    - **Replay:** Git then applies each of the commits from `feature-branch` one by one onto the tip of `main`.   
   
## How Rebase Affects Branching   
Rebasing can significantly affect how branches relate to each other. Here are some key points:   
1. **Linear History:**
	Rebasing creates a linear commit history, which can be easier to understand and follow. This is especially useful in collaborative projects where a clean history helps new contributors understand the changes that have been made.   
2. **Conflicts:**
	During the rebase process, if there are conflicting changes between the commits being rebased and the base branch (e.g., `main`), Git will pause and allow you to resolve these conflicts manually. After resolving conflicts, you continue the rebase.   
    ```bash
	git add <resolved-file>
	git rebase --continue
	```
3. **Changing Commit Hashes:**
	Rebasing changes the commit hashes of the rebased commits because their parent commit has changed. This can be problematic if those commits have already been pushed to a shared repository because it requires a force push to update the remote branch.   
    ```bash
	git push --force
	```
4. **History Rewriting:**
	Since rebase essentially rewrites history, it should be used with caution, particularly with shared branches. It's generally safe to rebase local branches that haven't been shared with others. For shared branches, it's better to use `merge`.   
5. **Avoiding Merge Commits:**
	By using rebase, you can avoid unnecessary merge commits in the history. This makes the history cleaner but means you won't see explicit points where branches were merged, which might hide the context of the changes.   
   
## Example Scenario   
Consider this scenario:   
- `main` has commits `A`, `B`, and `C`.   
- `feature-branch` has commits `D` and `E` based on commit `B` of `main`.   
```bash
main: A---B---C
	       \
feature:    D---E

```
After rebasing `feature-branch` onto `main`, the history would look like this:   
```bash
main: A---B---C
               \
feature:        D'---E'

```
Commits `D` and `E` are now reapplied on top of commit `C` in `main`, becoming `D'` and `E'`.   
# Undo Rebase   
## Undoing an Ongoing Rebase   
If you are in the middle of a rebase and want to stop and undo the changes:

**Abort the Rebase:**
This command will stop the rebase process and return your branch to the state it was in before the rebase started.   
```bash
git rebase —abort
```
This will discard all changes made during the rebase and reset the branch to its original state before the rebase was initiated.   
This will discard all changes made during the rebase and reset the branch to its original state before the rebase was initiated.   

### Scenario:   
You are in the middle of rebasing `feature-branch` onto `main`, but decide to abort the process.   
- **Initial State**:   
```bash
main:       A---B---C
		         \
feature-branch:   D---E
```
- **During Rebase**:   
You start rebasing `feature-branch` onto `main`, and Git is in the process of replaying commits `D` and `E`.   
```bash
main:       A---B---C
		              \
feature-branch:        (D---E) [In progress]
```
- **Aborting the Rebase:**   
Use the command:   
```bash
git rebase --abort
```
- **Final State (after aborting)**:   
```bash
main:       A---B---C
				 \
feature-branch:   D---E

```
## Undoing a Completed Rebase   
If you have already completed the rebase and want to undo it:

**Use the ORIG\_HEAD Reference:**
After a rebase, Git temporarily saves the previous state of your branch in `ORIG\_HEAD`. You can reset your branch to this state.   
```bash
git reset --hard ORIG_HEAD
```
This will reset your branch to the state it was in before the rebase. Note that this command will discard any changes made during the rebase, so use it with caution.   
   
### Scenario:   
You have completed rebasing `feature-branch` onto `main`, but decide to undo it.   
- **Initial State (before rebase):**   
```bash
main:       A---B---C
				 \
feature-branch:   D---E
```
- **After Rebase:**   

You have successfully rebased `feature-branch` onto `main`.   
```bash
main:       A---B---C
				 \
feature-branch:   D'---E'
```
**Undoing the Rebase:** 

- Use the command:   
```bash
git reset --hard ORIG_HEAD
```
- **Final State (after resetting to ORIG\_HEAD):**   

```bash
main:       A---B---C
				 \
feature-branch:   D---E
```
## Undoing a Pushed Rebase   
If you have already pushed the rebased branch to a remote repository, undoing the rebase becomes more complex, especially if others have already started working on the rebased branch. Here are the steps:   
1. **Inform Your Team:**
Communicate with your team to ensure no one else is working on the rebased branch or has pulled the changes. This is crucial to avoid conflicts and lost work.   
2. **Reset the Local Branch:**
Reset your local branch to the previous state before the rebase using `ORIG\_HEAD`.   
```bash
git reset --hard ORIG_HEAD

```
3. **Force Push to the Remote:**
Force push the reset branch to the remote repository to overwrite the rebased history. This should be done carefully and only if you are sure no one else is affected.   
```bash
git push --force

```
   
### Scenario:   
You completed the rebase but `ORIG\_HEAD` is not available. You will use the reflog to find the previous state.   
- **Initial State (before rebase):**   
```bash
main:       A---B---C
                 \
feature-branch:   D---E

```
- **After Rebase:**   
You have successfully rebased `feature-branch` onto `main`.   
```bash
main:       A---B---C
                     \
feature-branch:       D'---E'

```
- **Using Reflog:**   
View the reflog to find the commit before the rebase.   
```bash
git reflog
```
You find that the commit hash before the rebase was `B`.   

- **Resetting to the Previous Commit:**   
Use the commit hash found in the reflog.   
```bash
git reset --hard <commit-hash>
```
- **Final State (after resetting):**   
```bash
main:       A---B---C
                 \
feature-branch:   D---E

```

## Using a Reflog for More Complex Cases   
If `ORIG\_HEAD` is not available or you need to undo more complex changes, you can use Git's reflog to find the commit before the rebase and reset to that commit.   
1. **View the Reflog:**
The reflog shows a history of all actions (including rebases) that have affected the HEAD.   
```bash
git reflog
```
2. **Find the Commit Before the Rebase:**
Identify the commit hash before the rebase started.   
3. **Reset to the Previous Commit:**
Reset your branch to that commit.   
```bash
git reset --hard <commit-hash>
```
   
### Scenario:   
You pushed the rebased `feature-branch` to the remote and now need to undo it.   
- **Initial State (before rebase):**   
```bash
main:       A---B---C
                 \
feature-branch:   D---E
```

- **After Rebase:**   
You have successfully rebased and pushed `feature-branch` to the remote.   
```bash
main:       A---B---C
                	 \
feature-branch:       D'---E'
```

- **Resetting Locally:**   
Use `ORIG\_HEAD` to reset your local branch to the state before the rebase.   
```bash
git reset --hard ORIG_HEAD
```

- **Final State (locally after resetting):**   
```bash
main:       A---B---C
                 \
feature-branch:   D---E
```

- **Force Pushing to Remote:**   
Force push to update the remote branch.   
```bash
git push --force
```

- **Final State (remote and local are now in sync):**   
```bash
main:       A---B---C
                 \
feature-branch:   D---E
```
   
