TASK 02 (A):
````
include irvine32.inc
.data
	temp byte ?   

.code
main proc
       
    mov ecx, 4     
    mov eax, 1
    mov ebx, 1
L1: 
    mov edx, ecx
    mov ecx,ebx
    L2:
    call writedec
    loop L2
    call crlf     
    mov ecx, edx    
    inc ebx
    loop L1       
    exit
main endp
end main

````
![image](https://github.com/user-attachments/assets/12b9ea9b-65a7-4e5a-983b-d753e2ebd226)

b.

````
include irvine32.inc
.data
	temp byte ?   

.code
main proc
    mov eax, 1     
    mov ecx, 4     

L1: 
    mov edx, ecx  
    L2:
    call writedec 
    loop L2
    call crlf     
    mov ecx, edx    
    loop L1       

    exit
main endp
end main

````
![image](https://github.com/user-attachments/assets/a4efc725-36df-4a0d-8018-2659bf230981)


C.
````
include irvine32.inc
.data
	temp byte ?   

.code
main proc
       
    mov ecx, 4     

L1: 
    mov eax, 4  
    mov edx, ecx  
    L2:
    call writedec
    dec eax
    loop L2
    call crlf     
    mov ecx, edx    
    loop L1       

    exit
main endp
end main

````
![image](https://github.com/user-attachments/assets/2479ba4c-1422-4a8e-b296-561f5d665e6c)

D.
```
include irvine32.inc
.data
	temp byte ?   

.code
main proc
       
    mov ecx, 4     

L1: 
    mov eax, 1  
    mov edx, ecx  
    L2:
    call writedec
    inc eax
    loop L2
    call crlf     
    mov ecx, edx    
    loop L1       

    exit
main endp
end main

````
![image](https://github.com/user-attachments/assets/d9a230a1-17ad-4e3d-96e1-89fd56aea4c9)


TASK 03:
````
include irvine32.inc

.DATA
  
   id dword 5 DUP(?)
   n byte 5 DUP( 40 DUP (?)) 
   year dword 5 DUP(?) 
   salary dword 5 DUP(?) 
   promt byte "Enter the following : Employees Name,ID,Y_O_B,Salary",0
   promt1 byte "Enter Emplyee number: ",0
   totalsalary byte "Annual Salary: ",0
   temp dword 1
   strecx dword ?
.CODE
MAIN PROC

       mov ecx,2
       mov esi,0
       mov ebx,0 
       mov edx, offset promt
       call writestring
       call crlf

     
       L1:
       mov edx, offset promt1
       mov eax,temp
       call writestring
       call writedec
       call crlf

       mov edx, OFFSET n
        mov eax, esi
        imul eax, 30
        add edx, eax
        call ReadString

       call readint
       mov id[esi],eax
       call readint
       mov year[esi],eax
       call readint
       mov salary[esi],eax
       add ebx,eax
       add esi,4
       inc temp
       LOOP L1

      
       mov eax,ebx
       mov edx, offset totalsalary
       call writestring
       call writedec
       call crlf

       mov ecx,2
       mov esi,0
       L2:
       mov eax,id[esi]
       call writedec
       mov eax,year[esi]
       call writedec
       mov eax,salary[esi]
       call writedec
       call crlf
       add esi,4
       LOOP L2


    exit
MAIN ENDP
END MAIN

````
![image](https://github.com/user-attachments/assets/70af133b-5f32-4f6a-908d-624fb08d31e6)

TASK 04:
````
include irvine32.inc

.DATA
    source byte "this is the source string",0
    target byte 12 DUP(?)
    m1 byte "Source String: ",0
    m2 byte "Destination String: ",0
.CODE
MAIN PROC

    mov edx,offset m1
    call writestring
    mov edx,offset source
    call writestring
    call crlf

    
    mov esi,0
    mov ecx,lengthof source
    L1:
        mov al,source[esi]
        mov target[esi],al
        inc esi
    LOOP L1

  
    mov edx,offset m2
    call writestring
    mov edx,offset target
    call writestring
    call crlf
    exit
MAIN ENDP
END MAIN

````
![image](https://github.com/user-attachments/assets/be0e59a3-d463-474e-9ac2-f11e4f571776)


TASK 05:
````

````




