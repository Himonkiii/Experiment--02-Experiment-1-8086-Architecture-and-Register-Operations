# Experiment--02-Experiment-1-8086-Architecture-and-Register-Operations
 DATE:11/17/2026
NAME: Himank Bhandari
ROLL NUMBER: RA2511030010355
DEPARTMENT: NWC
## Aim

To study the architecture of the 8086 microprocessor and write assembly
language programs for register-to-register data transfer, memory
storage, and exchanging two 16-bit memory values.

## Learning Outcomes

After completing this experiment, students will be able to: - Explain
the main functional units of the 8086 microprocessor. - Describe the
roles of the Bus Interface Unit (BIU) and Execution Unit (EU). - Write
8086 assembly instructions for 16-bit data transfer. - Exchange data
between two memory locations using registers.

## Software Required

-   An 8086 assembly emulator, such as emu8086 or an equivalent
    8086-compatible emulator.
-   A text editor for writing the assembly programs.

------------------------------------------------------------------------

## Part (a): 8086 Architecture and Functional Units

### Question

Explain the architecture of the 8086 microprocessor with a neat block
diagram, describing the functions of the BIU and EU.

### Theory

The Intel 8086 is a 16-bit microprocessor with a 16-bit data bus and a
20-bit address bus. It can address up to 1 MB of physical memory. Its
architecture is divided into two major units:

**1. Bus Interface Unit (BIU)** - Generates the 20-bit physical
address. - Fetches instructions from memory. - Reads data from and
writes data to memory and I/O devices. - Contains the segment registers:
CS, DS, SS, and ES. - Contains the Instruction Pointer (IP). - Includes
a 6-byte instruction prefetch queue, allowing instruction fetching and
execution to overlap.

**2. Execution Unit (EU)** - Decodes and executes instructions fetched
by the BIU. - Contains the Arithmetic Logic Unit (ALU). - Contains
general-purpose registers AX, BX, CX, and DX, which can be accessed as
8-bit halves. - Contains pointer and index registers SP, BP, SI, and
DI. - Contains the Flag Register, which records status and control
flags. - Requests the BIU to perform memory and I/O transfers when
required.

### Simplified Block Diagram

``` text
                 +-----------------------------------+
                 |          8086 MICROPROCESSOR     |
                 |                                   |
Memory / I/O <-->+-----------------------------------+<--> System Bus
                 |       Bus Interface Unit (BIU)    |
                 |  +-----------------------------+  |
                 |  | Segment Registers            |  |
                 |  | CS, DS, SS, ES               |  |
                 |  +-----------------------------+  |
                 |  | Instruction Pointer (IP)     |  |
                 |  +-----------------------------+  |
                 |  | 6-byte Instruction Queue     |  |
                 |  +-----------------------------+  |
                 |  | Address Generation / Bus     |  |
                 |  | Control                      |  |
                 |  +---------------+-------------+  |
                 |                  |                |
                 |       Instruction/Data Interface  |
                 |                  |                |
                 |       Execution Unit (EU)         |
                 |  +-----------------------------+  |
                 |  | Instruction Decoder &       |  |
                 |  | Control Circuitry           |  |
                 |  +-----------------------------+  |
                 |  | ALU                         |  |
                 |  +-----------------------------+  |
                 |  | AX, BX, CX, DX               |  |
                 |  | SP, BP, SI, DI               |  |
                 |  | Flag Register                |  |
                 |  +-----------------------------+  |
                 +-----------------------------------+
```

### Working Principle

The BIU fetches instruction bytes and stores them in its 6-byte queue
while the EU executes instructions already available in the queue. When
the EU needs memory or I/O access, it requests the BIU to perform the
bus operation. A change in program flow, such as a jump, may cause the
instruction queue to be flushed and refilled.

------------------------------------------------------------------------

## Part (b): Transfer a 16-bit Value Between Registers and Store It in Memory

### Question

Write an 8086 assembly language program to transfer a 16-bit data value
from one register to another and store the result in memory.

### Algorithm

1.  Load a 16-bit value into AX.
2.  Transfer the value from AX to BX.
3.  Store the value in BX into the memory variable `RESULT`.
4.  Stop the program.

### Assembly Program

``` asm
.MODEL SMALL
.STACK 100H

.DATA
    RESULT DW 0000H

.CODE
MAIN PROC
    MOV AX, @DATA
    MOV DS, AX

    MOV AX, 1234H       ; Load 16-bit value into AX
    MOV BX, AX          ; Copy AX into BX
    MOV RESULT, BX      ; Store BX in memory

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

### Expected Result

-   AX = `1234H`
-   BX = `1234H`
-   RESULT = `1234H`

### Explanation

`MOV BX, AX` copies the 16-bit contents of AX into BX without changing
AX. `MOV RESULT, BX` stores the contents of BX in the 16-bit memory
variable `RESULT`. The `MOV` instruction does not modify the source
operand.

## Screenshot of the results 
<img width="2878" height="1799" alt="Screenshot 2026-11-17 154317" src="https://github.com/user-attachments/assets/cdc162ef-9533-4059-af75-f3747a031e14" />


------------------------------------------------------------------------

## Part (c): Exchange Two 16-bit Memory Locations Using Registers

### Question

Write an 8086 assembly language program to exchange the contents of two
16-bit memory locations using registers.

### Algorithm

1.  Load the first memory value into AX.
2.  Load the second memory value into BX.
3.  Store BX at the first memory location.
4.  Store AX at the second memory location.
5.  Stop the program.

### Assembly Program
.MODEL SMALL
.STACK 100H

.DATA
    VALUE1 DW 1111H
    VALUE2 DW 2222H

.CODE

    MOV AX, @DATA
    MOV DS, AX

    MOV AX, VALUE1       ; Load VALUE1 into AX
    MOV BX, VALUE2       ; Load VALUE2 into BX

    MOV VALUE1, BX       ; Store VALUE2 into VALUE1
    MOV VALUE2, AX       ; Store VALUE1 into VALUE2

    HLT
 

### Expected Result

  Memory Variable     Before Execution   After Execution
  ----------------- ------------------ -----------------
  VALUE1                       `1111H`           `2222H`
  VALUE2                       `2222H`           `1111H`

### Explanation
The 8086 does not allow memory-to-memory MOV (for example, MOV VALUE1, VALUE2 is invalid). So both values are first loaded into registers AX and BX, then stored back crosswise: BX goes to VALUE1 and AX goes to VALUE2. This swaps the two values without losing either one.
  
------------------------------------------------------------------------

## Procedure

1.  Open an 8086-compatible assembler or emulator.
2.  Create a new assembly source file.
3.  Enter and assemble the program for the selected part.
4.  Correct any syntax or assembler-specific errors.
5.  Execute the program step by step or run it.
6.  Inspect the registers and memory variables.
7.  Record the observed results and compare them with the expected
    results.
## Screenshot of the results 

<img width="2875" height="1599" alt="Screenshot 2026-11-17 154921" src="https://github.com/user-attachments/assets/3e71888b-d4c4-4a8a-ae0a-2371882a2fb4" />


## Result

The 8086 architecture and the functions of the BIU and EU were studied.
The assembly programs demonstrate 16-bit register transfer with memory
storage and the exchange of two 16-bit memory values.


## Viva Voce Questions

1.  What is the function of the BIU in the 8086?
2.  What is the role of the EU?
3.  Why does the 8086 use a 6-byte instruction queue?
4.  What is the maximum physical memory address space of the 8086?
5.  What is the difference between a register and a memory variable?
6.  Does the `MOV` instruction change the source operand?
7.  Why are registers used when exchanging two memory values?
8.  What is the purpose of the DS segment register?
Viva Voce Answers

Function of the BIU: It fetches instructions, generates the 20-bit physical address, and reads/writes data from memory and I/O devices. It also holds the segment registers, the IP, and the instruction queue.
Role of the EU: It decodes and executes instructions supplied by the BIU, using the ALU, general-purpose registers, and the flag register.
Why a 6-byte instruction queue: It lets instruction fetch and execution overlap (pipelining), so the EU does not sit idle waiting for the next instruction.
Maximum physical memory: 1 MB (2^20 bytes), because the address bus is 20 bits wide.
Register vs memory variable: A register is a small storage location inside the CPU and is very fast. A memory variable lives in RAM and is slower, because accessing it needs a bus cycle.
Does MOV change the source? No. It only copies data to the destination.
Why use registers for the exchange: The 8086 has no direct memory-to-memory transfer, so a register must hold at least one value temporarily.
Purpose of DS: It holds the base address of the data segment, which is used with an offset to access variables in the data area.
 
` 
