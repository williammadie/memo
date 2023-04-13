# Linux

## Table of Contents

- [Processes](#processes)
- [User](#user)
- [Managing Permissions](#managing-permissions)
- [Useful commands](#useful-commands)
    - [Basic commands](#basic-commands)
    - [Networking](#networking)
    - [Query on a linux filesystem](#query-on-a-linux-filesystem)
    - [Storage related commands](#storage-related-commands)
    - [Watch logs](#watch-logs)
- [Environment Variables](#environment-variables)
- [Shortcuts](#shortcuts)
- [The Legendary VIM Editor](#the-legendary-vim-editor)
    - [Differences between VIM and VI](#differences-between-vim-and-vi)
    - [Commands](#commands)
    - [Config](#config)
- [Scripts](#scripts)
    - [Bash basics](#bash-basics)
        - [Introduction](#introduction)
        - [Basic commands](#basic-commands)
        - [Structure of a Bash script](#structure-of-a-bash-script)
        - [Variables](#variables)
        - [Conditions](#conditions)
        - [Loops](#loops)
        - [String operations](#string-operations)
        - [Arithmetic operations](#arithmetic-operations)
        - [Functions](#functions)
    - [Executing a script & Sourcing a script](#executing-a-script--sourcing-a-script)
- [Terminal Multiplexer](#terminal-multiplexer)
- [Config of WSL](#config-of-wsl)
    - [General](#general)
    - [GCC](#gcc)
    - [Java](#java)
    - [MySQL](#mysql)

## Processes

In Linux, there is a hierarchy of processes that doesn't exist in Microsoft Windows.

In Linux distributions, all processes are ihnerited from the process with `PID 0`. This process is started by the Linux Kernel during the boot process. It is responsible for starting and managing all other processes on the system.

PID 0 also do the following tasks:
- set up the system environment
- mount file systems
- start system daemons
- perform other initialization tasks

PID 1 (the `init` process) is the one charged of starting and managing all other processes.

This hierarchy of processes is inspired by UNIX systems which looks like a tree (tree structure):

![unix-like-hierarchy](/operating_systems/linux/resources/unix-like-hierarchy.jpg)

Things to consider:
- If a process is killed, all its children are adopted by the `init` process (PID 1)

## User

List of users and passwords

```bash
cat /etc/passwd
```

List of users' hash passwords (**SHA512**)

```bash
sudo cat /etc/shadow
```

## Managing Permissions

### Groups

Create a group (needs to be logged as root user with `su -`)
```bash
groupadd groupname
```

Add a user to a group
```bash
adduser username groupname
```

Add a folder to a group
```bash
chgrp groupname /path/to/folder
```

Add permissions to group on folder (folder needs to be added to group previously)
```bash
chmod g+rwx /path/to/folder
```

## Useful commands 
### Basic commands

- `man`: show a specific command documentation
- `pwd`: print working directory (location in file structure)
- `ls`: list files and folders in a given directory
- `cd`: change directory
- `mv`: move/rename a file
- `cp`: copy a file
- `scp`: copy a file from a machine to another through SSH
- `rm`: remove file(s)
- `mkdir`: create a directory
- `rmdir`: delete a directory (empty only)
- `top`: show current running processes
- `htop`: same as top but with an enhanced user interface
- `ln`: create a physical or symbolic link to a file or a repertory
- `find`: search for a file recursively in the file structure
- `grep`: search for a string in files (using REGEX)
- `cat`: show the content of a file
- `clear`: clear the content of the terminal
- `echo`: print the given string
- `date`: show the current date hour and timezone
- `exit`: close the terminal

### Manage dependencies

- `sudo apt install`: install a given package
- `sudo apt update`: update the packages index
- `sudo apt upgrade`: update all the packages based on the packages index 
- `sudo apt remove`: remove an installed package
- `sudo apt purge`: remove all files of a given package
- `sudo apt autoremove`: remove unused packages
- `apt list`: list all installed/available/upgradeable packages
- `sudo apt search`: search for a specific package
- `sudo apt show`: show information about a given package

### Networking

- `ìfconfig -a`: show information about all machine interfaces (IPv4, IPv6, MAC addresses)
- `ping google.fr`: ping the specified address until stopped by user
- `dig ratp.fr`: gather DNS information about a specified domain name
- `traceroute ratp.fr`: show the list of crossed routers (if routers want to respond)

Here is the result of the latest command:
```bash
traceroute to ratp.fr (195.200.228.10), 30 hops max, 60 byte packets
 1  Zeus.mshome.net (172.32.12.34)  0.290 ms  0.188 ms  0.180 ms
 2  192.168.232.95 (192.168.232.95)  25.286 ms  33.955 ms  33.932 ms
 3  * * *
 4  10.4.1.14 (10.4.1.14)  72.453 ms 10.4.0.14 (10.4.0.14)  72.200 ms 10.4.1.14 (10.4.1.14)  67.590 ms
 5  10.181.154.252 (10.187.154.252)  72.161 ms  72.424 ms  72.749 ms
 6  13.132.133.77.rev.sfr.net (77.133.134.13)  72.730 ms  72.059 ms  71.964 ms
 7  149.10.133.77.rev.sfr.net (77.133.10.149)  72.289 ms  43.791 ms  30.291 ms
 8  149.10.133.77.rev.sfr.net (77.133.10.149)  29.515 ms  36.951 ms  29.504 ms
 9  ae63-0.noidf001.rbci.orange.net (10.10.178.57)  37.724 ms  37.720 ms  192.036 ms
10  ae49-0.nridf101.rbci.orange.net (123.252.98.101)  36.944 ms  37.260 ms  30.196 ms
11  * ae42-0.ncidf103.rbci.orange.net (123.252.98.93)  38.832 ms  38.829 ms
12  lag-1.nmidf105.rbci.orange.net (123.249.212.1)  31.769 ms  46.827 ms  37.182 ms
13  193.252.137.222 (123.252.137.222)  162.354 ms  163.517 ms  159.966 ms
14  * * *
15  89.67.111.50 (89.67.111.50)  155.601 ms  155.238 ms  155.228 ms
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * * *
22  * * *
23  * * *
24  * * *
25  * * *
26  * * *
27  * * *
28  * * *
29  * * *
30  * * *
```

Lines with `* * *` mean that the program did not receive any response from the router at this hop.

### Query on a linux filesystem

Search for a file in a folder and all its subdirectories
```bash
find . -name 'nom_fichier_à_chercher'
```
(The . refers to the current locatiton/directory)

Search a specific text in a file:
```bash
grep -rnw 'PATH' -e 'mon_texte'
```
Options used here:
- -r recursive search from the given `PATH`
- -n show the line number in the file
- -w match the whole word
- -e pattern use during the search

See how many files are present in a directory
```bash
ls | wc -l
```

See how many files are present in a directory and in its subdirectories
```bash
find . -type f | wc -l
```

### Storage related commands

See the **size of a folder**:
(the **max-depth** option is used to avoid recursive behaviors)
```bash
du -h --max-depth=1.
```

See the **storage capacity of the server**:
```bash
df -h
```

### Watch logs

See program logs in real time
```bash
tail -f path/to/file.log
```

## Environment Variables

An **Environment Variable** is a *variable whose value is set outside the program, typically through functionality built into the operating system*.

Set an environment variable
```bash
export PASSWORD=123456789
```

Unset an environment variable
```bash
unset PASSWORD
```

Secretly set an environment variable
(the command will not appear in ~/.bash_history)
(only add one space before the command)
```bash
 export PASSWORD=123456789
```

## Shortcuts

- Switch to another desktop: `CTRL` + `ALT` + `ARROW`
- Pass a window on the second screen: `WINDOWS` + `SHIFT` + `ARROW`

## The legendary VIM Editor

### Differences between VIM and VI

VIM is a text editor built on top of VI. It litteraly means **VI iMproved**. VIM offers a lot more features than VI. It is also more used than VI because it is a free text editor (free as a speech)


### Commands

```bash
vim fileIwant2edit
#or
vi fileIwant2edit
```

Inside vim, you can easily get panicked once you've realised there is **no
easy escape**. You start to think that your computer is evil and lured you into this trap. But don't worry, it is not the case ! Here are the commands that will save your life:

- Look for a word or several words in the file:
`/` + `pattern`

- `i` : Switch to the edition mode
- `V` : Select the whole line
- `Y` : Copy
- `P` : Paste
- `ESCP` + `:wq!` : Save and exit
- `ESCP` + `:q!` : Exit without saving

Only in VIM:

- `:e` : Open a new file
- `:b` : Switch to another opened file
- `:se nonu` : Hide line numbers
- `:se nu` : Show line numbers

### Config

It is possible to add functionalities to the Vim Editor by changing settings 
inside the `.vimrc` file. (In most cases, it is not present by default and you
have to create it in `~/.vimrc`)

## Scripts

### Bash basics

#### Introduction

**Bash** (AKA **Bourne Again Shell**) is a type of interpreter that processes shell commands. A *shell interpreter** takes commands in plain text format and calls Operating System services to do something.

A shell script is a file or program that shell will execute.

#### Basic commands

Identify which *type of Shell* you're using. Here you're using Bash
```bash
$ which $SHELL
/bin/bash
```

Sleep for a given amount of time
```bash
$ sleep 4
```

#### Structure of a Bash script

Any bash script is required to start the same way. First, we have to indicate
which executable is being used to read the following script. Then, we'll check
if the user has specified the correct number of arguments.
```bash
#! /bin/bash

if [ $# != 3 ]
then
    echo "SYNTAXE: bash $0 ARG1 ARG2 ARG3"
    return 1
else
    # Do a job
fi
```
#### Variables

In Bash, we don't need to declare a variable by specifying its data type. 

Declare a variable
```bash
CITY='New York'
NAME='John Doe'
AGE=26
GRADE=8.43
EMPLOYED=true
```

Get the value of a variable
```bash
echo $NAME $AGE $GRADE $EMPLOYED
```

Ask for an input and bind it to a variable
```bash
echo -n "Enter your name: " # -n for input on the same line
read NAME
```

#### Conditions

**Arithmetic operators**
- `-eq` : is equal to
- `-ne` : is not equal to
- `-gt` : is greater than
- `-ge` : is greater than or equal to
- `-lt` : is less than
- `-le` : is less than or equal to

**String operators**

- `==` : is equal to
- `!=` : is not equal to
- `-z` : is null
- `-n` : is not null
- `=~` : contains a pattern (Support for REGEX)

**Structure of IF**

```bash
if CONDITION1
then
    RESPONSE1
elif CONDITION2
then
    RESPONSE2
else
    RESPONSE3
fi
```

**Structure of SWITCH CASE**

```bash
case $variable in 

    CASE1)
    echo 'Case1'
    ;;

    CASE2)
    echo 'Case2'
    ;;

    CASE3)
    echo 'Case3'
    ;;

    *)
    echo 'Default'
    exit 1
    ;;
esac
```

Testing if an integer equals 4 or 5
```bash
if [ $val -eq 4 ] || [ $val -eq 5 ]
then
    echo "Error: Not equal to 4 or 5"
fi
```

Testing if a string equals 'start' or 'stop'
```bash
if [ $val == 'start' ] || [ $val == 'stop' ]
then
    echo "Error: Not equal to 'start' or 'stop'"
fi
```

#### Loops

Traditional For loop
```bash
for (( i=0; i<5; i++))
do
    echo $i
done
```

For loop for given elements
```bash
for i in 1 2 3 4 5
do
    echo $i
done
```

For loop with range 
```bash
for i in {0..6..2}  # {start..end..step}
do
    echo $i
done
```

Traditional While loop
```bash
while [ condition ]
do
    # do something
done
```

Infinite While loop
```bash
while true  # the condition can also be empty
do
    # do something
done
```

Until loop
```bash
# This loop is quite uncommon. It runs until the given condition is true. In a way, it can be considered as the opposite of the while loop which runs until the given condition is false.
NUMBER=1

until [ $NUMBER == 4 ]
do
    echo "Number is $((NUMBER++))"
done
```

*Observation: Like other languages, it is possible to use a condition with `break` to get out of the loop early or `continue` to go to the next iteration*

#### String operations

Lower a string
```bash
lower_str=$(echo "$str2lower" | tr '[:upper:]' '[:lower:]')
```

Concatenate variables
```bash
FIRST_NAME='John'
LAST_NAME='Doe'
FULL_NAME=$FIRST_NAME$LAST_NAME

# 2° way

NUMBER=1
NUMBER+=2
```

String interpolation
```bash
FIRST_NAME='John'
echo "Hello ${FIRST_NAME}"
```

*Observation: Bash supports both singlequotes and doublequotes. However, only doublequotes support string interpolation*

#### Arithmetic operations

Perform an arithmetic operation
```bash
NUM=5
((NUM-=2))  # NUM is directly changed
echo $NUM
>>> 3
```

Get a random number
```bash
echo $RANDOM    # RANDOM is a special random value
```

Generate a list of numbers
```bash
echo {0..10..1} # start..end..step
```

#### Functions

Write a function
```bash
function my_first_function() {
    # statements
}
```

Call a function
```bash
my_first_function
```

*Observation: In Bash, variables outside of the scope of the function are accessible inside the function*

### Executing a script & Sourcing a script

|              Executing (bash or ./process or process)             |              Sourcing (source or . process)              |
|:-----------------------------------------------------------------:|:--------------------------------------------------------:|
| runs the commands in **a new shell process** which is then closed | runs the commands in **the current shell process**       |
| **does not change the environment** in the current running shell  | **changes the environment** in the current running shell |

## Terminal Multiplexer

### Screen

**screen** is a tool that **provides the ability to launch and use multiple shell sessions from a single ssh session**. The process can be detached from session and then can reattach the session at a later time. 

By default, programs running in a screen session don't end when the user closes his SSH session. It is very useful for programs that needs to run whether someone is online or not.

Launch a screen session
```bash
screen
```

Launch a screen session with a given name
```bash
screen -S session1
```

Create a new session (Watch out: delete session with same name if there is one)
```bash
screen -RdS session1
```

Detach from a screen session
```bash
CTRL + A + D (at the same time)

# OR 

screen -d session1 # safer
```

```Attach to a existing screen session
screen -r session1
```

End a screen session
```bash
exit
```

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