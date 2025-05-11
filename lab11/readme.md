TASK 01:
````
INCLUDE Irvine32.inc

.data
    Str1 BYTE "127&j~3#^&*#*#45^",0
    m2 BYTE "Letter Not found",0

.code

Scan_String PROTO arr:PTR BYTE, w:BYTE

main PROC
    INVOKE Scan_String, ADDR Str1, '#'
    exit
main ENDP

Scan_String PROC arr:PTR BYTE, w:BYTE
    push edi                
    mov edi, arr           
    mov al, w              
    mov ecx, lengthof Str1   
    cld                    
    repnz scasb            
    jnz NotFound           

    mov eax, lengthof Str1  
    sub eax, ecx           
    dec eax                
    call WriteInt
    call Crlf
    pop edi
    ret

NotFound:
    mov edx, OFFSET m2
    call WriteString
    call Crlf
    pop edi
    ret
Scan_String ENDP

END main

````
![image](https://github.com/user-attachments/assets/a52a6330-756b-43a2-8736-fe7ec0851aad)


TASK 02:
````
INCLUDE Irvine32.inc

.data
    Str1 BYTE "127&j~3#^&*#*#45^",0
    m2 BYTE "Letter Not found",0

.code

Scan_String PROTO arr:PTR BYTE, w:BYTE

main PROC
    INVOKE Scan_String, ADDR Str1, '#'
    exit
main ENDP

Scan_String PROC arr:PTR BYTE, w:BYTE
    push edi                
    mov edi, arr           
    mov al, w              
    mov ecx, lengthof Str1   
    cld                    
    repnz scasb            
    jnz NotFound           

    mov eax, lengthof Str1  
    sub eax, ecx           
    dec eax                
    call WriteInt
    call Crlf
    pop edi
    ret

NotFound:
    mov edx, OFFSET m2
    call WriteString
    call Crlf
    pop edi
    ret
Scan_String ENDP

END main

````
![image](https://github.com/user-attachments/assets/a037f123-7e0a-43e8-baa3-a2cedf9ae2bb)


TASK 03:
````
INCLUDE Irvine32.inc

.data
   s1 BYTE "Hello",0
   s2 BYTE "Hello w",0
   m1 BYTE "Both Strings are same",0
   m2 BYTE "Both strings are not same",0

.code

IsCompare PROTO,
 str1:PTR BYTE, str2:PTR BYTE, len:DWORD

main PROC
    INVOKE IsCompare, ADDR s1, ADDR s2, LENGTHOF s1
    exit
main ENDP

IsCompare PROC,
 str1:PTR BYTE, str2:PTR BYTE, len:DWORD

    mov esi, str1
    mov edi, str2
    mov ecx, len
    cld
    repe cmpsb              

    jz strings_equal        
    mov edx, OFFSET m2
    call WriteString
    jmp done

strings_equal:
    mov edx, OFFSET m1
    call WriteString

done:
    ret
IsCompare ENDP

END main

````
![image](https://github.com/user-attachments/assets/d90c994a-af15-43e3-aa29-a7d187708e4d)


TASK 04:

`````
INCLUDE Irvine32.inc

.data
  arr byte "HEllo World",0

.code

Str_Reverse proto,
    arr1:PTR byte,len:dword

main PROC
    INVOKE Str_Reverse, ADDR arr, lengthof arr
    mov edx, offset arr
    call writestring
    exit
main ENDP

Str_Reverse proc,
    arr1:PTR byte,len:dword
    mov ecx,len
    shr ecx, 1   
    mov esi,arr1
    mov edi,arr1
    add edi,len
    sub edi,2
    
    L1:
    mov al,[edi]
    mov bl,[esi]
    mov [edi],bl
    mov [esi],al
    inc esi
    dec edi
    loop L1
    ret
Str_Reverse endp

END main

`````
![image](https://github.com/user-attachments/assets/64bcf9fc-f22a-4ff6-9392-e83c631dc4d7)



TASK 05:
````
INCLUDE Irvine32.inc

.data
  arr byte 1,2,3,4,5,6,7,8,9
  multi byte 20
.code

LOAD proto,
    arr1:PTR byte,multiplier:byte

main PROC
    INVOKE LOAD, ADDR arr, multi
    mov ecx,lengthof arr
    mov esi,0
    mov eax,0
    L1:
    mov al,arr[esi]
    call writeint
    call crlf
    inc esi
    loop L1

    exit
main ENDP

LOAD proc,
    arr1:PTR byte,multiplier:byte
    mov esi,arr1
    mov edi,arr1
    mov ecx,lengthof arr

    L1:
    lodsb
    mul multiplier
    stosb
    loop L1
    ret
LOAD endp

END main


````
![image](https://github.com/user-attachments/assets/45448b8e-0b77-409f-8192-ad811f3c6282)



