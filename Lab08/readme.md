TASK 01:
````
include irvine32.inc
.data
	m1 byte "Intgers are equal",0
	m2 byte "Intgers are not equal",0
	m3 byte "Enter 4 integers",0
	vals dword 4 DUP(?)
.code
main proc
	mov edx,offset m3
	call writestring
	call crlf
	mov esi,0
	mov ecx,lengthof vals
	L1:
	call readint
	mov vals[esi* type vals],eax
	inc esi;
	loop L1

	mov esi,1
	mov ecx,lengthof vals -1
	mov eax,vals[0]
	L2:
	cmp eax,vals[esi* type vals]
	je cont
	mov edx, offset m2
	call writestring
	call crlf
	exit
	cont:
	inc esi
	loop L2
	mov edx, offset m1
	call writestring
   exit
main endp
end main


````
![image](https://github.com/user-attachments/assets/d9ae8be2-66f6-4731-b657-266ffd34059e)



TASK 02:
````
include irvine32.inc
.data
	m1 byte "No non zero element is present",0
	m2 byte "first non zero element is:",0
	vals sdword 0,0,0,23,12,3,-12,0,0,0
.code
main proc
	mov esi,0
	mov ecx,lengthof vals
	L1:
	cmp vals[esi* type vals],0
	jne br_L1
	inc esi;
	loop L1
	mov edx, offset m1
	call writestring
	exit
	br_L1:
	mov edx, offset m2
	call writestring
	mov eax,vals[esi* type vals]
	call writeint
	
   exit
main endp
end main

````
![image](https://github.com/user-attachments/assets/c41b03ec-40ab-4c70-ab17-4504298a5289)

TASK 03:
````
include irvine32.inc
.data
	x dword ?
	var dword 5
	vals sword 0,0,0,15,20,5,-12,6,4,0
.code
main proc
	mov edx,var + 1
	mov esi,0
	mov ecx,lengthof vals
	
	cmp var,ecx
	jge ElseCase
	cmp ecx,edx
	jl ElseCase
	mov x,0
	jmp print
	ElseCase:
	mov x,1
	print:
	mov eax,x
	call writeint
   exit
main endp
end main

````
![image](https://github.com/user-attachments/assets/c0164ca5-bc07-4ff5-bfa2-3256cdc6070f)


TASK 04:
````
include irvine32.inc
.data
	var dword 0
	m1 byte "Hi",0
	m2 byte "Everyone",0
.code
main proc
	l1:
	cmp var,10
	ja br_while
	cmp var,5
	jae elsecase
	mov edx,offset m1
	call writestring
	call crlf
	jmp cont
	elsecase:
	mov edx,offset m2
	call writestring
	call crlf
	cont:
	inc var
	jmp l1
	br_while:
   exit
main endp
end main


````
![image](https://github.com/user-attachments/assets/56e99364-bd39-43ce-bc71-788449428b98)

TASK 05:
````
include irvine32.inc
.data
	var word ?
	vals word 10,4,7,14,299,156,3,19,29,300,20
	m1 byte "Value Found at index: ",0
	m2 byte "Value not found in array ",0
	m3 byte "Enter a variable : "
.code
main proc
	mov edx, offset m3
	call writestring
	call readint
	mov var,ax

	mov ecx,lengthof vals
	mov esi,0

	l1:
	cmp vals[esi * type vals],ax
	je br_loop
	inc esi
	loop l1
	mov edx,offset m2
	call writestring
	br_loop:
	mov edx,offset m1
	call writestring
	mov eax,esi
	imul eax,2
	call writeint

   exit
main endp
end main

````
![image](https://github.com/user-attachments/assets/4a63dbd5-b4fd-440c-a158-904aeadb4753)


TASK 06:
````
include irvine32.inc

.data 
    arr WORD 10, 4, 7, 14, 299, 156, 3, 19, 29, 300, 20

.code

bubblesort proto, arr1:PTR WORD, _size:BYTE

main proc
    invoke bubblesort, addr arr, lengthof arr
    exit
main endp

bubblesort proc, arr1:PTR WORD, _size:BYTE
    LOCAL temp:WORD, flag:BYTE
    LOCAL outer:BYTE

    movzx ecx, _size
    dec ecx
    mov outer, cl

L1:
    mov esi, arr1
    mov flag, 1          

    movzx ecx, _size
    dec ecx              

L2:
    mov ax, [esi]        ; AX = arr[i]
    mov dx, [esi+2]      ; DX = arr[i+1]
    cmp ax, dx
    jle cont             ; if arr[i] <= arr[i+1], no swap

    ; swap
    mov [esi], dx
    mov [esi+2], ax
    mov flag, 0

cont:
    add esi, 2
    loop L2

    cmp flag, 1
    je print              ; if no swaps, already sorted

    movzx ecx, outer
    dec outer
    jnz L1

print:
    mov esi, arr1
    movzx ecx, _size

print_loop:
    movzx eax, word ptr [esi]
    call WriteInt
    call Crlf
    add esi, 2
    loop print_loop

    ret
bubblesort endp

end main

````
![image](https://github.com/user-attachments/assets/8bde4db8-ca31-4939-ba88-a39ec986c10d)

TASK 07:
````
include Irvine32.inc

.data
    num dword ?
    m1 byte "Enter a number (0=Sat to 6=Fri): ",0

    d1 byte "Saturday ",0
       byte "Sunday   ",0
       byte "Monday   ",0
       byte "Tuesday  ",0
       byte "Wednesday",0
       byte "Thursday ",0
       byte "Friday   ",0

.code
main PROC

    mov edx, offset m1
    call WriteString

    call ReadInt
    mov num, eax

    mov ecx, 10
    imul eax, ecx        

    mov edx, offset d1
    add edx, eax         

    mov ecx, 10
print_loop:
    mov al, [edx]
    call WriteChar
    inc edx
    loop print_loop

    call Crlf

    exit
main ENDP
END main

````
![image](https://github.com/user-attachments/assets/aebaa303-45bf-4f85-86ce-40ac20f2950a)

TASK 08:
````
include Irvine32.inc

.data
   var byte ?
   m1 byte "Write Character: ",0
   m2 byte "Character is alphabet",0
   m3 byte "Character is not alphabet",0

.code
main PROC
    mov edx, offset m1
    call writestring
    call readchar
    call crlf

    cmp al,65
    jl not_alphabet
    cmp al,90
    jg check_capital
    mov edx, offset m2
    call writestring
    exit
    check_capital:
    cmp al,97
    jl not_alphabet
    cmp al,122
    jg not_alphabet
    mov edx, offset m2
    call writestring
    exit

    not_alphabet:
    mov edx, offset m3
    call writestring
    exit
main ENDP
END main
,
````
![image](https://github.com/user-attachments/assets/5e6c6bda-760e-40ee-a926-ba74394c25c6)


