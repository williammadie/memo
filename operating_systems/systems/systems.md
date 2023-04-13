# Systems

## Table of Contents

- [Computer Architecture in a Nutshell](#computer-architecture-in-a-nutshell)
- [Primary and Secondary Memory](#primary-and-secondary-memory)
- [Buffering](#buffering)
- [Synchronous and Asynchronous Operations](#synchronous-and-asynchronous-operations)

## Computer Architecture in a Nutshell

Today's computers use the **Von Neumann Architecture**. It was the idea of the Physician and Mathematician *John Von Neumann* to separate the ALU and the Control Unit that gave birth to this architecture.

![von-neumann-architecture](/operating_systems/systems/resources/von-neumann-architecture.png)

1. The CPU

**CPU** (**Central Processing Unit**): It is the brain of the computer, the place where arithmetic and logic is handled. It can take an instruction in input and execute it to create an output.

- **Control Unit**: CPU Unit charged of instructions sequencing. It accepts external instructions (= input) and turns them into a series of **control signals**.
- **ALU** (**Arithmetic Logic Unit**): CPU Unit charged of arithmetic calculations and logic handling.
- **Registers**: Data holding places part of the CPU. They are used for transfering data for immediate use by the CPU.
- **MMU** (**Memory Management Unit**): CPU Unit charged of transferring data from the RAM to the CPU or to from the Cache Memory to the CPU (if it is present in the Cache). 
- **Cache Memory**: CPU memory unit typically located on the CPU chip but separated from the CPU's processing units

2. Data Bus

**Data Bus**: Set of wires or electronic connectors that provide transportation for data between one component to another on a motherboard.

It is typically very slow compared to CPU speed. This is the reason why there are registers and also a Cache memory unit inside the CPU (which are a lot faster than taking the bus) 

3. RAM

**Random Access Memory**: It is better to refer to it as **Direct Access Memory**, a memory space where data is organized by addresses and where CPU can access a specific information by asking a given memory address.

It is considered as really fast compared to the secondary memory (HDD, SSD, USB Key...) but really slow compared to the CPU speed.

## Primary and Secondary Memory

(The words `storage` and `memory` refers to the same concept and are often used interchangeably. For this lesson, I use `memory`.)

- *Primary Memory*: fast, volatile memory used by the CPU to store data and instructions that are currently used by the computer.
- *Secondary Memory*: slow, non-volatile memory used for long-term storage of data and instructions not currently used by the computer.

In a nutshell, the difference between primary and secondary lies on whether the CPU **has a direct access to the memory**, the **speed of the memory** and whether it is **volatile or not**.

![primary-secondary-storage](/operating_systems/systems/resources/primary-secondary-storage.png)

The **MMU** is the CPU component that indicates to the CPU if the data is stored inside the Cache Memory or the Secondary Memory. The difference is important as in the second case, the data has to go through the **Data Bus** which is significantly slower than the **CPU speed**

Below, you'll find a short summary of all types of available memories. I added a category **Off-line Memory** which is basically a subpart of **Secondary Memory**

|     **Type of Memory**     |            **Specific Elements**           |                                                                                                      **Description**                                                                                                     |
|:--------------------------:|:------------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|     Primary/Main Memory    |                CPU Registers               |                                                                           A very small amount of high-speed memory located inside the CPU chip                                                                           |
|     Primary/Main Memory    |                Cache Memory                |                                                          Slightly slower memory typically located on the CPU chip but separated from the CPU's processing units                                                          |
|     Primary/Main Memory    |         RAM (Random Access Memory)         | The most common type of primary memory. It is used to store data and instructions currently being used by the CPU. ("Random" here means "Direct". It is completely misleading as there is no actual "random" operations) |
|     Primary/Main Memory    |           ROM (Read Only Memory)           |                      A type of non-volatile memory used to store permanent data and instructions that are not designed to be changed. It is typically used to store the computer's firmware or BIOS                      |
| Auxiliary/Secondary Memory |      Internal SSD (Solid State Drive)      |                                                                     A type of flash memory storage device that is faster and more durable than HDDs.                                                                     |
| Auxiliary/Secondary Memory |       Internal HDD (Hard Disk Drive)       |                                                              A type of magnetic storage device that is used for long-term storage of data and instructions.                                                              |
|       Off-line Memory      |         USB (Universal Serial Bus)         |                                                                           A small portable storage device that use flash memory to store data.                                                                           |
|       Off-line Memory      | Optical Drives (CD, DVD, Blu-ray Discs...) |                                                            A type of storage device that uses lasers to read and write data from CDs, DVDs and Blu-ray Discs.                                                            |
|       Off-line Memory      |                  SD Cards                  |                                                      A small, removable memory card that is commonly used in digital cameras, smartphone and other portable devices.                                                     |
|       Off-line Memory      |               External HDD...              |                                                              A type of magnetic storage device that is used for long-term storage of data and instructions.                                                              |

## Buffering

- **Buffer**: area in the man memory used to store or hold the data temporarily while it is being moved from one place to another.
- **Buffering**: the act of storing data temporarily in the buffer.

A buffer can be used between *2 devices or 2 processes*. It is typically used **when there is a difference between the rate of received data and the rate of processed data**. Is is typically the case for I/O operations (Input/Output).

Some examples of **I/O operations**:
- Write to a file or to the standard/error output
- Read characters from standard input

Here is a quick view of how it could work for 2 processes:

1. P1 waits until the buffer is empty.
2. P1 writes data to the buffer.
3. P2 waits until the buffer is not empty.
4. P2 reads data from the buffer.

![buffering-operating-systems](/operating_systems/systems/resources/buffering-operating-systems.png)

### Concrete example n°1 in C

A more concrete example (in C language) would be to write data to a file using the `fprintf()` function.

As **writing to a file is a very slow process due to the physical limitations of disk I/O**, writing direclty to a file would slow the whole program. In this case, it improves the global **performance of the program to first store the data in a buffer in memory**.

Additional Note: In the above case, we might want to ensure that all data has been writen to our file and that nothing is left behind in the buffer. We are going to use the `fflush()` function to **flush (=empty) the buffer associated with our stream operation**

### Concrete example n°2 in C

Another example is when the program asks for a user input by using the `scanf()` function. This function will stop reading input as soon as it encounters a `space`, `tab` or `newline`. However, any remaining characters will be left in the input buffer.

This means that if we call `scanf()` another time after the user wrote `hello world\n` the first time. The `\n` will be stuck inside the buffer and on the second call of `scanf()`, the program will immediately read `\n` and will not let the user writes anything.

So in this case, it is mandatory to use `fflush(stdin)` to empty the buffer before proceeding to another input.

## Synchronous and Asynchronous Operations

