# W2c2-Activity Variables and constants-Vunsh Mehta.md

## Objective
Learn how to assign variables and constants

## Flowchart

![Flowchart](https://github.com/user-attachments/assets/c7a2a29d-2f6e-48a3-aa56-b5f74c6ecb42)

## Final Code

```nasm
section .data
    var1 dd 10
    var2 dd 15

section .bss
    result resd 1

section .text
    global _start

_start:
    mov eax, [var1]
    add eax, [var2]
    mov [result], eax     ; Store result

    mov eax, 1            ; syscall: exit
    int 0x80
```


## GDB Output

![GDB Output](https://github.com/user-attachments/assets/12f8e5c1-770c-466d-8681-7b3cc0a55a6e)

## Challenges

- I struggled initially getting GDB to be nice to me with watching result because result wasn't cast to a type, so I found the location of the variable and casted it to an int: `watch *(int*)0xresult_address`
