# Git
## Table of Content

- [First config](#first-config)
- [CLI](#cli)
  - [Where am I?](#where-am-i)
  - [Lookin for my branch](#lookin-for-my-branch)
  - [List commits not pushed](#list-commits-not-pushed)
  - [How to merge](#how-to-merge)

## First config

```bash
git config --global user.name "username"
git confg --global user.email "william.madie@yahoo.fr"
```

## CLI

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
```bash
git checkout -b new-branch-name
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

## List commits not pushed

```
git log branch-name
```

## How to merge

In this example, **main** has changes that **features** doesn't have. We need to work on a new feature so we have to start a new branch from **features**. So let's add **main** changes to the **features** branch!

1. Make sure that **main** and **features** are **up to date** by running `git pull` on both of them.
2. Checkout to **features**
3. Run `git merge main` from the **features** branch
