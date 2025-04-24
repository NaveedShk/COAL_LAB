Task 03:
```
include irvine32.inc
.data
	arr BYTE 61h,43h,11h,52h,25h
.code
main proc
	mov al,0

	mov al,[arr]
	call writehex
	call crlf
	XCHG al,[arr+2] 
	mov [arr],al ; 11,43,61,52,25
	call writehex
	call crlf


	mov al,[arr+1]
	call writehex
	call crlf
	XCHG al,[arr+4] 
	mov [arr+1],al ;11,25,61,52,43
	call writehex
	call crlf

	mov al,[arr+2]
	call writehex
	call crlf
	XCHG al,[arr+4]
	mov [arr+2],al ; 11,25,43,52,64
	call writehex
	call crlf


	exit
main endp
end main 

```
![image](https://github.com/user-attachments/assets/a5025e4e-3555-4505-982f-53ddddf438a3)

Task 04:
```
include irvine32.inc
.data
	arrayB BYTE 10, 20, 30 
	arrayW WORD 150, 250, 350 
	arrayD DWORD 600, 1200, 1800
	sum1 DWORD 0
	sum2 DWORD 0
	sum3 DWORD 0
.code
main proc
	movzx eax,arrayB[0] 
	movzx ebx,arrayW[0]
	add eax, ebx
	add eax, arrayD[0]
	mov sum1,eax
	call writeint
	call crlf

	movzx eax,arrayB[1] 
	movzx ebx,arrayW[2]
	add eax, ebx
	add eax, arrayD[4]
	mov sum2,eax
	call writeint
	call crlf

	movzx eax,arrayB[2] 
	movzx ebx,arrayW[4]
	add eax, ebx
	add eax, arrayD[8]
	mov sum2,eax
	call writeint
	call crlf
	exit
main endp
end main 
```
![image](https://github.com/user-attachments/assets/ef504831-d79d-45d9-bcbf-acc5b2d45322)

Task 05:
```
include irvine32.inc
.data
	array1 BYTE 10, 20, 30, 40
    array2 BYTE 4 DUP (?)
.code
main proc
	mov esi,offset array1
	mov edi,offset array2 +3
	mov eax, 0

	mov al,[esi]
	mov [edi],al
	inc esi
	dec edi

	mov al,[esi]
	mov [edi],al
	inc esi
	dec edi

	mov al,[esi]
	mov [edi],al
	inc esi
	dec edi

	mov al,[esi]
	mov [edi],al

	
	mov al,0

	mov al,array2[0]
	call writeint 
	call crlf

	mov al,array2[1]
	call writeint 
	call crlf

	mov al,array2[2]
	call writeint 
	call crlf

	mov al,array2[3]
	call writeint 
	call crlf
	exit
main endp
end main 

```
![image](https://github.com/user-attachments/assets/d2a4f886-17f9-474e-a745-a57d4d353a54)

Task 06:
```
include irvine32.inc

.DATA
   arr DWORD 14,13,12,11,10
   result DWORD ?
.CODE
MAIN PROC
        mov eax,0
        mov esi, offset arr
        mov eax,[esi]
        add esi,4
        sub eax,[esi]
        add esi,4
        sub eax,[esi]
        add esi,4
        sub eax,[esi]
        add esi,4
        sub eax,[esi]
        mov result,eax
        call writeint
        call crlf

    exit
MAIN ENDP
END MAIN

```
![image](https://github.com/user-attachments/assets/b36ecf13-b03e-439d-bb97-b2106b643be0)

Task 07:
```
include irvine32.inc

.DATA
   arrayB BYTE 60, 70, 80
    arrayW WORD 150, 250, 350
    arrayD DWORD 600, 1200, 1800
.CODE
MAIN PROC
        mov eax,0
        mov esi,0
        mov al,arrayB[esi* TYPE arrayB]
        add esi,2
        add al,arrayB[esi* TYPE arrayB]
        call writeint
        call crlf

        mov esi,0
        mov ax,arrayW[esi* TYPE arrayW]
        add esi,2
        add ax,arrayW[esi* TYPE arrayW]
        call writeint
        call crlf

        mov esi,0
        mov eax,arrayD[esi* TYPE arrayD]
        add esi,2
        add eax,arrayD[esi* TYPE arrayD]
        call writeint
        call crlf



    exit
MAIN ENDP
END MAIN

```
![Uploading image.png…]()

