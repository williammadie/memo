# Systems

## Table of Contents

- [Primary and Secondary Memory](#primary-and-secondary-memory)

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