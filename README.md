# BITBOT Computer

**Author:** Eshaan Saini (433009808)

This repository contains the hardware description language (HDL) implementation for the BITBOT Computer, a 16-bit computer platform. The project involves building the core components—CPU, Data Memory, and the top-level Computer chip—from the ground up, capable of running programs written in the BITBOT machine language.

## About The Project

The goal of this project is to construct a complete, general-purpose computer by integrating fundamental processing and storage components. Drawing inspiration from the HACK and TOY computer architectures, the BITBOT computer is designed to execute a custom instruction set that includes arithmetic, logical, memory, branch, and I/O operations.

The final platform integrates a custom CPU with a memory system that includes RAM, a memory-mapped screen, and a keyboard interface.

## Core Components

The implementation is centered around the following three main HDL files:

*   `CPU.hdl`: The Central Processing Unit, which fetches, decodes, and executes instructions.
*   `Memory.hdl`: The top-level Data Memory component that integrates RAM, Screen, and Keyboard memory maps.
*   `Computer.hdl`: The top-level chip that wires together the CPU, Instruction ROM, and Data Memory to form the complete computer platform.

## Architecture Specifications

The BITBOT Computer is a 16-bit machine, where an instruction or data value is referred to as a "word".

### 1. Central Processing Unit (CPU)
*   **Registers:** 8 general-purpose 16-bit registers (R0 through R7).
*   **ALU:** A 16-bit custom Arithmetic Logic Unit capable of 2's complement arithmetic and logical operations.
*   **Program Counter (PC):** A 16-bit counter that points to the next instruction in ROM. Supports conditional (BEQ) and unconditional (JMP) branching.

### 2. Memory
*   **Instruction Memory:** A 32K-word ROM for storing programs. This is provided as a built-in chip.
*   **Data Memory:** A 40K-word address space, organized as follows:
    *   **RAM:** 32K words for general-purpose data storage.
    *   **Screen:** 8K words memory-mapped to the display output.
    *   **Keyboard:** 1 word memory-mapped to the keyboard input.

### 3. Instruction Set Architecture (ISA)

The BITBOT computer supports a custom 16-bit instruction set with five categories of operations:

*   **Arithmetic:** `ADD`, `SUB` (register-to-register) and `ADDI`, `SUBI` (immediate value).
*   **Logical:** `NAND`, `NOR` (bitwise operations).
*   **Memory:** `READ` (`Rx = MEM[Ry]`) and `WRITE` (`MEM[Rx] = Ry`).
*   **Branch:** `BEQ` (Branch if Equal to Zero) and `JMP` (Unconditional Jump).
*   **Input/Output:** `INP` (read from keyboard) and `OUT` (write to screen).

## Instruction Format

All instructions are 16 bits wide with the following format:

```
Bits [15:14]: OPCODE
- 00: Arithmetic operations
- 01: Logical operations  
- 10: Memory/Branch operations
- 11: I/O operations

Bits [13:12]: OPTYPE
- Determines specific operation within each category

Bits [11:9]: Destination register (Rd)
Bits [8:6]: Source register 1 (Rx)
Bits [5:3]: Source register 2 (Ry)
Bits [2:0]: Immediate data or additional control
```

## Sample Programs

The project includes three demonstration programs written in BITBOT machine language:

*   `Add.hack`: Adds two numbers from RAM[0] and RAM[1] and stores the result in RAM[2].
*   `Mult.hack`: Multiplies two numbers using repeated addition and demonstrates loop control.
*   `Rect.hack`: Draws a rectangle on the screen using memory-mapped I/O operations.

## Testing

The components and the final computer can be tested using the provided **Nand2tetris Hardware Simulator**.

*   **Unit Testing:** The `CPU.hdl` and `Memory.hdl` chips can be tested individually using their respective `.tst` scripts.
*   **System Testing:** The fully assembled `Computer.hdl` can be tested by loading and running the provided programs.

### Test Files Included:
- `CPU.tst` - Comprehensive CPU instruction testing
- `Memory.tst` - Memory system validation
- `ComputerAddition.tst` - End-to-end addition program test
- `ComputerMult.tst` - End-to-end multiplication program test
- `ComputerRect.tst` - End-to-end rectangle drawing test

## Implementation Details

### Control Unit Design
The CPU implements a sophisticated control unit that:
- Decodes 16-bit instructions into control signals
- Manages register file operations (8 registers with load enable)
- Controls memory access patterns and addressing
- Handles program counter updates for branching and jumping

### Memory Hierarchy
The memory system implements a three-tier hierarchy:
- **RAM32K** (0x0000-0x7FFF): General-purpose data storage
- **Screen** (0x8000-0x9FFF): Memory-mapped display output
- **Keyboard** (0xA000): Memory-mapped keyboard input

### ALU Operations
The custom ALU supports:
- 16-bit two's complement arithmetic with overflow detection
- Bitwise logical operations (NAND, NOR)
- Operation selection based on instruction opcode

## Key Features

1. **Complete Instruction Set**: 12+ instruction types covering all major computer operations
2. **Memory Hierarchy**: Integrated RAM, screen, and keyboard subsystems
3. **Control Flow**: Conditional and unconditional branching capabilities
4. **I/O Support**: Keyboard input and screen output functionality
5. **Modular Design**: Clean separation of concerns between components
6. **Comprehensive Testing**: Extensive test coverage for all components

## Usage Instructions

1. Load the `Computer.hdl` file in the Nand2tetris Hardware Simulator
2. Load a `.hack` program file into ROM32K
3. Set initial memory values if required (for test programs)
4. Run the simulation to execute the program
5. Observe results in memory or on screen output

## Technical Specifications

- **Word Size**: 16 bits
- **Address Space**: 64K words (16-bit addressing)
- **Register File**: 8 general-purpose 16-bit registers
- **Memory**: 32K RAM + 8K Screen + 1 Keyboard
- **Instruction Set**: 12+ instruction types across 5 categories
- **Clock**: Synchronous operation with tick/tock cycles

## Project Highlights

This project demonstrates:
- Complete computer architecture implementation
- Custom instruction set design and implementation
- Control unit and microarchitecture design
- Memory hierarchy and memory-mapped I/O
- Hardware description language (HDL) programming
- System integration and comprehensive testing

The BITBOT computer serves as a complete example of how fundamental computer components work together to create a functional computing platform.
