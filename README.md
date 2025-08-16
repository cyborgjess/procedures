[printletters.txt](https://github.com/user-attachments/files/21810952/printletters.txt)# procedures




1. thought process
   <img width="621" height="284" alt="procedures" src="https://github.com/user-attachments/assets/2bd4c7af-b378-4929-8861-010e5a618c1f" />


2. Challenges
   Ensuring registers used for system calls and letter storage weren’t overwritten.

   Properly pushing and popping registers to maintain the loop counter and letter across procedure calls.

   Initially mishandling stack operations caused strange output or terminal freezes.

3. Working Code:

  [printletters.txt](https://github.com/user-attachments/files/21810960/printletters.txt)
section .bss
buffer resb 1

section .data
newline db 0xA

section .text
global _start

_start:
    mov ecx, 26        
    mov al, 'A'       

print_loop:
    push ecx           
    push eax           

    mov esi, buffer
    mov [esi], al      

    mov eax, 4         ; sys_write
    mov ebx, 1         ; stdout
    mov ecx, buffer
    mov edx, 1
    int 0x80

    mov eax, 4
    mov ebx, 1
    mov ecx, newline
    mov edx, 1
    int 0x80

    pop eax            
    pop ecx            
    inc al             
    loop print_loop

    mov eax, 1         
    xor ebx, ebx
    int 0x80






   ![procedure](https://github.com/user-attachments/assets/82579b24-2ca0-43fc-aa17-20d3c7cc4301)
