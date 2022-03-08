# Kubernetes

## Table of Contents

- [What is Kubernetes ?](#what-is-kubernetes)
    - [Introduction](#introduction)
    - [Architecture](#architecture)

## What is Kubernetes ?

### Introduction

*Kubernetes*, also called *K8s* is an open-source system for automating deployment, scaling and management of containerized applications. 

### Architecture

Kubernetes is based on a ***Master*** which is charged to schedule, manage and control the ***Worker Nodes***.

![img_1](/networks/kubernetes/resources/kubernetes-general-architecture.png)

The ***Master*** uses an ***API Endpoint*** which is reached by users and then redirects them to the ***Worker Nodes***. These ***Worker Nodes*** designate the containerized application(s).

![img_1](/networks/kubernetes/resources/kubernetes-architecture.png)
