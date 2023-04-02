# SSH (Secure Shell Protocol)

## Table of Contents

- [How does it work ?](#how-does-it-work)
    - [Generate private/public keys](#generate-privatepublic-key)
    - [Public & Private keys mechanism](#public--private-keys-mechanism)
    - [SSH Client & Server connection](#ssh-client--server-connection)
- [SSH useful commands](#ssh-useful-commands)
    - [SSH connection](#ssh-connection)
    - [scp](#scp)
- [FTP & SFTP](#ftp--sftp)

## How does it work ?

### Generate private/public key

The keys are generated in `/home/<user>/.ssh`

```bash
ssh-keygen
```
View of the `/home/<user>/.ssh` folder:
```
.ssh
├── id_rsa
├── id_rsa.pub
└── known_hosts
```
<center>

| Files      |      Content  |
|:-----------|:-------------:|
| id_rsa     |  private key  | 
| id_rsa.pub |  public key   |

</center>

Add a password to an existing key
(Then follow instructions)
```bash
ssh-keygen -p
```

### Public & Private keys mechanism

- The public key is used by the server **to encrypt a message**
- The private key is used the client **to decrypt the message**

![img_1](/networks/ssh/resources/public-private-keys.png)

### SSH Client & Server connection

1. At each and every connection, the client sends his public key to the server.
2. The server matches the client's public key with all the public keys it knows.
3. The server generates a random numbe and sends it in an encrypted message (with the correct public key).
4. The client decrypts the message with the private key and calculates the MD5 hash value of the message. Then it returns the value to the server. The server checks that its value and the client's one are the same.
5. If the values are the same, it means that the client has the corresponding private key. The authentication is complete.

![img_2](/networks/ssh/resources/ssh-client-server.png)

## SSH useful commands

### SSH connection

In order to connect to the server through SSH, you'll need to register your **public key** in the set
of keys known by the server. (*see part above*). After that, you'll be able to connect to the server by typing:

```bash
ssh username@hostname
```

- **username** is your username on the server.
- **hostname** is the name of the server

### scp

To copy a file `from the server to the client's machine`, we can use the **scp** command. It takes 2 arguments : 

1. The path of the server's file we want to copy 
2. The path of the local folder we want to paste the new file
```bash
scp infile outfolder
```

### SSH tunneling

**SSH tunneling** also called **SSH port forwarding** can be used to forwards traffic from a remote server's given port to a local machine's given port (and vice-versa) over an encrypted SSH connection.

It is particularly useful when it comes to protecting services. It allows users to access a distant service **without having to expose associated ports** of the remote server. 

Create a SSH tunnel
```bash
ssh -f -N user@hostname -L localport:hostname:distantport
```

- `-f`: runs ssh in the background (detached process)
- `-N `: specifies that no command should be executed on the remote server
- `-L`: sets up local port forwarding between the two machines

![ssh-tunneling](/networks/ssh/resources/ssh-tunneling.png)

In the diagram above, we can see that connections to a remote server requires to expose specific services ports. However, it is generally not a good practices in terms of security. 

But why is it considered as dangerous to open my ports?

It is because of the following principle: 

- **The robustness of a chain depends on the weakest link**

Each time we open a port for a service, it **allows traffic to flow through that port**. Moreover, if the service running on that port has vulnerabilities or is misconfigured, it could be exploited by hackers **to gain unauthorized access to your server**.

## SFTP

***SFTP*** stands for ***Secure shell File Transfer Protocol***. SFTP is a component of an SSH protocols which aims at transferring files over SSH.

WARNING: It must not be confused with ***FTP*** wich is a proper protocol over *SSL* (*Secure Sockets Layer*). Unlike SFTP, FTP **is not** based on SSH. It uses its own port (Port 20/21)

![img_3](/networks/ssh/resources/sftp-ftp.png)

Here is a quick comparison between FPT and SFTP:

|                         FTP                         |                                                        SFTP                                                        |
|:---------------------------------------------------:|:------------------------------------------------------------------------------------------------------------------:|
|          Uploads data without any security          | Provides full security to the data by relying on the SSH protocol. It also uses SSH keys to provide authentication |
|             Anyone can access the server            |             SFTP can be accessed by only server owner as port 22 is not open in case of shared hosting             |
| Not encrypted because FTP is anonymously accessible |                          Before sending it to another host, SFTP encrypts the information                          |
|                     Uses Port 21                    |                                                    Uses Port 22                                                    |