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
  - [Undoing Last Pushed Commit](#undoing-last-pushed-commit)
  - [Gitignore not working](#gitignore-not-working)
- [How to merge](#how-to-merge)
- [GitHub Actions](#github-actions)
  - [Best Practices](#best-practices)
  - [Self-hosted Runners](#self-hosted-runners)

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

### Undoing Last Pushed Commit

```bash
git reset HEAD^ --hard

git push origin -f
```

### Gitignore not working

Sometimes, you add a file to your `.gitignore` file and... it simply won't ignore it. But why ?

It is because git likes to cache files to gain speed. However, sometimes it can break the surveillance system for some files. So here are the steps to force Git to ignore your unwanted file:

1. Commit your important work

2. Remove all files from 
```bash
git r -
```

## How to merge

In this example, **main** has changes that **features** doesn't have. We need to work on a new feature so we have to start a new branch from **features**. So let's add **main** changes to the **features** branch!

1. Make sure that **main** and **features** are **up to date** by running `git pull` on both of them.
2. Checkout to **features**
3. Run `git merge main` from the **features** branch

### Merge in CLI

Sometimes, life is hard and you will meet very restricted development environment. It is possible to you have to merge two branches and resolve conflicts in CLI. How do we proceed?

A conflict (less one `<` because otherwise, your IDE will consider it as a real conflict!)
```bash
If you have questions, please
<<<<<< HEAD
open an issue
=======
ask your question in IRC.
>>>>>> branch-a
```

If you've ran: `git merge my-branch` while being on master. HEAD is your `master` branch (top one) and `my-branch` is the bottom one. Branch changes are separated by the `==========`.

## GitHub Actions

### Best Practices

- Always set a timeout for your workflows.

```yaml
jobs:
  my-first-job:
    timeout-minutes: 10
    runs-on: ubuntu-latest
    steps:
      - [...]
```

- Always consider if third-party actions are really needed. They can constitue a threat to the repository and give access to h4ck3rs.

- Apply the 0-trust principle to your workflows: limit scope of your workflow tokens.

### Self-hosted Runners

Keep in mind that GitHub Actions is limited in **time** (Runner Minutes). Your workflows run on the servers of Microsoft so if you regurlarly go over the limit of your offer, you can deploy your own runner and execute your workflows on this runner.

![ga-pricing](/devOps/git/resources/ga-pricing.png)

However, inform yourself before using a `self-hosted runner` and look up for potential vectors of attack. For instance, a self-hosted runner shared between a private and a public repository can be a problem because it violates security isolation principle.
