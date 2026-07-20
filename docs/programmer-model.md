# Programmer's Model

**Document Version:** 1.0 Draft
**Architecture Version:** Helix ISA v1.0

---

## Overview

The Helix Programmer's Model defines the architectural state that is visible to software executing on a Helix processor. It describes the registers, memory, execution state, and system resources that may be accessed directly or indirectly through the instruction set.

The Programmer's Model provides a stable interface between software and hardware. All compliant Helix implementations must present the same architectural state to software, regardless of their internal implementation.

---

## Execution Model

Helix executes programs as a sequential stream of instructions.

For each instruction, the processor conceptually performs the following steps:

1. Fetch the next instruction from memory.
2. Decode the instruction.
3. Read any required operands.
4. Execute the requested operation.
5. Write results back to the architectural state.
6. Advance the Program Counter or transfer control to a new location.

Implementations may internally optimize or reorder operations provided that the architectural behavior observed by software remains identical.

---

## Programmer-Visible State

Software executing on a Helix processor has access to the following architectural resources:

* General-purpose registers
* Program Counter (PC)
* Stack Pointer (SP)
* Status Register (FLAGS)
* Main memory
* Privilege level

The detailed behavior of each resource is specified in later documents.

---

## Register Model

Helix provides a set of 64-bit programmer-visible registers used for arithmetic, logical operations, addressing, and control flow.

Registers are classified into:

* General-purpose registers
* Control registers
* Status registers

The complete register specification is defined in **registers.md**.

---

## Memory Model

Helix presents memory as a linear, byte-addressable address space.

Instructions and data share the same memory space (Von Neumann architecture).

Software interacts with memory through explicit load and store instructions.

The detailed memory model is specified in **memory.md**.

---

## Instruction Execution

Every instruction operates on the current architectural state.

Instructions may:

* Read registers
* Modify registers
* Access memory
* Update status flags
* Transfer program control

Unless explicitly stated, instructions do not produce hidden side effects.

---

## Program Counter

The Program Counter (PC) identifies the address of the next instruction to be executed.

Sequential execution advances the Program Counter automatically.

Control flow instructions may modify the Program Counter directly.

---

## Stack

Helix provides a dedicated Stack Pointer (SP) for managing stack memory.

The stack is intended for:

* Function calls
* Local variables
* Register preservation
* Temporary storage

The exact stack behavior and calling convention are defined separately.

---

## Status Register

The processor maintains a status register that records information about the results of selected operations.

Typical status information includes:

* Zero
* Carry
* Overflow
* Negative

Additional status bits may be defined in future revisions.

---

## Privilege Levels

Software executes within a privilege level that determines access to protected architectural resources.

Helix ISA v1.0 defines two execution modes:

* User Mode
* Supervisor Mode

Additional privilege levels may be introduced through future architecture revisions.

---

## Exceptions and Interrupts

Execution may be interrupted by synchronous exceptions or asynchronous interrupts.

These events transfer control to privileged software.

Their detailed behavior is defined in the Exceptions specification.

---

## Architectural Compatibility

Any implementation that exposes the programmer-visible state defined by this document and follows the Helix ISA specification is considered architecturally compatible, regardless of its internal microarchitecture.

Processors may differ in implementation details such as pipelining, caching, or execution units while remaining fully compatible with Helix software.

