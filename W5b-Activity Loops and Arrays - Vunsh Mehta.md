# Loops and Arrays Activity

### Objective
Learn to perform loops and arrays instructions in Assembly Language.

## Task 1 - Counter Using EBX


### Code

```assembly
section .text
        global _start

_start:
        mov ebx, 10

label:
        dec ebx
        cmp ebx, 0
        jne label

        mov eax, 1
        int 0x80
```

### Flowchart  
![Flowchart Task 1](https://github.com/user-attachments/assets/e3521723-25bd-4784-abfb-8786a2ea805e)

### GDB Output  
![GDB Task 1 Output 1](https://github.com/user-attachments/assets/e0d10645-45f2-44af-adf8-c9ddfaa39a22)  
![GDB Task 1 Output 2](https://github.com/user-attachments/assets/b8d617f3-f74f-49ef-b20a-41ba30608e58)

---

## Task 2 - 10th Fibonacci Number


### Code

```assembly
section .text
        global _start

_start:
        mov eax, 0
        mov ebx, 1
        mov ecx, 10

loop_fib:
        mov edx, eax
        add eax, ebx
        mov ebx, edx
        dec ecx
        jnz loop_fib

        mov [result], eax
        mov eax, 1
        int 0x80

section .bss
        result resd 1
```

### Flowchart  
![Flowchart Task 2](https://github.com/user-attachments/assets/2caf1de3-e166-4f46-b348-229cb14a7336)

### GDB Output  
![GDB Task 2 Output](https://github.com/user-attachments/assets/7bbcee79-bc70-4ddb-ae64-5374bfe5a493)

---

## Task 3 - Largest Element in Array


### Code

```assembly
section .text
        global _start

_start:
        mov esi, array
        mov eax, [esi]
        add esi, 4
        mov ebx, 2

loop_check:
        mov ecx, [esi]
        cmp ecx, eax
        jg update
        jmp skip

update:
        mov eax, ecx

skip:
        add esi, 4
        dec ebx
        jnz loop_check

        mov [largest], eax
        mov eax, 1
        int 0x80

section .data
        array dd 17, 42, 29

section .bss
        largest resd 1
```

### Flowchart  
![Flowchart Task 3](https://github.com/user-attachments/assets/038e632b-6868-4466-9a66-23c0704e399b)

### GDB Output  
![GDB Task 3 Output](https://github.com/user-attachments/assets/51967d27-7e5c-4bb6-b255-cb2bea33e5b7)

---


## Challenges Faced

The main challenge I faced was in Task 2, which was ensuring the loop generated the correct Fibonacci value. Initially, the loop ran the wrong number of times, and a logic error caused `eax` to reset. It took several resets of `gdb` stepping to confirm that the loop length and register assignments were correct. 
