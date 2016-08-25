---
layout: post
title: IceCTF 2016 Hidden in Plain Sight Writeup
---

Hidden in Plain Sight, 45 points, ReverseEngineering

Plain_sight was the first Reversing Challenge of this CTF and lucky for
everyone turned out to be just a password hardcoded into the binary.

Unfortunately, strings does not find this password but radare2 does.

Firstly, open up r2, analyze the file, and print main. Below is a snippet of
how that is done.

```
r2 plain_sight
aaaa
pdf@main

0x0804851b      b049           mov al, 0x49                ; 'I'
|           0x0804851d      b063           mov al, 0x63                ; 'c'
|           0x0804851f      b065           mov al, 0x65                ; 'e'
|           0x08048521      b043           mov al, 0x43                ; 'C'
|           0x08048523      b054           mov al, 0x54                ; 'T'
|           0x08048525      b046           mov al, 0x46                ; 'F'
|           0x08048527      b07b           mov al, 0x7b                ; '{'
|           0x08048529      b06c           mov al, 0x6c                ; 'l'
|           0x0804852b      b06f           mov al, 0x6f                ; 'o'
|           0x0804852d      b06f           mov al, 0x6f                ; 'o'
|           0x0804852f      b06b           mov al, 0x6b                ; 'k'
|           0x08048531      b05f           mov al, 0x5f                ; '_'
|           0x08048533      b06d           mov al, 0x6d                ; 'm'
|           0x08048535      b06f           mov al, 0x6f                ; 'o'
|           0x08048537      b06d           mov al, 0x6d                ; 'm'
|           0x08048539      b05f           mov al, 0x5f                ; '_'
|           0x0804853b      b049           mov al, 0x49                ; 'I'
|           0x0804853d      b05f           mov al, 0x5f                ; '_'
|           0x0804853f      b066           mov al, 0x66                ; 'f'
|           0x08048541      b06f           mov al, 0x6f                ; 'o'
|           0x08048543      b075           mov al, 0x75                ; 'u'
|           0x08048545      b06e           mov al, 0x6e                ; 'n'
|           0x08048547      b064           mov al, 0x64                ; 'd'
|           0x08048549      b05f           mov al, 0x5f                ; '_'
|           0x0804854b      b069           mov al, 0x69                ; 'i'
|           0x0804854d      b074           mov al, 0x74                ; 't'
|           0x0804854f      b07d           mov al, 0x7d                ; '}'

```

That is pretty much it for this one.
