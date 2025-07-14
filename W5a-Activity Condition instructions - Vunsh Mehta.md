# Conditional Instructions Activity

### Objective
Learn to perform conditional instructions in Assembly Language.

## Task 1 - Even Number Sequence

### Code

```assembly
section .text
        global _start

_start:
        mov eax, 0

loop:
        mov [tmp], eax
        push eax

        mov eax, 4
        mov ebx, 1
        mov ecx, tmp
        mov edx, 1
        int 0x80

        mov eax, 4
        mov ebx, 1
        mov ecx, space
        mov edx, 1
        int 0x80

        pop eax
        add eax, 2
        cmp eax, 22
        jl loop

        mov eax, 1
        int 0x80

section .bss
        tmp resb 1

section .data
        space db 10
```

### Flowchart
Flowchart used to plan Task 1 logic:  
![Flowchart Task 1](https://github.com/user-attachments/assets/b7bd582f-4daf-46c7-badb-b9112a7c9201)

### GDB Output
Screenshot 1:  
![GDB Output 1](https://github.com/user-attachments/assets/09e05087-37a3-4131-b54f-08648c68e8a1)

Screenshot 2:  
![GDB Output 2](https://github.com/user-attachments/assets/44d42a3e-ee38-4afd-8318-f2ec5e096b36)

---

## Task 2 - Find Largest of Five Numbers

### Code

```assembly
section .text
        global _start

_start:
        mov eax, [num1]
        cmp eax, [num2]
        jg skip2
        mov eax, [num2]
skip2:
        cmp eax, [num3]
        jg skip3
        mov eax, [num3]
skip3:
        cmp eax, [num4]
        jg skip4
        mov eax, [num4]
skip4:
        cmp eax, [num5]
        jg skip5
        mov eax, [num5]
skip5:
        mov [largest], eax
        mov eax, 1
        int 0x80

section .data
        num1 dd 12
        num2 dd 27
        num3 dd 8
        num4 dd 31
        num5 dd 20

section .bss
        largest resd 1
```

### Flowchart
Flowchart used to plan Task 2 logic:  
![Flowchart Task 2](https://github.com/user-attachments/assets/6283f4cb-bfeb-4f1e-b9dc-cb0c5e8cfe2d)

### GDB Output
![GDB Output Task 2](https://github.com/user-attachments/assets/cda3bd9a-61b4-47ae-99c9-d66c35003b3e)

---

## Challenges Faced

The biggest challenge I faced was outputting the numbers. Because it was just raw byte data and not converted ASCII characters, it just outputted as empty characters in the terminal. I instead used gdb to watch the tmp variable (casted to a Char) and watched it update. 

