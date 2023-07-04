# Git
## Table of Content

- [First config](#first-config)
- [CLI](#cli)
  - [Starting](#starting)
  - [Where am I?](#where-am-i)
  - [Is my branch up-to-date with the origin?](#is-my-branch-up-to-date-with-the-origin)
  - [Lookin for my branch](#lookin-for-my-branch)
  - [Switch to a Branch That Came From a Remote Repo](#switch-to-a-branch-that-came-from-a-remote-repo)
  - [List commits not pushed](#list-commits-not-pushed)
  - [Check for differences between branches](#check-for-differences-between-branches)
  - [Oups I am in trouble](#oups-i-am-in-trouble)
- [How to merge](#how-to-merge)

## Git in Theory

![git-workflow-diagram](/devOps/git/resources/git-workflow.png)

- The working tree : it is simply the set of files and folders a developer can add/edit/rename/delete during software development.
- 
- 
## First config

```bash
git config --global user.name "username"
git confg --global user.email "william.madie@yahoo.fr"
```

## CLI

### Starting

Initialize a new Git Repository
```bash
git init
```

Create a local branch from a remote branch
```bash
git checkout -b remote/branch
```

### Where am I?

See all my branches and what branch is active now (*)
```bash
git branch
```
Output:
```bash
  deidentification
* main
```

Create a new branch from current branch
(Please note that all uncommited changes will GET CARRIED OVER the new branch)
```bash
git checkout -b new-branch-name
```

### Is my branch up-to-date with the origin?

See if local branch is up-to-date with remote branch AND See current
local modifications
```bash
git status
```

### Lookin for my branch

Refresh git in order to see a new remotely added branch
```
git fetch
git branch -av
```

Change branch
```
git checkout branch-name
```

### Switch to a Branch That Came From a Remote Repo

```
git checkout --track origin/my-branch-name
```

### List commits not pushed

List commits not pushed
```
git log branch-name
```

### Check for differences between branches

Checks for differences of one file between two branches
```bash
git diff origin/branch1:path/to/file.csv origin/branch2:path/to/file.csv
```

### Oups I am in trouble

Replace local branch with remote branch
(Here I want to replace the local branch123 with the remote branch123)
```bash
git checkout branch123 # Don't forget to go on the local branch to replace before reset
git reset --hard origin/branch123
```

## How to merge

In this example, **main** has changes that **features** doesn't have. We need to work on a new feature so we have to start a new branch from **features**. So let's add **main** changes to the **features** branch!

1. Make sure that **main** and **features** are **up to date** by running `git pull` on both of them.
2. Checkout to **features**
3. Run `git merge main` from the **features** branch

