# Table of Content

- [DOS and Windows NT](#dos-and-windows-nt)
- [Windows File System](#windows-file-system)
- [Windows Commands](#windows-commands)
    - [Shortcuts](#shortcuts)
    - [Disk Operation System Commands (DOS commands)](#disk-operating-system-commands-dos-commands)
    - [User](#user)
    - [Query on a Windows Filesystem](#query-on-a-windows-filesystem)
    - [Scripts](#scripts)
    - [WSL (Windows Subsystem for Linux)](#wsl-windows-subsystem-for-linux)

## DOS and Windows NT

**DOS** (**Disk Operating System**) was a popular family of operating systems in the early 1980s. It was developed by Microsoft. It was designed for **IBM-PCs** and has been used until 1993 (year of release of **Windows NT 3.1**)

Here is a list of the most used DOS operating systems:

[Single User and Single Task]

- `MS-DOS` (Microsoft Disk Operating System)
- `PC DOS` (IBM Personal Computer Disk Operating System)
- `DR-DOS` (Digital Research Disk Operating System)
- `FreeDOS` (an open-source version of DOS)

**Windows NT** (**New Technology**) is the current family of Windows operating systems. The first version was **Windows NT 3.1** release in 1993.

Here is a list of the most famous Windows NT operating systems: 

[Multi-Users and Multi-Tasks]

- `Windows NT 3.1`
- `Windows NT 3.5`
- `Windows NT 4.0`
- `Windows 2000`
- `Windows XP`
- `Windows Server 2003`
- `Windows Vista`
- `Windows 7`
- `Windows 8`
- `Windows 10`
- `Windows 11`

**Important Note**: Operating systems from the Windows NT family have a lot of differences but also of common points with DOS operating systems. Microsoft intentionally retained a certain level of compatibility with DOS. You'll find some examples below:

**Common**:

1. Both systems use the same filepath format, the `DOS format` which looks like `C:\Users\user\Documents\my-doc.txt`. As a reminder, UNIX-based systems like Linux and macOS use the **POSIX** (**Portable Operating System Interface**) format which looks like `/home/user/Documents/my-doc.txt`

2. Windows NT and DOS support batch files (script files) and have some common system files.

**Differences**:

1. Windows NT supports GUI whereas DOS only supports CLI

2. Windows NT supports **multiple users at the same time** while DOS is a **single-user operating system**.

3. Windows NT supports multiple file systems (`NTFS` which is far more advanced than `FAT` used by DOS but it also supports `FAT`). By default, latest Windows NT operating systems use `NTFS`.

4. Windows NT natively supports networking whereas DOS requires third-party softwares.

## Windows File System

The Windows file system is quite different compared to its fellows. There is **more than a single root** because disks are mounted on their own (= on different trees)

![img_1](/operating_systems/windows/resources/file-tree.jpg)

In comparison, the Linux and the MacOSX file system (which is also based on Linux) has a single root and disks are mounted in the same tree.

## Windows commands

### Shortcuts

- `Windows` + `R` => Open the **Run Window**
    - `wt` => Open the **Terminal Application**
- `Windows` + `E` => Open the File Browser
- `Windows` + `M` => Minimize all windows
- `Windows` + `L` => Lock the system
- `Windows` + `I` => Access the settings
- `Windows` + `ALT` + `DEL` => Open the Task Manager   

### Disk Operating System commands (DOS commands)

- `dir`: list files and folders in working directory
- `cd`: change current directory
- `md` or `mkdir`: create a new directory
- `del`: remove a file or several files
- `rmdir` or `rd`: remove one or several folder(s)
- `copy`: copy a file
- `cls`: clear the content of the terminal
- `clip`: copy the output of a command to the clipboard (needs to be used with a pipe)

### Networking

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

### User

### Query on a windows filesystem

### Scripts

### WSL (Windows Subsystem for Linux)

List all distros installed
```sh
wsl --list
```

Terminate a specific instance of a distro
```sh
wsl --terminate DistroName
```

Fix WSL Clock Drift (might happen sometimes)
```sh
sudo hwclock -s
```