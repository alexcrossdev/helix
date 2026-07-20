# Registers

**Document Version:** 1.0 Draft
**Architecture Version:** Helix ISA v1.0

---

## Overview

The Helix register file provides the processor's fastest storage and forms the primary interface between software and the execution hardware.

All programmer-visible registers are 64 bits wide. Unless otherwise specified, registers may be read from and written to by any instruction that accepts a register operand.

The Helix register model is divided into two categories:

* General-Purpose Registers
* Special-Purpose Registers

---

## General-Purpose Registers

Helix defines **32 general-purpose registers**, named **R0** through **R31**.

Each register is 64 bits wide and is capable of storing integer values, addresses, pointers, or other programmer-defined data.

No general-purpose register has a predefined architectural purpose. All registers are functionally identical.

Future software conventions, such as calling conventions or compiler register allocation, may assign conventional roles to specific registers, but these roles are not enforced by the architecture.

| Register |   Width | Purpose                 |
| -------- | ------: | ----------------------- |
| R0–R31   | 64 bits | General-purpose storage |

---

## Special-Purpose Registers

Helix defines several registers that control processor execution.

### Program Counter (PC)

The Program Counter contains the address of the next instruction to be executed.

Sequential execution advances the Program Counter automatically.

Control flow instructions such as jumps, branches, calls, and returns modify the Program Counter.

---

### Stack Pointer (SP)

The Stack Pointer identifies the top of the active program stack.

The architecture does not require software to use the stack, but standard calling conventions are expected to rely on it for:

* Function calls
* Local variables
* Register preservation
* Temporary storage

---

### Status Register (FLAGS)

The Status Register records the results of selected arithmetic and logical operations.

The initial version of Helix defines the following status flags:

| Flag | Meaning         |
| ---- | --------------- |
| Z    | Zero result     |
| N    | Negative result |
| C    | Carry generated |
| V    | Signed overflow |

Additional status bits may be introduced in future architecture revisions.

---

## Register Width

All architectural registers are 64 bits wide.

Operations on smaller integer types affect only the defined portion of the destination register. The behavior of partial-width operations is specified by the instruction set.

---

## Reset State

Following processor reset:

* The initial value of the Program Counter is implementation-defined.
* The initial Stack Pointer is implementation-defined.
* General-purpose register contents are unspecified unless initialized by system software.
* The Status Register is initialized to a processor-defined reset state.

The boot environment is responsible for establishing the initial execution context.

---

## Architectural Notes

The Helix ISA intentionally avoids assigning fixed architectural roles to general-purpose registers.

This design provides flexibility for operating systems, compilers, and language runtimes while maintaining a simple and uniform programming model.

Software conventions may define register usage without requiring changes to the architecture itself.

