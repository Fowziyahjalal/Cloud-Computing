# Ex.No 02 – Virtual Machine: C Compiler

## Aim
To install a C compiler in the virtual machine created using VirtualBox and execute simple programs.

## Tools Used
- VirtualBox
- Tiny Core Linux (CorePlus) guest OS
- `tce-load` package manager, GCC

## Procedure
1. Install VMware/VirtualBox player and host the virtual machine (CorePlus).
2. Open the workstation and power on the virtual machine.
3. After the guest OS loads, open the terminal and run:
   ```
   tc@box:~$ tce-load -wi compiletc
   ```
4. Wait for all dependencies (`compiletc`, `bison`, `gettext`, `file`, etc.) and GCC to download and install.
5. Open the terminal and run:
   ```
   sudo editor
   ```
   Type your C program in the text editor that appears and save it with a `.c` extension.

   Example program (leap year check):
   ```c
   #include<stdio.h>
   int main()
   {
       int y;
       printf("Enter the Year");
       scanf("%d",&y);
       if(y%4==0)
       {
           if(y%100==0)
           {
               if(y%400==0)
                   printf("%d is a Leap Year");
               else
                   printf("%d is not Leap Year");
           }
           else
               printf("%d is a Leap Year");
       }
       else
           printf("%d is not Leap Year");
       return 0;
   }
   ```
6. Exit the editor with `CTRL+Q` to return to the terminal.
7. Compile the program:
   ```
   tc@box:~$ cc demo.c
   ```
8. Run the compiled program:
   ```
   tc@box:~$ ./a.out
   ```

   Sample output:
   ```
   Enter year: 1991
   1991 is not a Leap Year
   ```

## Result
A C compiler was successfully installed in the virtual machine, and a simple C program was compiled and executed.
