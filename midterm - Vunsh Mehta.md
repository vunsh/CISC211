## Midterm

### Question 1 – Assembly Arithmetic Expression

**Problem:**  
Write an x86-compatible assembly code that calculates the following equation:

```
result = (var1 + 2) / (var3 - var2)
```

---

### a. Variable Values and Expected Result

```assembly
; var1 = 10
; var2 = 3
; var3 = 7
; result = 3
```

---

### b. Assembly Code

```nasm
section .data
    ; (a) Variable values
    ; var1 = 10, var2 = 3, var3 = 7
    ; result = 3

    result_msg db "Result = ", 0
    newline    db 10
    buffer     db 0

section .text
    global _start

_start:
    ; calculate result = (var1 + 2) / (var3 - var2)
    mov eax, 10         ; var1
    add eax, 2          ; var1 + 2 = 12
    mov ebx, 3          ; var2
    mov ecx, 7          ; var3
    sub ecx, ebx        ; var3 - var2 = 4

    cdq                 ; sign-extend eax into edx:eax
    idiv ecx            ; divide eax by ecx → quotient in eax, remainder in edx

    add eax, '0'        ; convert to ASCII
    mov [buffer], al

    ; print "Result = "
    mov eax, 4
    mov ebx, 1
    mov ecx, result_msg
    mov edx, 9
    int 0x80

    ; print result
    mov eax, 4
    mov ebx, 1
    mov ecx, buffer
    mov edx, 1
    int 0x80

    ; newline
    mov eax, 4
    mov ebx, 1
    mov ecx, newline
    mov edx, 1
    int 0x80

    ; exit
    mov eax, 1
    xor ebx, ebx
    int 0x80
```

---

### c. Register Table (After `idiv`)

| Register | Purpose   | Value |
|----------|-----------|-------|
| `EAX`    | Quotient  | `3`   |
| `EDX`    | Remainder | `0`   |

---

### d. GDB Verification Screenshot

#### Output Screenshot (after /run.sh) :
![Result Displayed](https://github.com/user-attachments/assets/12ebf924-dedd-46ea-99d1-20c8b148d65c)

#### GDB Screenshot After Division:
![GDB Registers](https://github.com/user-attachments/assets/8a6f843c-a25d-4721-a53f-26e8d744c890)

Break immediately after `idiv`, showing:
- `eax = 0x33` (ASCII `'3'`)
- `edx = 0x0`
---
### Question 2

**Problem:**  
Using a K-map, simplify the following equation:

```
Y = a·b + ¬a·b + a·¬b
```

---

### a. Truth Table Analysis

First we want to make a table with all combinations of A and B.

Rows where `Y = 1`:  
- a=0, b=1  
- a=1, b=0  
- a=1, b=1

---

### b. K-map Construction

|       | b=0 | b=1 |
|-------|-----|-----|
| a=0   |  0  |  1  |
| a=1   |  1  |  1  |

1s are placed in the following cells:
- (a=0, b=1)
- (a=1, b=0)
- (a=1, b=1)

---

### c. Grouping and Simplification

Group adjacent 1s:
- Horizontal group at a=1 row → (1,0) and (1,1) → simplifies to **a**
- Vertical group at b=1 column → (0,1) and (1,1) → simplifies to **b**

---

### d. Final Simplified Expression

```
Y = a + b
```

---

### e. Handwritten Work

Here was my handwritten work with these steps:

**Image:**  
![Handwritten Work](https://github.com/user-attachments/assets/da487fb8-b44f-489b-bedf-5890d32e5f8b)

---
### Question 3

**Problem:**  
Write a program in x86 assembly to identify whether a number is **odd** or **even**, without using the AND/OR logical instructions.

---

### a. Thought Process and Design

By definition:
- An even number divided by 2 has a remainder of 0
- An odd number divided by 2 has a remainder of 1

So we:
- Divide the number by 2 using `idiv`
- Inspect the remainder in the `EDX` register
- If `EDX == 0`, it's even, if it's not, it is odd!

This logic uses only arithmetic and comparison — no logical gates.

Here is a flowchart with my thought process:

**Image:**  
![Even/Odd Flowchart](https://github.com/user-attachments/assets/74ad511a-3ec0-4de4-a922-962dc78695d1)

---

### b. Assembly Code

```nasm
section .data
    even_msg db "even number", 10, 0
    odd_msg  db "odd number", 10, 0

section .text
    global _start

_start:
    ; Load number to check
    mov eax, 7           ; Can input any number here

    ; Set divisor = 2
    mov ebx, 2

    ; Sign-extend EAX into EDX
    cdq

    ; Divide EAX by EBX (2)
    idiv ebx

    ; Check if remainder == 0 (even)
    cmp edx, 0
    je print_even

print_odd:
    mov eax, 4
    mov ebx, 1
    mov ecx, odd_msg
    mov edx, 11
    int 0x80
    jmp end_program

print_even:
    mov eax, 4
    mov ebx, 1
    mov ecx, even_msg
    mov edx, 12
    int 0x80

end_program:
    mov eax, 1
    xor ebx, ebx
    int 0x80
```
---

### c. Output Screenshot

This is the output of the program when tested with `mov eax, 7`:

**Image:**  
![Even/Odd Output](https://github.com/user-attachments/assets/a4cf9e0f-54e4-494d-923b-6d601a91f491)

---


