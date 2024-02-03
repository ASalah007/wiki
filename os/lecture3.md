# Lecture 3

# Multi Level Feedback Queue (MLFQ) Scheduling policy

There are many queues with different priorities.

## Rules

1. if priority of job A > priority of B, then A run and B doesn't.
2. if priority of A == priority of B, then we will round robin over them.
3. every new process has the highest priority.
4. if process uses time slice at given priority, at the end of time slice move down one level.
5. every **T** seconds move all processes to the highest priority.

## Parameters

1. N: Queues Number
2. Q: Quantum length
3. T: reset Interval

# Virtual Memory

## Process

a process is a running program with its own address space.

Process:

- Registers
- Memory (virtual address space):
  - Code
  - heap
  - stack

Memory Access happens when:

- Instruction Fetch
- Explicit Memory Access (load/store)

## Requirements

1. provide abstraction of large memory to each process
2. protect processes from each other
3. protect processes from the OS

## Solutions

### 1. Address Translation

on each memory access, translate virtual address to physical address.

#### Dynamic Relocation (Base and Bound)

in the cpu there is a memory management unit (mmu), which contains 2 registers: base and bound.
their values comes from each process's pcb (process control block)

when a process is running, the mmu will translate the virtual address to physical address by adding the base to the virtual address.

`Physical Address = Base Address + Virtual Address (as long it is within the bound limit)`

## Fragmentation

fragmented memory is free memory but it is distributed among the memory

defragmentation is the process of moving the process used memory beside
each other, so that we can use the free memory as one block of memory.

## Segmentation

multiple base and bound registers per process for each logical part of
the address space (stack, heap, code, ...)
