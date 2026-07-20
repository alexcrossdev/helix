# Helix Architecture

**Document Version:** 1.0 Draft
**Architecture Version:** Helix ISA v1.0

---

## High-Level Characteristics

| Property               | Value                                              |
| ---------------------- | -------------------------------------------------- |
| ISA Width              | 64-bit                                             |
| Register Width         | 64-bit                                             |
| Address Space          | 64-bit                                             |
| Endianness             | Little-endian                                      |
| Addressable Unit       | Byte                                               |
| Instruction Format     | Fixed-width *(planned)*                            |
| Memory Architecture    | Von Neumann *(shared instruction and data memory)* |
| Privilege Levels       | User and Supervisor *(planned)*                    |
| Floating-Point Support | Planned as an optional extension                   |
| SIMD Support           | Planned as an optional extension                   |

The values marked as **planned** describe the intended direction for Helix ISA v1.0 and may evolve as the specification matures.

---

## Architectural Goals

Helix is designed to:

* Provide a clean and coherent instruction set.
* Eliminate unnecessary historical complexity.
* Maintain predictable and consistent behavior.
* Be straightforward to implement in both software and hardware.
* Support the development of complete computing systems, from firmware to operating systems.
* Encourage experimentation with architectural features while preserving compatibility within a major ISA version.

---

## Architectural Scope

The Helix project encompasses more than the instruction set itself. The long-term ecosystem includes:

* ISA specification
* Assembler
* Linker
* Emulator
* Compiler toolchain
* Hardware implementation
* FPGA implementation
* Operating system
* Development tools
* Documentation and educational materials

Each component is intended to be developed from the specification upward, ensuring that every layer of the system reflects the same architectural principles.

---

## Design Process

The Helix architecture is specified before implementation.

The ISA serves as the authoritative reference for all software and hardware components. Assemblers, emulators, compilers, and processor implementations are expected to conform to the published specification rather than defining behavior independently.

As the architecture evolves, changes will be introduced through versioned revisions of the specification to preserve compatibility and maintain a stable development process.

---

## Future Work

This document provides only a high-level overview of the Helix architecture.

Detailed specifications for registers, memory, instruction encoding, privilege levels, exceptions, calling conventions, and the instruction set are defined in separate documents within the Helix ISA specification.

