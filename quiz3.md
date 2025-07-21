# Quiz 3

## Output
Input value: 5

![Screenshot of output](https://github.com/user-attachments/assets/319be638-4689-4b0e-af10-92792d31e9a5)

## Code

```nasm
section .data
    x db 5
    newline db 0xA
    digits db '0123456789'

section .bss
    result resd 1

section .text
    global _start

_start:
    mov eax, 1
    mov [result], eax
    movzx ecx, byte [x]

.loop_start:
    cmp ecx, 1
    jl .done
    mov eax, [result]
    mov ebx, ecx
    call multiply
    mov [result], eax
    dec ecx
    jmp .loop_start

.done:
    mov eax, [result]
    call print_number
    mov eax, 4
    mov ebx, 1
    mov ecx, newline
    mov edx, 1
    int 0x80
    mov eax, 1
    xor ebx, ebx
    int 0x80

multiply:
    push ecx
    mov ecx, ebx
    xor ebx, ebx

.m_loop:
    cmp ecx, 0
    je .m_done
    add ebx, eax
    dec ecx
    jmp .m_loop

.m_done:
    mov eax, ebx
    pop ecx
    ret

print_number:
    mov ebx, 10
    xor esi, esi

.p_loop:
    xor edx, edx
    div ebx
    push edx
    inc esi
    test eax, eax
    jnz .p_loop

.print:
    cmp esi, 0
    je .p_done
    pop edx
    lea ecx, [digits + edx]
    mov eax, 4
    mov ebx, 1
    mov edx, 1
    int 0x80
    dec esi
    jmp .print

.p_done:
    ret
```
