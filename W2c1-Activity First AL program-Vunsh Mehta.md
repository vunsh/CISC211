# W2c1-Activity First AL program
## Objective

Learn how to write your first assembly language code.

---

## Flowchart

![Flowchart](https://github.com/user-attachments/assets/f21ae37d-f975-41cd-b24d-dfa9f0915f9a)

---

## Challenges Faced

- Newline characters: I initially forgot to add `0xA`to the end of each message to make sure it causes a new line, which caused all output to appear on one line. I was able to look closer at the example program in the lexture and realize the 0xA was the newline registry.

---

## Code

```nasm
section .text
    global _start

_start:
    ; Print first message
    mov eax, 4
    mov ebx, 1
    mov ecx, msg1
    mov edx, len1
    int 0x80

    ; Print second message
    mov eax, 4
    mov ebx, 1
    mov ecx, msg2
    mov edx, len2
    int 0x80

    ; Print third message
    mov eax, 4
    mov ebx, 1
    mov ecx, msg3
    mov edx, len3
    int 0x80

    ; Exit program
    mov eax, 1
    int 0x80

section .data
    msg1 db 'I came,', 0xA
    len1 equ $ - msg1

    msg2 db 'I saw,', 0xA
    len2 equ $ - msg2

    msg3 db 'I conquered.', 0xA
    len3 equ $ - msg3
```

---

## Output

![Output Screenshot](https://github.com/user-attachments/assets/4adc7fe3-9f3e-4fc7-8399-8df0887b6848)

---

