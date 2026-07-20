# Instruction Encoding

**Document Version:** 1.0 Draft
**Architecture Version:** Helix ISA v1.0

---

# Overview

The Helix instruction encoding defines the binary representation of every instruction executed by the processor.

Helix ISA v1.0 uses **fixed-width 32-bit instructions**. Every instruction occupies exactly one 32-bit word in memory regardless of its operation.

A fixed-width encoding simplifies instruction decoding, improves implementation clarity, and provides a consistent programming model.

---

# Bit Numbering

Instruction bits are numbered from most significant to least significant.

```text
31                             0
+-------------------------------+
|         Instruction           |
+-------------------------------+
```

---

# Register Encoding

Helix defines **32 general-purpose registers**.

Each register is encoded using **5 bits**.

| Register | Encoding |
| -------- | -------: |
| R0       |    00000 |
| R1       |    00001 |
| ...      |      ... |
| R31      |    11111 |

---

# Instruction Formats

Helix defines several standard instruction formats.

Each format is optimized for a specific class of instructions while maintaining a consistent layout.

---

# R-Type (Register)

Used for arithmetic and logical instructions operating entirely on registers.

```text
31          24 23   19 18   14 13   9 8        0
+-------------+-------+-------+------+----------+
| Opcode (8)  |  Rd   | Rs1   | Rs2  | Func (9) |
+-------------+-------+-------+------+----------+
```

| Field  | Size | Description                           |
| ------ | ---: | ------------------------------------- |
| Opcode |    8 | Primary instruction identifier        |
| Rd     |    5 | Destination register                  |
| Rs1    |    5 | First source register                 |
| Rs2    |    5 | Second source register                |
| Func   |    9 | Operation variant or future extension |

---

# I-Type (Immediate)

Used for instructions containing an immediate constant.

```text
31          24 23   19 18   14 13                0
+-------------+-------+-------+------------------+
| Opcode (8)  |  Rd   | Rs1   | Immediate (14)   |
+-------------+-------+-------+------------------+
```

---

# M-Type (Memory)

Used for load and store instructions.

```text
31          24 23   19 18   14 13                0
+-------------+-------+-------+------------------+
| Opcode (8)  | Reg   | Base  | Offset (14)      |
+-------------+-------+-------+------------------+
```

Where:

* **Reg** identifies the source or destination register.
* **Base** contains the base memory address.
* **Offset** is added to the base register to form the effective address.

---

# B-Type (Branch)

Used for conditional branches.

```text
31          24 23   19 18   14 13                0
+-------------+-------+-------+------------------+
| Opcode (8)  | Rs1   | Rs2   | Offset (14)      |
+-------------+-------+-------+------------------+
```

The branch target is computed by adding the signed offset to the current Program Counter.

---

# J-Type (Jump)

Used for unconditional jumps and function calls.

```text
31          24 23                               0
+-------------+----------------------------------+
| Opcode (8)  |   Signed Offset (24)             |
+-------------+----------------------------------+
```

The target is PC-relative, so taget = PC + offset

---

# JR-Type (Jump Register)

Used for unconditional jumps and function calls using a register address.

```text
31          24 23   19 18                          0
+-------------+-------+--------------------------+
| Opcode (8)  | Rs1   | Offset (19)              |
+-------------+-------+--------------------------+
```

The target is Rs1 + Offset.

---

# Opcode Space

The 8-bit opcode field provides **256 primary instruction encodings**.

Opcode allocation is organized by instruction category.

| Range     | Purpose                      |
| --------- | ---------------------------- |
| 0x00–0x1F | Arithmetic                   |
| 0x20–0x3F | Logical                      |
| 0x40–0x5F | Memory                       |
| 0x60–0x7F | Branch                       |
| 0x80–0x9F | Jump                         |
| 0xA0–0xBF | System                       |
| 0xC0–0xFF | Reserved / Future Extensions |

---

# Immediate Values

Immediate fields are interpreted according to the instruction definition.

Unless otherwise specified:

* Integer immediates are sign-extended.
* Unsigned immediates are explicitly identified by the instruction.
* Offsets are interpreted as signed values.

---

# Reserved Encodings

Instructions with undefined opcodes or invalid field combinations are reserved.

Execution of a reserved encoding shall generate an Illegal Instruction exception.

---

# Future Extensions

Additional instruction formats may be introduced in future versions of the Helix ISA.

Existing instruction formats shall remain backward compatible within the same major architecture version.

