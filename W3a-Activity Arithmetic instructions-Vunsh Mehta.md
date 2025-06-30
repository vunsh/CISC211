# Activity Arithmetic instructions

## Flowchart

![Flowchart](https://github.com/user-attachments/assets/88f01b76-e3c8-40cd-bd17-a055aaf13f93)

---

## Equation 1: `result = -var1 * 10`

### Code:
```
section .data
    var1    dd 5
    result  dd 0

section .text
    global _start

_start:
    mov eax, [var1]
    neg eax
    imul eax, eax, 10
    mov [result], eax

    mov eax, 1
    mov ebx, 0
    int 0x80
```

### Debug Screenshot:
![Equation 1](https://github.com/user-attachments/assets/7c428781-620a-4a11-9ece-c6e70f62b9a0)

---

## Equation 2: `result = var1 + var2 + var3 + var4`

### Code:
```
section .data
    var1    dd 3
    var2    dd 7
    var3    dd 12
    var4    dd 8
    result  dd 0

section .text
    global _start

_start:
    mov eax, [var1]
    add eax, [var2]
    add eax, [var3]
    add eax, [var4]
    mov [result], eax

    mov eax, 1
    mov ebx, 0
    int 0x80
```

### Debug Screenshot:
![Equation 2](https://github.com/user-attachments/assets/8352caab-2774-4224-99dd-9163c0513c41)

---

## Equation 3: `result = (-var1 * var2) + var3`

### Code:
```
section .data
    var1    dd 4
    var2    dd 6
    var3    dd 10
    result  dd 0

section .text
    global _start

_start:
    mov eax, [var1]
    neg eax
    imul eax, [var2]
    add eax, [var3]
    mov [result], eax

    mov eax, 1
    mov ebx, 0
    int 0x80
```

### Debug Screenshot:
![Equation 3](https://github.com/user-attachments/assets/79eff3e0-2d60-4537-bdf5-8c2b7fb3d314)

---

## Equation 4: `result = (var1 * 2) / (var2 - 3)`

### Code:
```
section .data
    var1    dd 10
    var2    dd 5
    result  dd 0

section .text
    global _start

_start:
    mov eax, [var1]
    imul eax, eax, 2
    mov ebx, [var2]
    sub ebx, 3
    cdq
    idiv ebx
    mov [result], eax

    mov eax, 1
    mov ebx, 0
    int 0x80
```

### Debug Screenshot:
![Equation 4](https://github.com/user-attachments/assets/fc4d755f-4a0e-49cb-946d-fe712fa4e091)

---

## Challenges

- I was initially inclined to make one file for every equation, and I tried implementing this at first. I then re-read the assignment and saw that I had to do 4 seperate files, which actually make it way easier.

---
