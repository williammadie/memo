# Rust

## Table of Contents

- [Introduction](#introduction)
- [The Power of Rust](#the-power-of-rust)
- [Cargo CLI](#cargo-cli)
- [Simple Project Structure](#simple-project-structure)
- [Variables](#variables)
- [Shadowing](#shadowing)
- [Constants](#constants)
- [Comments](#comments)
- [Functions](#functions)
- [Macros](#macros)

## Introduction

Rust was born in 2006. It has been developed by the developer **Gradyon Hoare** as a personal project while working at **Mozilla Research**. Mozilla started to oficially sponsor the project in 2009.

As it is often said, the goal of Rust is to write code that can sit there and run reliably for decades. It is made possible thanks to Rust's major assets:

![rust-assets](/programming_languages/rust/resources/rust-assets.png)

Obviously, Rust is a very special language and can't always be used because of its complexity. As development is more expensive in Rust, projects made/reworked in Rust need to be chosen for a very good reason.

For instance, it could be that Typescript is too restrictive or unstable for a specific need or something else.

Based on the explanation of **Theo - t3.gg** on YouTube, Rust should be used when the code base doesn't need to be changed often. 

![use-rust](/programming_languages/rust/resources/use-rust.png)

## The Power of Rust

The Power of the Rust PL relies in its **compiler** which is very very very strict. Its goal is to put some **guardrails** in order to enforce **safe code writing**. It is basically there to ensure that compiled Rust code does not have vulnerabilities.

The compiler plays a **gatekeeper role**. The Rust experience focuses on detecting bug before runtime.

## Cargo CLI

**Cargo** is the Rust build tool and package manager. It can be used inside a terminal to build, run, test, publish a library to creates.io.

```bash
cargo --version
```

create a new project
```bash
cargo new my-project-name
```

build your project (for development purposes)
```bash
cargo build
```

check your code (= embedded linter)
```bash
cargo check
```

run your project
```bash
cargo run
```

test your project
```bash
cargo test
```

build the project's documentation
```bash
cargo doc
```

build your project (with optimization for release)
```bash
cargo build --release
```

publish a library to crates.io
```bash
cargo publish
```

## Simple Project Structure

```bash
my-project/
├── Cargo.toml
└── src
     └── main.rs
```

- `Cargo.toml`: Manifest file for Rust. It stores **project metadata** and **project dependencies**
- `src/main.rs`: Entry point of the application

run the project
```bash
cargo run
```

## Comments

```rust
// Single-line comment

// Multi-line
// comment
```

## Variables

In Rust, variables are `immutable` by default. Rust documentation says **safety** is the primary reason behind this choice of implementation. Moreover, by doing so, the compiler is able to detect when you try to modify an immutable object and can prevent you from doing it.

Reminder: `immutable` means `whose state cannot be changed after creation`.

Declare and initialize an immutable variable
```rust
let x = 4;
```

Declare and initialize a mutable variable
```rust
let mut x = 4;
```

## Shadowing

Shadowing is the concept of declaring a new variable with the same name as a previous variable. The first variable is `shadowed` by the second.

In the following example, outside of the block, `x` is equal to `5` then it is equal to `10` inside the block and when it reaches the end of the scope `{}`, it goes back to `5`
```rust
let x: i32 = 5;
{
    let x = x * 2;
    println!("The value of x is: {x}");
}
println!("The value of x is: {x}");
```

## Constants

Constants are `immutable` by default. The keyword `mut` cannot be used with them.

Declare a constant
```rust
const MY_CONSTANT: u32 = 60 * 60;
```

## Functions

```rust
fn main() {
    // do work
}
```

## Macros

Rust macros are called with `!`. For instance, `println!()` does not call a function but a macro.

Macros don't always follow the same rules as functions.