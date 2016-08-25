---
layout: note
title: Basic Assembly Pt II
---

# More Assembly

## Moving around

* movsx - signed mov
    - Pad with 0 for positive or F for negative
        + 0x1000 = 0x00001000
        + 0xFFFF = 0xFFFFFFFF
* movzx - ungsigned mov
    - Always pad with 0
        + 0x1000 = 0x00001000
        + 0xFFFF = 0x0000FFFF
* lea - load effective address
    - Mostly used for math or an array index
        + lea eax, [eax+eax] ; Doubles the value of eax -- eax = eax * 2
        + lea edi, [esi+0Bh] ; Adds 11 to esi and stores the result
        + lea eax, [esi+ecx*4] ; Index of an array of ints. esi is pointer to the
				 beginning of an array and ecx is the index. Index
				 is multiplied by 4 because Integers are 4 bytes
 				 long. eax will end up storing the address of the
				 ecx'th element of the array.
	+ lea edi, [eax+eax*2] ; Triples the value of eax
	+ lea edi, [eax+ebx*2] ; This indicates eax stores an array of 16 bit values
				 and that ebx is the offset.
## Math and Logic
* add, sub
    - add eax, 3 ; adds 3 to eax
    - add ebx, eax ; adds the value of eax to ebx
    - sub ecx, 3 ; subs 3 from ecx

* inc, dec essentially increment and decrement
    - inc eax ; eax++
    - dec ecx ; ecx--

* and, or, xor, neg - logical bitwise operators
    - and eax, 7 ; eax = eax & 7 this clears all bits except last 3
    - or eax, 16 ; eax = eax | 16 This sets 5th bit to the right to 1
    - xor eax, 1 ; eax = eax ^ 1 this toggles the right most bit in eax
				 0=>1 or 1=>0
    - xor eax, FFFFFFFFh ; this is a bitwise negation
    - neg eax ; eax = ~eax
    - xor eax, eax ; eax = 0 this clears eax very quickly
* mul, imul, idiv, cdq
    - mul is unsigned, imul is signed
    - mul  ecx ; edx:eax = eax * ecx (unsigned)
    - imul edx ; edx:eax = eax * edx (signed)
    - mul  ecx, 10h ; ecx = ecx * 0x10 (unsigned)
    - imul ecx, 20h ; ecx = ecx * 0x20 (signed)
    - div does div and mod at the same time
    - div  ecx ; eax = edx:eax / ecx (unsigned)
	       ; edx = edx:eax % ecx (unsigned)
    - idiv ecx ; eax = edx:eax / ecx (signed)
		 edx = edx:eax % ecx (signed)
    - cdq - generally used right before idiv
        + stands for convert double to quad

Common use of cdq and idiv

```
mov eax, 1007 ; 1007 will be divided
mov ecx, 10   ; by 10
cdq           ; extends eax into edx
idiv ecx      ; eax will be  1007/10 = 100 and edx will be 1007%10 = 7
```
* shl, shr, sal, sar
    - shl - shift left
    - shr - shift right
    - sal - shift arithmetic left
    - sar - shift arithmetic right
    - equivalent to << and >> in C
    - Faster than mul and div involving powers of 2

Divide by 2
```
mov eax, 16   ;eax = 16    0000 1000
shr eax, 1    ;eax = 8     0000 0100
```

Multiply by 4
```
mov eax, 5    ;eax = 5     0000 0101
sal eax, 2    ;eax = 20    0000 1010
```

