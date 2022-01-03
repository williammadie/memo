# Linux

[User](user)

## User

List of users and passwords

```bash
cat /etc/passwd
```

List of users' hash passwords (**SHA512**)

```bash
sudo cat /etc/shadow
```

## Query on a linux filesystem

Search a specific text in a file:
```bash
grep -rnw 'PATH' -e 'mon_texte'
```
Options used here:
- -r recursive search from the given `PATH`
- -n show the line number in the file
- -w match the whole word
- -e pattern use during the search

## Scripts

### Executing a script & Sourcing a script

|              Executing (bash or ./process or process)             |              Sourcing (source or . process)              |
|:-----------------------------------------------------------------:|:--------------------------------------------------------:|
| runs the commands in **a new shell process** which is then closed | runs the commands in **the current shell process**       |
| **does not change the environment** in the current running shell  | **changes the environment** in the current running shell |


## Config of WSL

### Java

1. Install IntelliJ in Windows
2. Install the SDK (Software Development Kit) in the WSL

`sudo apt update && sudo apt update`

`sudo apt install default-jdk`

`java -version`