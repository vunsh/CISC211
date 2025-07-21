# Activity - Functions

## Output Screenshot

<img width="400" alt="Output" src="https://github.com/user-attachments/assets/1c7e9443-0ae2-4ef3-91e6-b2e99f502fc9" />

---

## Flowchart

<img width="600" alt="Flowchart" src="https://github.com/user-attachments/assets/207b8d5c-7816-475b-98cf-a991e51f1408" />

---

## Challenges Faced

The main challenge was ensuring that the correct message ("odd" or "even") was printed after the function was called. Initially, the output wasn't printing because the result variable was treated as a pointer, and I forgot to dereference it before passing it to the syscall.

---

## Code 
Testing with the number 7

```nasm
section .data
    even_msg db "even", 10, 0
    odd_msg db "odd", 10, 0

section .bss
    result resd 1

section .text
    global _start

_start:
    push 7
    call _check_even_odd

    mov eax, 4
    mov ebx, 1
    mov ecx, [result]
    mov edx, 5
    int 0x80

    mov eax, 1
    int 0x80

_check_even_odd:
    push ebp
    mov ebp, esp
    sub esp, 4

    mov eax, [ebp+8]
    and eax, 1
    cmp eax, 0
    jne .odd

    mov dword [ebp-4], even_msg
    jmp .done

.odd:
    mov dword [ebp-4], odd_msg

.done:
    mov eax, [ebp-4]
    mov [result], eax
    leave
    ret
```
