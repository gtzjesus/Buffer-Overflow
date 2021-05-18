Jesus Gutierrez
Buffer Overflow

Task #1:

	Initial Setup:
		
		To make the attack easier for me, I first must disable the address space randomization. Let’s recall that space randomization is a defense against buffer overflows which makes guessing addresses in the heap and stack more difficult. Under the root privileges, I had to run the following commands:

 

	The Vulnerable Program ‘stack.c’:

		So firstly, this c file needs to be made a set-root-uid in order for the exploiting of the buffer overflow to be able to function properly by giving the ability to gain access to a root shell. As you know, the Stack Guard option is enabled by default, I was able to disable it at compile time in this task as well as the next task. Lastly, to make this file execute properly, i had to “chmod” the permissions to 4755:

 
 

	Note: I was able to use the executable stack option to be able to run the shellcode from the actual buffer that was implemented.

Demonstration:
	
	Actually, Exploiting the Vulnerability:

		In this next task, the badfile must be crafted adequately. This file will be read by the vulnerable program ‘stack.c’ and will be stored into the buffer where then it will be overflowed. File provided ‘exploit.py’, I was having difficulty with python towards this method, ended up switching the language to c-programming which will contain code that basically will dump the buffer in order for the vulnerable program to read it. Same name just extension would be ‘exploit.c’.

To demonstrate the buffer overflow attack, I ran following commands:

 
 
 

Note: these commands will simply compile and run the exploit file.

What happens when we compile and run the file?
-	The exploit file will evaluate the stack pointer and will craft a buffer that will follow saving it to the badfile that will be generated. This is strictly done with the stack pointer and the shellcode.
-	After this step, the program ‘stack.c’ will then be executed, resulting in reading the badfile and will load the buffer. When the buffer loads, it will trigger the buffer overflow and will execute the shellcode.
-	After previous step, it will give us a root shell.
-	An additional .c file was implemented named ‘set_uid_root.c’. This file is important because it is what gives us the root shell. This root shell that is obtained is still using the user ID. This file must be run effectively in order to have both the real and effective used IDs.

Task #2:

Defeating Address Randomization:
	
	Running the task that was provided in the assignment gives me a segmentation fault (core dumped) error.
Im thinking that this is given most likely because the address is randomized each time the program is executed.
	Also because the stack pointer is different.
	The exploit.c program will not set the address properly anymore for the buffer flow to run the shellcode.
