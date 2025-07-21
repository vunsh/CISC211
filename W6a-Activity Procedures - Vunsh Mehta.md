# Activity – Procedures


## Flowchart

![Flowchart](https://github.com/user-attachments/assets/93d160db-2c31-4aae-9f53-a31008a249c5)

---

## Output

![Terminal Output](https://github.com/user-attachments/assets/2265d36f-c783-42b7-b732-3c39fdd7a036)

---

## Code

```nasm
section .data
    newline db 0xA
    char db 'A'

section .text
    global _start

_start:
    mov ecx, 26

print_loop:
    push ecx
    call print_char
    pop ecx
    inc byte [char]
    loop print_loop

    mov eax, 1
    xor ebx, ebx
    int 0x80

print_char:
    mov eax, 4
    mov ebx, 1
    mov ecx, char
    mov edx, 1
    int 0x80

    mov eax, 4
    mov ebx, 1
    mov ecx, newline
    mov edx, 1
    int 0x80

    ret
```

---

## Challenges Faced

- I had trouble making sure ecx was being preserved and assigned properly inside the scope of the loop initially.

---
