# Computers

## Table of Contents

- [Inspiration](#inspiration)
- [Basics](#basics)
    - [Modern Computer's Architecture](#modern-computers-architecture)
    - [CPU's Language](#cpu-language)
    - [Executing a program](#executing-a-program)
    - [Taking the bus](#taking-the-bus)
    - [The Kernel](#the-kernel)
    - [Privileges](#privileges)
    - [Syscalls](#syscalls)
- [Multitasking](#multitasking)
    - [Preemptive Multitasking](#preemptive-multitasking)
    - [Timeslice Calculation](#timeslice-calculation)
    - [Kernel Preemptability](#kernel-preemptability)
    - [Cooperative Multitasking](#cooperative-multitasking)

## Inspiration

These are my notes taken from the website *cpu.land* so don't be surprised if you see a similar structure, diagrams or even same sentences.

## Basics

### Modern Computer's Architecture

A computer's heart is called a **CPU**. It stands for **Central Processing Unit**. This part is in charge of all computation. It starts running as soon as you start your computer.

A computer also has a main memory bank called **RAM** for **Random Access Memory**. It is a large multi-purpose space which stores all data used by programs actively running on your computer. In a nutshell, a program cannot be launched if it is not loaded into RAM first.

![modern-computers-architecture](/fundamentals/computers/resources/computer-modern-architecture.png)

Don't worry if you don't understand everything on this diagram, we will come back to it later in this lesson.

### CPU Language

A **CPU** understands only one language called `machine code`. It can be in two forms:

1. `binary`: a series of rows of `1` and `0`.
2. `hexadecimal`: a series of `0xAA` where `A` is in `123456789ABCDEF`

In binary, a rows of 8 digits (=bits) is called a **byte**.
In hexadecimal, `0xAA` represents a **byte**.

The first **bytes** represents the **action to make** and the following, the **data** needed to make this action.

This `machine code` can be translated to `assembly code` which is another low-level language more readable for humans.

![cpu-language](/fundamentals/computers/resources/cpu-language.png)

### Executing a program

As we've seen in the first part of the basics, in order to execute a program, the computer has to load **its machine code** first in the RAM. It will then read machine code directly from RAM,instruction after instruction, by using an **instruction pointer**. It it known as the *fetch-execute cycle*.

![fetch-execute-cycle](/fundamentals/computers/resources/fetch-execute-cycle.png)

After executing the instruction, the pointer moves forward to the next instruction. The instruction pointer just keeps getting forward reading instruction after instruction and by doing so it goes through the program. It can't be a twisted journey as some instructions may say "please don't mind these instruction if this condition is valid" or even "please jump to this block of instructions". This allows developers to reuse their code and to use **conditional logic** in their programs.

The **instruction pointer** used by the CPU to read instructions is stored in what is called a **register**. Imagine it as a very small and tight place where the computer can store a single information like a **memory address**. They are very small but extremely fast as they are directly built into the CPU.

### Taking the Bus

**Registers** are **extremely fast storage places** compared to **RAM**, but why is it such a thing?

Take another look at our previous diagram:

![modern-computers-architecture](/fundamentals/computers/resources/computer-modern-architecture.png)

Identify the location of registers and RAM on this diagram. Have you got it? Sweet! Now, as you can see the RAM is distinct from the CPU. They are two separate entities enjoying their lives in their side. However, they always work together. Information stored in the RAM are always traveling back and forth to the CPU. They simply take the bus.

![computer-buses](/fundamentals/computers/resources/computer-buses.png)

Look at the picture above, it is a bit like a big city, there are a lot of buses that transport information. This is marvelous but, as in real life, it takes time to travel. This is why some information have to be stored directly in the CPU's registers.

### The Kernel

An **operating system** is a collection of software that runs on a computer a make all the basic stuff work. It is the essential support for running other software on your computer.

When we talk about the **kernel**, we refer directly to **the core of the operating system**. It is basically the first program launched by the **instruction pointer** at computer boot up. This program has near-full access to your computer's memory, peripherals and other resources and is in charge of running software installed on your computer called **userland programs**.

Most common kernels are:
- Linux: kernel of GNU/Linux operating systems
- XNU: kernel of macOS
- NT Kernel: modern kernel of Windows OS's family

### Privileges

Modern computer architectures can support several **privileges** also called **modes**. These privileges define what a program can or cannot do. Here is what changes between different privileges:

|                **Actions**                | **Kernel/Supervisor Privilege** | **User Privilege** |
|:-----------------------------------------:|:-------------------------------:|:------------------:|
| Full Access to all supported instructions |               YES               |         NO         |
|            Full Access to RAM             |               YES               |         NO         |
|      Unrestricted access to hardware      |               YES               |         NO         |
|                   Users                   |        Kernel and Drivers       |    Applications    |

Note that processors always start with **Kernel Privilege** and after initializing all necessary programs, it switches to **User Privilege**.

### Syscalls

A **syscall** refers to the action made by a userland program when it requests a service from the operating system on which it is executed.

This is a kind of special procedure that lets a program start a transition from **user space** to **kernel space**. So when a syscall is made, the CPU switches from **User Mode** to **Kernel Mode**, executes its instructions and then mades another switch back to **User Mode**. We call this kind of procedures **software interrupts**.

![system-call-explained](/fundamentals/computers/resources/system-call-explained.png)

There are also different kinds of syscalls that can be made:

![syscall-types](/fundamentals/computers/resources/syscall-types.png)

Syscalls can be made using standard libraries which are platform dependent such as *libc* on Unix-like systems and *ntdll.dll* on Windows.

## Multitasking

### Preemptive Multitasking

A CPU is able to handle a lot of programs at the same time. If we take the example of a single-core CPU able to run one instruction at a time, it is still possible to make it run multiple programs at once.

How is it possible? By cycling through running processes and running each time a couple instructions from each one. This way, they can all be responsive and no process is blocking the CPU.

In order to do so, operating systems use task schedulers based on a **timer chips**. These schedulers are able to trigger **hardware interrupts**. The **hardware interrupts** refers to the action of switching to Kernel Mode and jump to some OS code.

This mechanism is called **premptive multitasking** and the interruption is called **preemption**.

![preemptive-multitasking](/fundamentals/computers/resources/preemptive-multitasking.jpg)

### Timeslice Calculation

The duration an OS scheduler allows a process to run before **prempting it** is called a **timeslice**. The simplest way to manage timeslices is to give every process the same timeslice and cycle through tasks in order. This is called *fixed timeslice round-robin* scheduling.

### Kernel Preemptability

Modern kernels, including Linux, are *preemptive kernels*. This means they're programmed in a way that allows kernel code itself to be interrupted and scheduled just like userland processes.

### Cooperative Multitasking

Ancient operating systems, including old macOS and versions of Windows before NT, used another mechanism for achieving multitasking.

Rather than the OS deciding when to preempt programs, the programs themselves would choose to yield to the OS. These explicit yields were the only way for the OS to regain control and switch to the next scheduled process.

It was really easy for malicious or poorly designed programs to freeze the entire operating system. It also has some other inconvenients so the tech world switched to preemptive multitasking a long time ago.
