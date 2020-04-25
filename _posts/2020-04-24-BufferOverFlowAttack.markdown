This week I am going to talk about buffer overflow attacks and how they work. 
Buffer overflow vulnerabilities have been around since the early days of computers 
and still exist today. Most Internet worms use buffer overflow vulnerabilities to propagate, 
and even the most recent zero-day VML vulnerability
in Internet Explorer is due to a buffer overflow.
C is a high-level programming language, but it assumes that the
programmer is responsible for data integrity. If this responsibility were
shifted over to the compiler, the resulting binaries would be significantly
slower, due to integrity checks on every variable. Also, this would remove a
significant level of control from the programmer and complicate the language.
While C’s simplicity increases the programmer’s control and the efficiency
of the resulting programs, it can also result in programs that are vulnerable
to buffer overflows and memory leaks if the programmer isn’t careful. This
means that once a variable is allocated memory, there are no built-in safeguards to 
ensure that the contents of a variable fit into the allocated memory
space. If a programmer wants to put ten bytes of data into a buffer that had
only been allocated eight bytes of space, that type of action is allowed, even
though it will most likely cause the program to crash. This is known as a
buffer overrun or buffer overflow, since the extra two bytes of data will overflow
and spill out of the allocated memory, overwriting whatever happens to
come next. If a critical piece of data is overwritten, the program will crash. 


These types of program crashes are fairly common—think of all of the
times a program has crashed or blue-screened on you. The programmer’s
mistake is one of omission—there should be a length check or restriction on
the user-supplied input. These kinds of mistakes are easy to make and can be
difficult to spot

The program that I had to break or cause an overflow was from a recent NCL
challenge.  There are a few programs that can help you discover that a program
is vulnerable to a buffer overflow.

gdb is a good one that will let you step your way through the program and see
what is happening and what is stored where.  It takes a bit of training to 
understand the commands and how to use the full power of this program.

	gdb <filename>
	break main
	run

Another good program is objdump which is easier to use but will dump the entire
program in assembly language.  This will allow you to view what is happening.

	objdump -d <filename>

![objdump](https://v1ndl3r.github.io/CIT480/assets/buffer1.PNG "objdump")


A much easier program to run that is extremely powerful is ghidra, it is a tool
made by the NSA and is much easier to use than others.

![ghidra](https://v1ndl3r.github.io/CIT480/assets/buffer2.PNG "ghidra")

We can see from this that you must provide a tid value, this was provided with 
the challenge.  It is just a 4 digit number. We can also see that char local_38 [44];
Is a char array of 44 bytes.  This is the buffer that we are going to overflow.

![buffer](https://v1ndl3r.github.io/CIT480/assets/buffer3.PNG "buffer")

You can see when less than 44 chars are used it fails, the second uses 45 chars and it
causes a dump and you can view the flag.
