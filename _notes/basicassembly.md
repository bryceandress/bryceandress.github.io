---
layout: post
title: Basic Assembly
---

# Registers

ESP = Stack Pointer

EIP = Instruction Pointer

EAX = Primary Accumulator, also stores function return values

ECX = Count Register, Counter for string and loop operations

EDX = Data Register, I/O pointer

EBX = Base Register, Base pointer to the data section

ESI = Source Index, Source pointer for string operations

EDI = Destination Index, Destination pointer for string operation

# Common Instructions

NOP = No operation

PUSH = Move a word or register onto the stack

POP = Removes a word off the stack and puts it in a register

CALL = Transfers control to a different function in a way that control can be returned back

RET = Used to return from a function

MOV = Can move a register to a memory or memory to a register, an immediate to register, or an immediate to memory

LEA = Copy the result of one operand to another

CMP = Compares to operands

JMP = Moves conrtol to absolute or relative address

# JMP CMP conditions

JE - When Equal

JNE - When not equal

JZ - When zero

JNZ - When not zero

JG - When Greater

JGE - When greater than or equal

JL - When less than

JLE - When less than or equal to

# Sizes

Bit 1

Bytes is 8 bits

Word is 2 bytes

Dword is 2 words

Qword is 4 words

