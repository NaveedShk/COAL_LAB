TASK 01:
```
include irvine32.inc
.data
.code
main proc
	mov eax,10
	mov ebx,eax
	mov ecx,eax
	shl eax,4
	shl ebx,2
	add eax,ebx
	add eax,ecx
	call writeint
exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/aed925ea-dc87-436f-a511-c6c1cb9a6bd1)


TASK 02:

````
INCLUDE Irvine32.inc

.data

.code
main PROC

    mov ax, -128       
    movzx eax, ax        


    shl eax, 16          
    sar eax, 16          

    call WriteInt        
    call Crlf
    exit
main ENDP

END main

````
![image](https://github.com/user-attachments/assets/97b019d0-961c-443b-922b-fbe6bf619b62)


TASK 03:
````
INCLUDE Irvine32.inc

.data
    msg1 BYTE "BX after manual shift: ", 0
    msg2 BYTE "BX after SHRD: ", 0

.code
main PROC

    mov ax, 0003h      

    shl ax, 15         
    mov bx,0
    or  bx, ax        
    mov edx, OFFSET msg1
    call WriteString
    movzx eax, bx
    call WriteHex

    mov ax, 0003h  

    mov dx, ax          
    shl dx, 15         
       
    mov cx, 1
    shrd bx, dx, cl    

    call Crlf
    mov edx, OFFSET msg2
    call WriteString
    movzx eax, bx
    call WriteHex

    call Crlf
    exit
main ENDP

END main

````
![image](https://github.com/user-attachments/assets/742bdfaa-ef0f-4928-8898-a8b432d72dd5)

TASK 04:
````
INCLUDE Irvine32.inc

.data
    val1 SDWORD 100
    val2 SDWORD 20
    val3 SDWORD 5

.code
main PROC
    ; (val2 / val3)
    mov eax, val2       ; dividend
    cdq                 ; sign-extend EAX into EDX:EAX
    mov ecx, val3       ; divisor
    idiv ecx            ; EAX = val2 / val3
    mov ebx, eax        ; store result in EBX: ebx = (val2 / val3)

    ; (val1 / val2)
    mov eax, val1
    cdq
    mov ecx, val2
    idiv ecx            ; EAX = val1 / val2
    imul ebx            ; EAX = (val2 / val3) * (val1 / val2)

    ; Store result back in val1
    mov val1, eax

    ; Print result
    call Crlf
    mov edx, OFFSET val1Label
    call WriteString
    mov eax, val1
    call WriteInt

    call Crlf
    exit
main ENDP

.data
    val1Label BYTE "val1 = ", 0

END main

````
![image](https://github.com/user-attachments/assets/abdbd2c7-e986-4b95-b3a2-b211daf35106)

TASK 05:
````
INCLUDE Irvine32.inc

.data
    val1Low SDWORD 0x12345678h        ; Lower 32 bits of the first 64-bit integer
    val1High SDWORD 0x9ABCDEF0h        ; Upper 32 bits of the first 64-bit integer
    val2Low SDWORD 0x23456789h         ; Lower 32 bits of the second 64-bit integer
    val2High SDWORD 0xABCDEF01h        ; Upper 32 bits of the second 64-bit integer
    resultLow SDWORD 0                ; Lower 32 bits of the result
    resultHigh SDWORD 0               ; Upper 32 bits of the result

.code
main PROC
    ; Call Extended_Add procedure
    call Extended_Add

    ; Print the result (lower part)
    mov edx, OFFSET resultLow
    call WriteString
    mov eax, resultLow
    call WriteHex

    call Crlf

    ; Print the result (upper part)
    mov edx, OFFSET resultHigh
    call WriteString
    mov eax, resultHigh
    call WriteHex

    call Crlf
    exit
main ENDP

; Procedure to add two 64-bit integers
; Arguments: 
;   val1Low, val1High  -> First 64-bit integer
;   val2Low, val2High  -> Second 64-bit integer
; Result:
;   resultLow, resultHigh -> Result of the addition
Extended_Add PROC
    ; Add the lower 32 bits of the two integers (val1Low + val2Low)
    mov eax, val1Low            ; Load lower part of the first integer
    add eax, val2Low            ; Add lower part of the second integer
    mov resultLow, eax          ; Store the result of lower part

    ; Check if carry occurred (set by add instruction)
    jc CarryOccurred            ; If carry occurred, jump to carry handling

    ; No carry: Add the upper parts (val1High + val2High)
    mov eax, val1High
    add eax, val2High
    mov resultHigh, eax         ; Store the result of the upper part
    ret

CarryOccurred:
    ; Carry occurred: Add the upper parts (val1High + val2High) + 1
    mov eax, val1High
    add eax, val2High
    inc eax                     ; Add the carry (1)
    mov resultHigh, eax         ; Store the result of the upper part with carry

    ret
Extended_Add ENDP

END main

````





