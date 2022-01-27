# SSH

## Connection

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

### Public & Private keys mechanism

- The public key is used by the server **to encrypt a message**
- The private key is used the client **to decrypt the message**

![img_1](/ssh/resources/public-private-keys.png)

### SSH Client & Server connection

1. At each and every connection, the client sends his public key to the server.
2. The server matches the client's public key with all the public keys it knows.
3. The server generates a random numbe and sends it in an encrypted message (with the correct public key).
4. The client decrypts the message with the private key and calculates the MD5 hash value of the message. Then it returns the value to the server. The server checks that its value and the client's one are the same.
5. If the values are the same, it means that the client has the corresponding private key. The authentication is complete.

![img_2](/ssh/resources/ssh-client-server.png)

## SSH useful commands

### ssh connection

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