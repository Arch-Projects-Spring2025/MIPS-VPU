# MIPS-VPU

### SIMD-Enabled MIPS Processor with 128-bit Vector Extensions

A custom MIPS processor extended with a dedicated Vector Processing Unit (VPU) capable of executing SIMD operations on 128-bit vectors.

This project was developed as part of the Computer Architecture course at Sharif University of Technology and explores how vector processors accelerate data-parallel workloads by performing multiple arithmetic and logical operations simultaneously.

---

## Overview

Traditional scalar processors execute a single operation on a single data element at a time.

The MIPS-VPU extends a standard MIPS architecture with:

* A dedicated 128-bit vector register file
* Parallel vector arithmetic units
* Vector memory operations
* Scalar-to-vector data transfer instructions
* Extended control logic for vector execution

The design enables Single Instruction Multiple Data (SIMD) execution, allowing multiple values to be processed in parallel within a single clock cycle.

---

## Architecture

### Scalar Core

The processor retains the standard MIPS datapath:

* Program Counter
* Instruction Memory
* Register File
* ALU
* Data Memory
* Control Unit

### Vector Extension

The vector subsystem introduces:

* 8 Vector Registers (V0–V7)
* 128-bit register width
* Dedicated Vector Register File
* Vector ALU
* Vector Memory Interface
* Scalar ↔ Vector transfer mechanism

Each vector register consists of four 32-bit lanes:

```text
V0 = [R0 | R1 | R2 | R3]
V1 = [R4 | R5 | R6 | R7]
...
V7 = [R28 | R29 | R30 | R31]
```

---

## Supported Vector Operations

### 32-bit SIMD Instructions

* VADD32
* VSUB32
* VMUL32

Each instruction performs four parallel 32-bit operations.

Example:

```text
A = [1, 2, 3, 4]
B = [5, 6, 7, 8]

VADD32(A, B)

Result:
[6, 8, 10, 12]
```

---

### 16-bit SIMD Instructions

* VADD16
* VSUB16
* VMUL16

These instructions operate on eight parallel 16-bit values packed into a 128-bit vector.

---

### Vector Logical Instructions

* VAND
* VOR
* VXOR

Bitwise logical operations are executed simultaneously on all vector lanes.

---

## Vector Memory System

The memory subsystem supports both:

### Scalar Access

```text
Load 32-bit
Store 32-bit
```

### Vector Access

```text
Load 128-bit
Store 128-bit
```

The processor can transfer an entire vector register between memory and the vector register file in a single operation.

---

## Scalar ↔ Vector Communication

Two dedicated instructions are implemented:

### TOCOP

Transfers a scalar register into a selected vector lane.

### FROMCOP

Transfers a selected vector lane back into the scalar register file.

These instructions allow seamless cooperation between scalar and vector execution.

---

## Control Unit Extensions

The original MIPS control unit was extended with new control signals:

* RegWriteV
* RegDstV
* ToCop
* FromCop
* IsVStore

Additional memory control modes were introduced to distinguish between:

| Mode | Operation     |
| ---- | ------------- |
| 0    | Read 32-bit   |
| 1    | Write 32-bit  |
| 2    | Read 128-bit  |
| 3    | Write 128-bit |

---

## Key Features

* 128-bit SIMD execution
* Parallel arithmetic units
* Parallel logical units
* Dedicated vector register file
* Vector memory operations
* Scalar/vector interoperability
* Modular Logisim implementation
* Educational exploration of vector processor design

---

## Technologies

* Logisim Evolution
* MIPS ISA
* SIMD Architecture
* Vector Processing
* Digital Logic Design

---

## Authors

* Sobhan Aghasi Zadeh
* Parmis Hemasian
* Nima Kahdenarouei
* Fatemeh Tamehri

Sharif University of Technology
Computer Architecture Course
