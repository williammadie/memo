# Systems

## Table of Contents

- [Primary and Secondary Memory](#primary-and-secondary-memory)
- [Buffering](#buffering)

## Primary and Secondary Memory

(The words `storage` and `memory` refers to the same concept and are often used interchangeably. For this lesson, I use `memory`.)

- *Primary Memory*: fast, volatile memory used by the CPU to store data and instructions that are currently used by the computer.
- *Secondary Memory*: slow, non-volatile memory used for long-term storage of data and instructions not currently used by the computer.

In a nutshell, the difference between primary and secondary lies on whether the CPU **has a direct access to the memory**, the **speed of the memory** and whether it is **volatile or not**.

![primary-secondary-storage](/systems/resources/primary-secondary-storage.png)

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

![buffering-operating-systems](/systems/resources/buffering-operating-systems.png)

### Concrete example n°1 in C

A more concrete example (in C language) would be to write data to a file using the `fprintf()` function.

As **writing to a file is a very slow process due to the physical limitations of disk I/O**, writing direclty to a file would slow the whole program. In this case, it improves the global **performance of the program to first store the data in a buffer in memory**.

Additional Note: In the above case, we might want to ensure that all data has been writen to our file and that nothing is left behind in the buffer. We are going to use the `fflush()` function to **flush (=empty) the buffer associated with our stream operation**

### Concrete example n°2 in C

Another example is when the program asks for a user input by using the `scanf()` function. This function will stop reading input as soon as it encounters a `space`, `tab` or `newline`. However, any remaining characters will be left in the input buffer.

This means that if we call `scanf()` another time after the user wrote `hello world\n` the first time. The `\n` will be stuck inside the buffer and on the second call of `scanf()`, the program will immediately read `\n` and will not let the user writes anything.

So in this case, it is mandatory to use `fflush(stdin)` to empty the buffer before proceeding to another input.