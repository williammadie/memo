# Kubernetes

## Table of Contents

- [What is Kubernetes ?](#what-is-kubernetes)
    - [Introduction](#introduction)
    - [Architecture](#architecture)
- [Commands](#commands)

## What is Kubernetes ?

### Introduction

*Kubernetes*, also called *K8s* is an open-source system for automating deployment, scaling and management of containerized applications. 

### Architecture

Kubernetes is based on a ***Master*** which is charged to schedule, manage and control the ***Worker Nodes***.

![img_1](/networks/kubernetes/resources/kubernetes-general-architecture.png)

The ***Master*** uses an ***API Endpoint*** which is reached by users and then redirects them to the ***Worker Nodes***. These ***Worker Nodes*** designate the containerized application(s).

![img_1](/networks/kubernetes/resources/kubernetes-architecture.png)

## Commands

### Nodes

Get Node resources
```bash
kubectl get node -A
```

List all available resources
```bash
kubectl api-resources
```

View details about a resource
```bash
kubectl describe kind/name
```

View the definition for a resource type with:
```bash
kubectl explain kind
```

### Services

List the services on our cluster
```bash
kubectl get services -A
```

### Pods

Pods are groups of containers. They are running together (on the same node) and are sharing resources (RAM, CPU, Network, Volumes).

List all pods
```bash
kubectl get pods
```

### Namespaces

Namespaces are used in order to segregate resources.

List all namespaces
```bash
kubectl get namespaces
```

List the pods in a specific namespace
```bash
kubectl -n my_namespace get pods
```