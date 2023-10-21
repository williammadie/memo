# Quarkus

## Table of Contents

- [What is Quarkus](#what-is-quarkus)
- [Quarkus CLI](#quarkus-cli)
- [Historical Details](#historical-details)
    - [Java SE, Java EE and Jakarta EE](#java-se-java-ee-and-jakarta-ee)
    - [Spring and Quarkus](#spring-and-quarkus)
- [What is New](#what-is-new)
    - [Build Time Processing](#build-time-processing)
    - [Embedded Healthchecks](#embedded-healthchecks)

## What is Quarkus

As modern frameworks do, Quarkus is centered around **performance**, **cloud-native support**, **micro-services** and **developer experience**.

As it is said on Quarkus official webpage: Quarkus applications are optimized for **low memory usage** and **fast startup times**.

## Arc Framework

Quarkus uses the `Arc` framework for implementing **CDI** (**Content Dependency Injection**).

## Quarkus CLI

Launch Quarkus Application with Hot reload and Dev UI
```bash
quarkus dev
```

Add an extension to `pom.xml`
```bash
quarkus extension add camel-quarkus-jackson
```

## Historical Details

### Java SE, Java EE and Jakarta EE

(history of all specifications)

### Spring and Quarkus

(history of both frameworks)

### What is New

### Build Time Processing

The central idea behind Quarkus is to do **at build-time what traditional frameworks do at runtime**:
- configuration parsing
- classpath scanning
- feature toggle based on classloading
- ...

In comparison to Spring, Quarkus does more checks at compiling/build time. For instance, it checks the validity of the `application.properties` file at compiling time.

### Embedded Healthchecks

In Quarkus, runtime capabilities such as **health checks** and **metrics** are exposed out of the box.

We only need to add the `smallrye-health` extension (see [Quarkus Smallrye Health](https://quarkus.io/guides/smallrye-health))