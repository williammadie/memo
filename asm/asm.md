# Assembly Language

## Table of Contents

## Introduction

## Registers

The Assembly Language works using **registers** which are **very small storage containers located inside the CPU**. Registers are the fastest way to access data for the CPU as it is located directly inside it. By doing so, the CPU is much faster as it does not need to send the data request across the control bus and into the **memory storage unit**.

However, registers number is very limited as they are directly built into the processor chip which is a very small element with a limited space.

In IA-32 (Intel Architecture 32bits), there are:
- 32bits registers x10
- 16bits registers x6

Registers are grouped into different groups depending on their main function:
- General registers
    - Data registers
    - Pointer registers
    - Index registers
- Control registers
- Segment registers

### Data Registers

4 32bits registers are used for arithmetic, logical and other operations:
- %eax
- %ebx
- %ecx
- %edx

They can be used completely or halfly.

- %esi
- %edi
- %ebp
- %esp

## Main Instructions


`