# Linux

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

## Shortcuts

- Switch to another desktop: `CTRL` + `ALT` + `ARROW`
- Pass a window on the second screen: `WINDOWS` + `SHIFT` + `ARROW`

## The legendary VIM Editor

```bash
vim fileIwant2edit
#or
vi fileIwant2edit
```

Inside vim, you can easily get panicked once you've realised there is **no
easy escape**. You start to think that your computer is evil and lured you into this trap. But don't worry, it is not the case ! Here are the commands that will save your life:

 - Look for a word or several words in the file:
`/` + `pattern`

 - Switch to the edition mode: `i`
 - Save and exit: `ESCP` + `:wq!`
 - Exit without saving: `ESCP` + `:q!`


## Scripts

### Executing a script & Sourcing a script

|              Executing (bash or ./process or process)             |              Sourcing (source or . process)              |
|:-----------------------------------------------------------------:|:--------------------------------------------------------:|
| runs the commands in **a new shell process** which is then closed | runs the commands in **the current shell process**       |
| **does not change the environment** in the current running shell  | **changes the environment** in the current running shell |


## Config of WSL

### General



```bash
sudo apt install man
sudo apt install wget
```
### Gcc

```bash
sudo apt update && sudo apt update
sudo apt autoremove
sudo apt install gcc
gcc --version
```

### Java

1. Install IntelliJ in Windows
2. Install the SDK (Software Development Kit) in the WSL

```bash
sudo apt update && sudo apt update
sudo apt autoremove
sudo apt install default-jdk
java -version
```

### MySQL

1. Install mysql-server
```bash
sudo apt install mysql-server
```
2. Launch the secure installation
```bash
sudo mysql_secure_installation
```
3. Start mysql
```bash
sudo service mysql start
```
4. If there is a problem, try :
```bash
sudo service mysql force-reload
```