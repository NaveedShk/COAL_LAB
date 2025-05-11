TASK 01:
````
include irvine32.inc
.data
	arr WORD 1,2,3,4,5,6,7,8
	brr WORD 8 DUP(0)
.code
main proc
	
	mov ecx,lengthof arr
	mov esi,0

	L1:
	push arr[esi]
	add esi, type arr
	loop L1
	
	mov ecx,lengthof arr
	mov esi,sizeof arr - type arr 
	L2:
	pop ax
	mov brr[esi],ax
	sub esi, type brr
	loop L2
   
   mov ecx,lengthof arr
   mov esi,0
   L3:
   movzx eax,brr[esi]
   call writedec
   call crlf
   add esi, type arr
   loop L3

   exit
main endp
end main

````
![image](https://github.com/user-attachments/assets/7ff6f53a-7938-448f-a9d7-e195d7372136)


TASK 02:
````
include irvine32.inc
.data
	a dword 3
	b dword 3
	d dword 3
.code
main proc
	push a
	push b
	push d

	pop eax
	pop ebx
	add eax,ebx
	pop ebx
	add eax,ebx

	call writedec 
	call crlf
   exit
main endp
end main

````
![image](https://github.com/user-attachments/assets/9b1b03f9-9ae3-4ca0-b392-086314d672cc)


TASK 03:
````
include irvine32.inc
.data
	arr dword 1,2,3,4,5
	brr dword 6,7,8,9,10
.code
main proc
	mov eax,0
	mov ebx,0
	call first_array
	call second_array
	call add_nums
	call writeint
   exit
main endp

first_array proc
	mov ecx, lengthof arr
	mov esi,0
	L1:
	add eax,arr[esi]
	add esi, type arr
	loop L1
	ret
first_array endp

second_array proc
	mov ecx, lengthof brr
	mov esi,0
	L2:
	add ebx,brr[esi]
	add esi, type brr
	loop L2
	ret
second_array endp

add_nums proc
	add eax,ebx
	ret
add_nums endp

end main

````
![image](https://github.com/user-attachments/assets/93c87e6d-0d90-4024-9d04-f95ab737b326)


TASK 04:
````
include irvine32.inc
.data
	cols dword 5
.code
main proc
	call Print_Loop	
   exit
main endp

Print_Loop proc
	 mov eax,1
	 mov ecx,cols

	 L1:
	 
	 push ecx
	 push eax
	 mov ecx,cols
	 sub ecx,eax

	 Gap:
	 cmp ecx,0
	 jle exit_gap
	 mov eax,32
	 call writechar
	 loop Gap

exit_gap:
	 pop eax
	 mov ecx,eax
	 push eax
	 Star:
	 cmp ecx,0
	 jl exit_star
	 mov eax,42
	 call writechar
	 loop Star

exit_star:
	 pop eax
	 pop ecx
	 inc eax
	 call crlf
	 loop L1
	 ret
Print_Loop endp

end main

````
![image](https://github.com/user-attachments/assets/9df329cb-e32f-4ed1-99b4-d30f4cba1bbd)


TASK 05:
````
include irvine32.inc
.data
	m1 byte "Enter Natural Number  ",0
.code
main proc
	mov eax,0
	call SunmOfNatural
	call writeint
   exit
main endp

SunmOfNatural proc
	 mov edx,offset m1
	 call writestring
	 call readint
	 mov ecx,eax
	 mov eax,0
	 L1:
	 add eax,ecx
	 loop L1
	 ret
SunmOfNatural endp

end main

````
![image](https://github.com/user-attachments/assets/c48701cd-2ecd-4660-a110-582377151b42)




