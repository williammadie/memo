# Software Architecture

## Table of Content

## Introduction

Software Architecture consists of "tiers" (= layers)

## Application Layers

### Presentation Layer

### Application Layer

### Data Layer

## DBMS Architecture (DataBase Management System)

### One-Tier Architecture

One-Tier applications refer to **Standalone applications**. The kind of applications regroups all the **application layers** in a single package. The data is stored in the local system or a shared drive.

Here the Database is directly available to the user. It is generally used for development of local application but **not in production**.

There is a single tier regrouping Presentation, Application and Business Layers.

![one-tier](/architecture/resources/one-tier.png)

**Aditional Note**: The discontinuous lines represent a same machine or Docker container.

### Two-Tier Architecture

It refers to the basic **client-server** architecture. Applications on the client end can directly communicate with the database at the server side.
- User Interface: Client-side
- Application Programs: Client-side
- Query Processing/Transaction Management: Server-side

So, there are two tiers:
1. Client Tier (Presentation + Application Layers)
2. Data Tier (Database Layer)

![one-tier](/architecture/resources/two-tier.png)

### Three-Tier Architecture

This is the basic architecture for Web applications. It is made of three tiers:

1. Client Tier (Presentation Layer)
2. Business Tier (Application Layer)
3. Database Tier (Database Layer)

![one-tier](/architecture/resources/three-tier.png)

### N-Tier Architecture

This layer is known as the **Distributed Application** architecture. It is similar to the **Three-Tier** Architecture but the number of **Application servers** is increased in order to distribute the business logic.

It is used in order to handle massive concurrency usage:

For instance, an massively used mobile application will communicate with **n** instances of a REST API in order to balance the load. 