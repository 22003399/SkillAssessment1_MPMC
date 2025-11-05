# SKILL_ASSESSMENT_2

## AIM
To Write an assembly language program in 8086 to check whether a given  number is a palindrome or not. 
---

## APPARATUS REQUIRED
- Personal Computer with **MASM** (Microsoft Macro Assembler) or **EMU8086** Software

---

## ALGORITHM
1.Step 1: Start the program
Initialize the data segment so the program can access variables and messages stored in memory.

2. Display message to enter a number
Use DOS interrupt INT 21H (function 9) to display
3.Read the number from keyboard
4. Store the entered number
5. Reverse the number
6. Compare original and reversed numbers
7. Display result
8. End the program

---

### PROGRAM

```
DATA SEGMENT
    msg1 DB 'ENTER A 5-DIGIT NUMBER:$'
    msg2 DB 0DH,0AH,'PALINDROME$'
    msg3 DB 0DH,0AH,'NOT PALINDROME$'
    num  DW ?
    rev  DW ?
DATA ENDS

CODE SEGMENT
ASSUME CS:CODE, DS:DATA

START:
    MOV AX, DATA
    MOV DS, AX

    ; Display prompt
    LEA DX, msg1
    MOV AH, 9
    INT 21H

    ; Read number as string
    MOV CX, 5          ; expecting 5 digits
    XOR BX, BX         ; BX = 0 (will store number)
READ_LOOP:
    MOV AH, 1          ; read character
    INT 21H
    SUB AL, '0'        ; convert ASCII to number
    MOV DL, AL
    MOV AX, BX
    MOV CX, 10
    MUL CX
    ADD AX, DX
    MOV BX, AX
    LOOP READ_LOOP

    MOV num, BX        ; store the number
    MOV AX, BX
    MOV rev, 0

REVERSE:
    MOV DX, 0
    MOV CX, 10
    DIV CX             ; AX ÷ 10
    MOV BX, rev
    MUL CX
    ADD DX, BX
    MOV rev, DX
    CMP AX, 0
    JNE REVERSE

    ; Compare numbers
    MOV AX, num
    CMP AX, rev
    JE IS_PAL

NOT_PAL:
    LEA DX, msg3
    MOV AH, 9
    INT 21H
    JMP EXIT

IS_PAL:
    LEA DX, msg2
    MOV AH, 9
    INT 21H

EXIT:
    MOV AH, 4CH
    INT 21H

CODE ENDS
END START

```
OUTPUT

<img width="643" height="417" alt="palindrome" src="https://github.com/user-attachments/assets/193d522b-e0a1-4cc6-83c9-1d9d79227a74" />



RESULT

Thus, the Assembly Language Program for 8086 microprocessor to find the Palindrome or not was successfully written and executed using MASM/EMU8086.

