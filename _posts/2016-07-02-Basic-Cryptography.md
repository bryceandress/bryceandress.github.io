---
layout: note
title: Basic Cryptography
---

# Cryptography

## Terms
* Plaintext is the original message
* Ciphertext is the coded message
* Cipher is the algorithm use to transform plaintext to ciphertext
* Key is the info used in cipher known only to sender/receiver
* Cryptanalysis (codebreaking) is the study of principles/methods of deciphering ciphertext without knowing the key
* Cryptology is the field of cryptography and cryptanalysis
* **Symmetric Encryption** is when both sender and receiver use the same keys
* **Asymmetric Encrpytion** is when sender/receiver use different keys

## Block vs. Stream ciphers
* Block ciphers encrypt block at a time
* Message is broken into blocks and encrypted
* Stream ciphers process a bit or byte at a time during encryption and decryption

## Confusion and Diffusion
* **Diffusion** dissipates statistical structure of plaintext over bul of cipher text
* **Confusion** makes relationships between ciphertext and key as complex as possible

## Fiestel Cipher
* Partitions input block into two halves
    - Employs multiple rounds of processing
    - Performs a substitution on left data half based on a fn of right half & subkey
    - Employs permutation swapping halves

## Cipher parameters
* Block Size
    - Increasing size improves security, but slows cipher
* Key Size
    - Increasing size improves security, makes exhaustive key searching harder, but may slow cipher
* Number of rounds
    - Increasing number improves security, but slows cipher
* Subkey generation
    - Greater complexity can make analysis harder but slows cipher
* Round function
    - Greater complexity can make analysis harder, but slows cipher

## DES cipher
* Data Encryption Standard
* Encrypts 64-bit data using 56 bit key
* The 56-bit key has 2^56 or 7.2*10^16 values

[Source](http://www.ee.tamu.edu/~reddy/ee689_06/encrypt-basics.pdf)
