---
layout: post
title: How to Run Shellcode in OllyDbg
---

# Running Shellcode in OllyDbg

1. Copy shellcode to clipboard
2. Within Memory Map select a priv region
3. Double-click rows to bring up hex dump
4. Right-click in Memory Map window select Set Access -> Full Access
    - This gives the shellcode read, write, execute permisions
5. Return to Mem Dump Windo, highlight a region of zero-filled bytes large enough for shellcode.
    - Right-click and select Binary -> Binary Paste
6. Set EIP to shellcode by right-clicking an instruction in the disassemble window and selecting New Origin Here

