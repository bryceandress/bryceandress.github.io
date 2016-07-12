---
layout: note
title: Useful Radare2 Commands
---
# Radare Commands

iI - File information

ie - Entry Points

iM - Main address

is - Symbols in binary

iz - Strings in binary

/  - Look for specific strings

axt - Find locations of functions or addresses

afl - list all functions

afn - Rename function

afvn - Rename variable

oo+ - open file in read-write mode

-Aw - Analyzes all functions and data and opens in write mode

f - shows all flags

axt **a**nalyze (**x**)reference **t**o

In visual mode d brings up a menu of things to do

f analyzes

Pressing A on NOPS will put you in the Visual Assembler where you can add functions

radiff2 shows changes made

-Ad puts in debugging mode

dcu main - **d**bugger **c**ontinue **u**ntil **m**ain

woe 42 3 @ edi!32 - write in memory o stands for operation and e stands for sequence
This code places 42, 45, 48, etc into edi until edi+32

wox `p8 32 @ edi` @ eax!32

ESIL commands are prefaced with ae

In visual mode O cycles between representations of the instructions


