# Git Commands Documentation

This document provides a comprehensive list of Git commands with a brief explanation for each. Git is a distributed version control system used to track changes in source code during software development.

## Table of Contents

- [Basic Commands](#basic-commands)
- [Branching and Merging](#branching-and-merging)
- [Remote Repositories](#remote-repositories)
- [Stashing](#stashing)
- [Undoing Changes](#undoing-changes)
- [Logs and History](#logs-and-history)

---

## Basic Commands

- **`git init`**  
  Initializes a new Git repository in the current directory.

- **`git clone <repository>`**  
  Clones a remote repository to your local machine.

- **`git add <file>`**  
  Stages changes in the specified file for the next commit.

- **`git commit -m "<message>"`**  
  Commits the staged changes with a descriptive message.

- **`git status`**  
  Displays the state of the working directory and staging area.

- **`git log`**  
  Shows the commit history of the current branch.

- **`git diff`**  
  Shows changes between commits, commit and working directory, etc.

- **`git config --global user.name "<name>"`**  
  Sets the global Git username.

- **`git config --global user.email "<email>"`**  
  Sets the global Git email.

---

## Branching and Merging

- **`git branch`**  
  Lists all local branches in the repository.

- **`git branch <branch-name>`**  
  Creates a new branch with the given name.

- **`git checkout <branch-name>`**  
  Switches to the specified branch.

- **`git checkout -b <branch-name>`**  
  Creates and switches to a new branch.

- **`git merge <branch-name>`**  
  Merges the specified branch into the current branch.

- **`git branch -d <branch-name>`**  
  Deletes the specified branch.

---

## Remote Repositories

- **`git remote -v`**  
  Lists all the remote repositories associated with the local repository.

- **`git remote add <name> <url>`**  
  Adds a new remote repository.

- **`git push <remote> <branch>`**  
  Pushes commits from the local branch to the specified remote branch.

- **`git pull`**  
  Fetches and integrates changes from the remote repository to your current branch.

- **`git fetch`**  
  Downloads changes from a remote repository but doesn't apply them.

---

## Stashing

- **`git stash`**  
  Temporarily saves changes in a dirty working directory.

- **`git stash pop`**  
  Applies the most recently stashed changes and removes them from the stash.

- **`git stash list`**  
  Lists all stashed changes.

- **`git stash drop`**  
  Discards the most recent stash.

---

## Undoing Changes

- **`git reset <file>`**  
  Removes a file from the staging area without deleting changes from the working directory.

- **`git reset --hard <commit>`**  
  Resets the working directory and index to the specified commit, discarding all changes.

- **`git revert <commit>`**  
  Reverts the specified commit by creating a new commit.

- **`git rm <file>`**  
  Removes a file from the working directory and stages the deletion.

---

## Logs and History

- **`git log --oneline`**  
  Displays a simplified version of the commit history.

- **`git log --graph --oneline`**  
  Shows a visual graph of the commit history.

- **`git log --author="<name>"`**  
  Filters commits by the specified author.

- **`git blame <file>`**  
  Shows who made changes to each line in a file and when.

---

## Conclusion

These are some of the most commonly used Git commands to help you manage your repositories efficiently. Git is a powerful tool, and mastering these commands will greatly enhance your version control workflow.
