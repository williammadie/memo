# Introduction

## Table of Contents

- [Useful commands](#useful-commands)
- [OSI Model](#osi-model)

## Basics

```bash
route -n

Table de routage IP du noyau
Destination     Passerelle      Genmask         Indic Metric Ref    Use Iface
0.0.0.0         192.168.7.254   0.0.0.0         UG    0      0        0 enp0s31f6
192.168.0.0     0.0.0.0         255.255.248.0   U     0      0        0 enp0s31f6
```

Here, we can see that the **default gateway** (= 0.0.0.0) redirects to the IP address 192.168.7.254

## OSI Model

The **Open Systems Interconnection Model** is a conceptual model that standardizes the telecommunications at different layers. It was developed in the 1970s because of the numerous diverse computer networking methods. The idea was to homogenize/standardize these methods at a large scale.

The **OSI Model** is a seven-layer model where layers belong to two different classes. Layers from **1 to 3** are called the ***Media layers** and layers from **4 to 7** are called the ***Host layers***

![img_1](/networks/introduction/resources/osi-model.png)