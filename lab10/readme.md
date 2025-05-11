TASK 01:
```
include Irvine32.inc

.data
  x dword 3
  y dword 6
  z dword 9

.code

main proc 
   
    push z
    push y
    push x
    call SumThree
    exit
main endp

SumThree proc 
    push ebp
    mov ebp, esp

    mov eax, [ebp+8]    ; x
    add eax, [ebp+12]   ; y
    add eax, [ebp+16]   ; z

    call WriteInt
    call Crlf           

    pop ebp
    ret 12              
SumThree endp

end main

```
![image](https://github.com/user-attachments/assets/9f107787-9d47-401b-b33e-d2d436783215)


TASK 02:
````
include Irvine32.inc

.data
  arr1 dword 1,2,3,4,5,6,7,8,9,8,7,6,5,4,3,2
  m1 byte "Min: ",0
  m2 byte "Max: ",0
.code

main proc 
   
    push offset arr1
    call MinMaxArray
    exit
main endp

MinMaxArray proc 
    push ebp
    mov ebp, esp

    mov esi, [ebp+8]    

    mov ecx,lengthof arr1
    mov ebx,10000 ;min
    mov eax,0 ;max
    L1:
    cmp eax,[esi]
    jg cont
    mov  eax,[esi]
    cont:
    cmp ebx,[esi]
    jl next
    mov ebx,[esi]
    next:
    add esi,4
    loop L1

    mov edx, offset m2
    call writestring
    call WriteInt
    call Crlf           

    mov edx, offset m1
    call writestring
    mov eax,ebx
    call WriteInt
    call Crlf    
    pop ebp
    ret 4             
MinMaxArray endp

end main

````
![image](https://github.com/user-attachments/assets/b05ceb88-7719-4d3b-b30c-74209300cc0a)


TASK 03:
```
include Irvine32.inc

.data
  m1 byte "Enter Integer for Square ",0

.code

main proc 
   
    call LocalSquare
    exit
main endp

LocalSquare proc 
    enter 4,0
    mov edx,offset m1
    call writestring
    call readint
    mov dword ptr[ebp-4],eax

    mov ebx,eax
    mul ebx
    call writeint
    leave
    ret              
LocalSquare endp

end main

```
![image](https://github.com/user-attachments/assets/2b67220d-1908-41ed-bbd9-38ced3430be1)

TASK 04:

````
include irvine32.inc

.data
    arr dword 4 DUP(?)
    flag dword 0
    m1 byte "Enter Four Numbers: ",0
    m2 byte "All Entered numbers are not prime",0
    m3 byte "Not Prime",0
    m4 byte "Prime",0
    m5 byte "Maximum prime: ",0

.code

largestPrime proto,
    arr1:ptr dword

CheckPrime proto,
    num: dword

main proc
    mov edx, offset m1
    call WriteString
    call Crlf

    mov ecx, lengthof arr
    mov esi, offset arr
L1:
    call ReadInt
    mov [esi], eax
    add esi, 4
loop L1


    mov ecx, lengthof arr
    mov esi, offset arr

L2:
    mov eax, [esi]
    invoke CheckPrime, eax
    cmp eax, 0
    je not_prime

    mov edx, offset m4
    call WriteString
    call Crlf
    jmp cont

not_prime:
    mov edx, offset m3
    call WriteString
    call Crlf
    mov flag,1
cont:
    add esi,4
loop L2

cmp flag,0
jne calllargest
jmp ddone

calllargest:
invoke largestPrime,addr arr

ddone:
    exit
main endp

CheckPrime proc,
    num: dword

    mov eax, num
    cmp eax, 2
    jl Not_prime    
    cmp eax, 2
    je Is_prime

    mov ecx, eax
    shr ecx, 1        
    mov ebx, 2

CheckLoop:
    mov eax, num
    xor edx, edx
    div ebx
    cmp edx, 0
    je Not_prime
    inc ebx
    cmp ebx, ecx
    jle CheckLoop

Is_prime:
    mov eax, 1
    ret

Not_prime:
    mov eax, 0
    ret

CheckPrime endp

largestPrime proc,
    arr1:ptr dword

    mov esi,arr1
    mov ecx,lengthof arr
    mov eax,0
    L1:
    cmp eax,[esi]
    jg cont
    mov eax,[esi]
    cont:
    add esi,4
    loop L1

    mov edx, offset m5
    call writestring
    call writeint
     ret
largestPrime endp

end main


````
![image](https://github.com/user-attachments/assets/3685f60b-a23e-4c56-bb53-7f2b20ea20b1)

TASK 05:
```
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

```
![image](https://github.com/user-attachments/assets/1fa4de72-9e11-4011-9311-8f8a1f26ed1c)



