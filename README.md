#  MIPS Vector-Extended Processor Architecture

### A SIMD-Enabled Vector Extension for a Single-Cycle MIPS Processor

MIPS-VPU is a custom vector-processing extension built on top of a single-cycle MIPS processor. The project introduces a dedicated 128-bit vector register file, a vector arithmetic and logic unit, vector memory operations, and new instructions for transferring data between scalar and vector registers.

Developed as part of the Computer Architecture course at Sharif University of Technology, this project explores the principles of SIMD (Single Instruction Multiple Data) execution and vector processor design.

---

## Overview

The original processor is a standard single-cycle MIPS implementation. The architecture is extended with a second register file and a dedicated vector execution unit capable of operating on 128-bit values.

The system supports:

* 128-bit vector registers
* Vector arithmetic operations
* Vector logical operations
* Vector memory accesses
* Scalar-to-vector data transfer
* Vector-to-scalar data transfer
* Extended control signals and datapath components

The goal of the design is to perform multiple arithmetic operations in parallel while maintaining compatibility with the original scalar processor.

---

## Architecture

The processor consists of two major execution domains:

### Scalar Processor

The original MIPS processor remains responsible for:

* Instruction Fetch
* Instruction Decode
* Register Access
* Scalar Arithmetic Operations
* Memory Address Computation
* Control Flow Instructions

### Vector Processing Unit (VPU)

The vector subsystem adds:

* Dedicated Vector Register File
* 128-bit Vector ALU
* Vector Memory Interface
* SIMD Arithmetic Units
* SIMD Logical Units

The vector hardware operates alongside the scalar processor and is controlled through new vector instructions.

---

## Vector Register File

The vector register file contains:

```text
8 Vector Registers
V0 ... V7
```

Each vector register stores:

```text
128 bits
= 4 × 32-bit values
```

The implementation maps vector registers onto groups of four scalar-sized elements:

```text
V0 = [R0, R1, R2, R3]
V1 = [R4, R5, R6, R7]
...
V7 = [R28, R29, R30, R31]
```

The vector register file supports:

* Reading entire vectors
* Writing entire vectors
* Partial scalar updates through transfer instructions

Vector register selection uses a 3-bit address.

---

## Scalar–Vector Transfer Instructions

Two special instructions are implemented to exchange data between the scalar processor and the vector register file.

### TOCOP

Transfers a scalar value into a selected lane of a vector register.

This instruction enables scalar values to be inserted into vector registers before SIMD execution.

### FROMCOP

Transfers a selected lane from a vector register back into the scalar register file.

This instruction allows results produced by vector instructions to be used by scalar code.

---

## Vector Memory System

The memory subsystem was redesigned to support both scalar and vector accesses.

### Scalar Memory Operations

```text
Load 32-bit
Store 32-bit
```

### Vector Memory Operations

```text
Load 128-bit
Store 128-bit
```

The memory design allows an entire vector to be transferred between memory and the vector register file in a single operation.

To support vector accesses, the original memory hierarchy was extended with 128-bit memory components capable of reading and writing four 32-bit values simultaneously.

---

## Vector Arithmetic Logic Unit

The Vector ALU executes SIMD operations by dividing 128-bit vectors into multiple lanes and performing operations on each lane in parallel.

All execution units operate simultaneously, while multiplexers select the final result according to the instruction opcode.

---

## Supported Vector Instructions

### 32-bit Vector Arithmetic

#### VADD32

Performs four parallel 32-bit additions.

```text
[A0 A1 A2 A3]
+
[B0 B1 B2 B3]
```

#### VSUB32

Performs four parallel 32-bit subtractions.

#### VMUL32

Performs four parallel 32-bit multiplications.

---

### 16-bit Vector Arithmetic

#### VADD16

Performs eight parallel 16-bit additions.

#### VSUB16

Performs eight parallel 16-bit subtractions.

#### VMUL16

Performs eight parallel 16-bit multiplications.

The 16-bit mode increases data-level parallelism by doubling the number of simultaneously processed values.

---

### Vector Logical Instructions

#### VAND

Bitwise AND across all vector lanes.

#### VOR

Bitwise OR across all vector lanes.

#### VXOR

Bitwise XOR across all vector lanes.

All logical operations execute simultaneously across the entire vector.

---

## Control Unit Extensions

The original processor control unit was extended with additional signals required for vector execution.

### Vector Register Signals

```text
RegWriteV
RegDstV
```

These signals perform functions similar to the scalar register-file control signals but operate on vector registers.

### Transfer Signals

```text
TOCOP
FROMCOP
```

Used for communication between scalar and vector register files.

### Vector Store Signal

```text
IsVStore
```

Used to distinguish vector memory operations.

---

## Memory Modes

The memory subsystem supports four operating modes:

| Mode | Operation     |
| ---- | ------------- |
| 0    | Read 32-bit   |
| 1    | Write 32-bit  |
| 2    | Read 128-bit  |
| 3    | Write 128-bit |

These modes allow both scalar and vector instructions to share the same memory subsystem.

---

## Design Goals

This project was designed to explore:

* SIMD Architectures
* Vector Processing
* Data-Level Parallelism
* ISA Extension Design
* Vector Register Files
* Parallel Arithmetic Units
* Memory System Extensions
* Control Logic Design

---

## Technologies

* Logisim Evolution
* MIPS ISA
* Digital Logic Design
* SIMD Processing
* Vector Architectures

---

## Project Context

This project was developed for the Computer Architecture course at Sharif University of Technology.

The implementation extends a previously developed single-cycle MIPS processor with a custom vector-processing subsystem and demonstrates how SIMD instructions can be integrated into a traditional scalar architecture.

---

## Authors

* Sobhan Aghasi Zadeh
* Parmis Hemasian
* Nima Kahdenarouei
* Fatemeh Tamehri

Computer Architecture Course – Spring 2025

Sharif University of Technology
