# Git

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
git checkout -b nom_nouvelle_branche
```

### Lookin for my branch

Refresh git in order to see a new remotely added branch
```
git fetch
git branch -av
```
