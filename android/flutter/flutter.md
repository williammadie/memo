# Flutter

## Introduction

Flutter is a framework based on the Dart language. It is a rising language used for building mobile, desktop and web applications from a single code base.

Flutter offers a productive development:

- it allows to quickly reload and see new changes as we code.
- it provides static analysis to find errors without even executing code

## Why does Flutter use the Dart Language

- Dart supports **asynchronous operations** (the computer is able to complete work while waiting for another operation to finish)
    - Fetching data
    - Writing to a database
    - Reading data from a file
- Dart does not use shared-memory threads. Instead it uses **isolates** which are less likely to introduce new errors due to shared-state concurrency.
- Dart is optimized for building UI for each platform
- Dart allows to customize everything


## Isolates

**isolate**: thread that has an event loop that continuously processes events in its own memory space.