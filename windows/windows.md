# Table of Content

- [Windows File System](#windows-file-system)
- [Windows Commands](#windows-commands)
    - [Shortcuts](#shortcuts)
    - [Disk Operation System Commands (DOS commands)](#disk-operating-system-commands-dos-commands)
    - [User](#user)
    - [Query on a Windows Filesystem](#query-on-a-windows-filesystem)
    - [Scripts](#scripts)
    - [WSL (Windows Subsystem for Linux)](#wsl-windows-subsystem-for-linux)

# Windows File System

The Windows file system is quite different compared to its fellows. There is **more than a single root** because disks are mounted on their own (= on different trees)

![img_1](/windows/resources/file-tree.jpg)

In comparison, the Linux and the MacOSX file system (which is also based on Linux) has a single root and disks are mounted in the same tree.

# Windows commands

## Shortcuts

- `Windows` + `R` => Open the **Run Window**
    - `wt` => Open the **Terminal Application**
- `Windows` + `E` => Open the File Browser
- `Windows` + `M` => Minimize all windows
- `Windows` + `L` => Lock the system
- `Windows` + `I` => Access the settings
- `Windows` + `ALT` + `DEL` => Open the Task Manager   

## Disk Operating System commands (DOS commands)

- `dir`: list files and folders in working directory
- `cd`: change current directory
- `md` or `mkdir`: create a new directory
- `del`: remove a file or several files
- `rmdir` or `rd`: remove one or several folder(s)
- `copy`: copy a file
- `cls`: clear the content of the terminal
- `clip`: copy the output of a command to the clipboard (needs to be used with a pipe)

## Networking

- `ipconfig`: show IPv4 and IPv6 addresses
- `ipconfig /all`: show DNS and MAC address
- `ipconfig /all | findstr DNS`: show only DNS address
- `ipconfig /release`: force to end DHCP lease
- `ipconfig /renew`: ask for another IP address to the DHCP server
- `ipconfig /displaydns`: list all websites (domain name) and their corresponding IP addresses
- `ipconfig /flushdns`: Erase DNS cache (all known domain names and their corresponding IP addresses)

- `ping -t google.fr`: ping the specified address until stopped by user
- `ping -b`: ping all machines on a network (deprecated?)

- `nslookup ratp.fr`: obtain information from DNS servers about a specified domain

## User

## Query on a windows filesystem

## Scripts

## WSL (Windows Subsystem for Linux)

List all distros installed
```sh
wsl --list
```

Terminate a specific instance of a distro
```sh
wsl --terminate DistroName
```