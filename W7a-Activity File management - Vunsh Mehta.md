# W7a-Activity File management

## Objective

Learn to perform file management in Assembly Language.

---

## Challenges Faced

#### A challenge I faced was figuring out the length of each quote for sys_write before moving onto the next. I was hardcoding it previously and running into issues calculating it with new lines and such, so I instead calculated it using "equ" to calculate the length of the String.
---

## Final Output

Terminal output after running `cat quotes.txt`

![quotes.txt output](https://github.com/user-attachments/assets/f14394e1-0a3d-44b7-b8db-a10290f4ff01)

---

## Code

```nasm
SECTION .data
filename db 'quotes.txt', 0

quote1 db 'To be, or not to be, that is the question.', 10
len1   equ $ - quote1

quote2 db 'A fool thinks himself to be wise, but a wise man knows himself to be a fool.', 10
len2   equ $ - quote2

quote3 db 'Better three hours too soon than a minute too late.', 10
len3   equ $ - quote3

quote4 db 'No legacy is so rich as honesty.', 10
len4   equ $ - quote4

SECTION .bss
fd resb 1

SECTION .text
global _start

_start:
mov eax, 8
mov ebx, filename
mov ecx, 0777o
int 0x80
mov [fd], eax

mov eax, 4
mov ebx, [fd]
mov ecx, quote1
mov edx, len1
int 0x80

mov eax, 4
mov ebx, [fd]
mov ecx, quote2
mov edx, len2
int 0x80

mov eax, 6
mov ebx, [fd]
int 0x80

mov eax, 5
mov ebx, filename
mov ecx, 2
mov edx, 0777o
int 0x80
mov [fd], eax

mov eax, 19
mov ebx, [fd]
mov ecx, 0
mov edx, 2
int 0x80

mov eax, 4
mov ebx, [fd]
mov ecx, quote3
mov edx, len3
int 0x80

mov eax, 4
mov ebx, [fd]
mov ecx, quote4
mov edx, len4
int 0x80

mov eax, 6
mov ebx, [fd]
int 0x80

mov eax, 1
int 0x80
```
