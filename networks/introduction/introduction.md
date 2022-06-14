# Introduction

## Table of Contents

- [Useful commands](#useful-commands)
- [OSI Model](#osi-model)

## Useful Commands

### Routing

```bash
route -n

Table de routage IP du noyau
Destination     Passerelle      Genmask         Indic Metric Ref    Use Iface
0.0.0.0         192.168.7.254   0.0.0.0         UG    0      0        0 enp0s31f6
192.168.0.0     0.0.0.0         255.255.248.0   U     0      0        0 enp0s31f6
```

Here, we can see that the **default gateway** (= 0.0.0.0) redirects to the IP address 192.168.7.254

### Netcat

**Netcat** is a very useful networking tool. It can be used in Cybersecurity for defending or attacking a network. It can also be used in Web Development for quickly setting up an echo server for instance.

Common commands include:

Setting up an **echo server**
```bash
nc -l 9999
# OR
nc -l localhost 9999
```

Communicating with the **echo server**
```bash
nc server_ip_address 9999
# then it will let you input what you want
```


Transfering a file to a server
Scanning Port on a distant machine
Checking whether a given port is open or not

### Curl

**Curl** is a short for **Client for URLs**. It is a command line tool used for transferring data using various protocols. It is very useful in Web Development and more specificaly APIs development for quickly testing HTTP requests.

Send a GET request
```bash
curl -X GET https://www.site-web.com
# OR (get is default so it can be removed)
curl https://www.site-web.com
```

Send a POST request
```bash
curl -X POST https://www.site-web.com
```

Send a PUT (=UPDATE) request
```bash
curl -X PUT https://www.site-web.com
```

Send a DELETE request
```bash
curl -X DELETE https://www.site-web.com
```


## OSI Model

The **Open Systems Interconnection Model** is a conceptual model that standardizes the telecommunications at different layers. It was developed in the 1970s because of the numerous diverse computer networking methods. The idea was to homogenize/standardize these methods at a large scale.

The **OSI Model** is a seven-layer model where layers belong to two different classes. Layers from **1 to 3** are called the ***Media layers** and layers from **4 to 7** are called the ***Host layers***

![img_1](/networks/introduction/resources/osi-model.png)