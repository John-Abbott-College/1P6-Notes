# Day 4 - Programs and Languages
*Tuesday, August 30, 2022*

Let's take a look at how computers process the algorithm that we've written.

## CPU

The Central Processing Unit (CPU) is the computer component that **interprets and executes** the instructions described in our algorithms. 

The CPU can only understand instructions written in **machine language**.

Machine language is a set of LOW LEVEL binary codes that are hard-coded into the architecture of the CPU.

The CPU can:

- Read and write data from memory 
- Add, multiply, subtract, divide two numbers 
- Compare numbers 
- Move data from one location to another. 

All the above is done at incredibly fast speed. 

However, we don't write machine language, we are writing in a HIGH LEVEL language called C#.

A **high level language** is typically defined as:

> A programming language enables a programmer  to write programs that are more or less independent of a particular type of computer. Such languages are considered high-level because they are closer to human languages and further from machine languages
>
> In contrast, assembly languages are considered low-level because they are very close to machine languages.

The CPU is running the instructions of the Operating Systems (OS) - and the OS is managing the computer's hardware.

The CPU can also receive an **interrupt** while it is executing code. An interrupt is an important notification such as moving a mouse, hitting a key on the keyboard.
Once the CPU receives an interrupt, it asks the OS what is the code to be run for that particular interrupt (Ex.: update the mouse position and repaint the screen).


## How a Program Works

A program is software - it is a series of instructions that carries out a specific task. This could be a game, your browser, an app, etc. Usually stored on the storage drive of your computer.

When a program is executed, 

1. The OS is informed that ***this*** program, located ***here*** on the disk needs to be executed.  

2. The OS will then instruct the IO chip to copy the program (or part of it) into the internal memory (RAM).

3. Once there, the OS instructs the CPU to begin executing the code located in RAM.

4. The CPU uses RAM as a temporary scratchpad between itself and an external storage device (usually a hard disk or USB key).

> **RAM is volatile**, meaning that when the computer loses power, **everything is lost**.

5. The memory management unit (MMU) manages the movement from RAM to memory within the CPU (CPU cache).

6. The speed of access between the CPU and the RAM is far faster than accessing the storage device (even an SSD drive).

7. When a CPU executes instructions it does a *fetch - decode - execute* Cycle 

  - **Fetch** - the instruction is retrieved from memory - or a cache very close to the CPU. This means that the program may have originally lived on a hard disk - but it was copied into RAM so that the CPU has high speed access to it. 
  - **Decode** - a binary bit pattern interpreted as an instruction - not data - that tells the CPU what to do 
  - **Execute** - the instruction is done.

![How programs execute code<br>Rectangle on left indicates RAM.  Out of ram is a ribbon of ones and zeros going to another rectangle on the right, indicating the MMU (memory management unit).  The ribbon passes through the MMU and feeds into another rectangle representing the CPU.  Inside the CPU rectangle, there is a picture of a calculator, as well as glasses and a piece of paper (indicating read/writing properties).  From the 'reading/writing' part of the CPU, another ribbon with ones and zeroes, snakes out to the left, passing through the MMU and ending at the rectangle indicating the RAM.<br> When the ribbon of binary goes from left to right from the RAM to the CPU, it is indicated as FETCH.<br> Where the ribbon of binary enters the CPU, a little brain is drawn, and it is indicated as DECODE.  <br>The calculator is indicated as 'EXECUTE' ](../Images/04_how_programs_execute.png)

**Figure 1** How programs execute code


## Levels of Language

### Low level languages

**Machine language** is store in binary: `10110110  10101011 … `

The CPU has small amounts of storage called **registers**, where it holds the instruction and the values of what is currently being executed and what will be executed next.

Registers have names like - PC (program counter), SP (stack pointer), R1 (register 1), R2 (register 2), etc…

**Assembly Language** is a level above machine language and has instructions like MOV R1, R1  JNZ R3  JMP R4. Each assembly instruction can be translated directly into binary code.

Example:

> Add 25 to the contents of the register `AX`
>
> `ADD AX,25`
>
> According to **Intel® 64 and IA-32 Architectures Software Developer’s Manual Volume 2 (2A, 2B, 2C & 2D): Instruction Set Reference, A-Z**
>
> the binary machine code is:
>
> ```0000 0011 0001 1001```


In a way you can think of an assembly language as a language that manipulates binary code. 

### High Level: 

**C#, Java, Python** older ones: **Fortran, Cobol** - 

These are very very English-like!!!! We code at a high level - meaning we do not deal with binary, we create variables, loops, arrays, structures etc. 

>  Think about this - if we write a C# program in "English" - how does the CPU understand this????? I thought the CPU only understands binary??? 

Great Question!!! Glad you asked! 


## Compilers & Interpreters 

### Compile and Link

A Compiler: a program that translates high level language programs into a separate machine language program. This way the CPU can understand it! 

> **The machine language that is produced MUST match the hardware where the program will eventually be executed**

A compiler will typically produce an object ( `*.obj`) file. This file may not be *complete* because it may be missing code from another set of program files.

Thus,  one or more object files are joined together via the *link* process which will produce an executable (`*.exe`) that can run on the target platform.

All this is done for you when you click the appropriate menu option (build) or button (play or lightning bolt) in your IDE (tool to create programs)

> Compilers are language specific - a compiler for C# is different than a compiler for Java!!!! 

> Changes to a program must be done at the high level language. Then the program is re-compiled and distributed.

![Compiling C++ : Three rectangles at the top of the picture are indicated as C++ source code.  Arrows from each source code pass through another rectangle labeled COMPILER. The arrows terminate at three circles, labeled OBJECT FILE.  There is one object file for each C++ source code.  A side text indicates that each object file is 'almost machine language'. Another circle indicates 'RUNTIME LIBRARY'.  There are four arrows leading from the runtime label, and the three object files to a box labelled 'LINKER'.  From the linker, a large dotted line leads to a square, inidicated as the 'APPLICATION FILE'. ](../Images/04_compiling_cpp.png)
**Figure 2** Compiling a high level language to create an executable file

![Running the executable file: The square as 'APPLICATION FILE' from figure 2 is drawn at the right.  From this square, a ribbon of ones and zeros goes into another square, labelled as the CPU.  There is a dotted arrow from the CPU to an application icon (a clock) which is labelled APPLICATION](../Images/04_running_executable.png)
**Figure 3** Running an executable file

### Virtual Machines and JIT (just in time) compilers

Java and C# do not compile to machine language, instead they have developed a *new* low-level languages that are independent of the machine they are running on.
* Java compiles to byte code
* C# compiles to MSIL (Microsoft Intermediate Language)

When the program is *executed*, what really happens is:
* Java: the JVM program (Java Virtual Machine) will read the byte code, and *interpret* or *compile* the byte code, translating it to machine language, which is sent to the CPU as required.
* C# (any .NET): The OS will read the MSIL, and *interpret* or *compile* the MSIL, translating it to machine language, which is sent to the CPU as required.

![Compiling Java code: Three rectangles at the top of the picture are indicated as Java source code.  Arrows from each source code pass through another rectangle labeled COMPILER. The arrows terminate at three circles, labeled BYTE Code.  There is one byte code file for each java source code.  A side text indicates that each byte source file is 'a very simple machine language'. ](../Images/04_compiling_java.png)
**Figure 4** Compiling Java code

![Running java byte code: A circle representing a byte code file (the output of java compilation described in previous pciture) has a ribbon with byte code written on it.  This ribbon enters the CPU.  Inside the cpu, a section of it is described as the JVM (java virtual machine).  The ribbon goes in as byte code and comes out as binary code.  The ribbon re-enters the CPU to be executed.  There is a dotted arrow from the CPU to an application icon (a clock) which is labelled APPLICATION. ](../Images/04_running_java_code.png)
**Figure 5** Running byte code

### Interpreter: 

A program that translates and executes instructions immediately as the line of code is parsed.  So for example Javascript - it takes one line of Javascript, translates it into machine code, sends it to the cpu, rinse and repeat, line by line. 

![Interpreting bash : A rectangle representing a bash file is drawn on the left.  A ribbon with the words 'echo "hello" comes from the bash file and enters the CPU.  Inside the cpu, a section of it is described as the 'bash interpreter'.  The riggon goes in as a bash command (echo "hello" and comes out as binary code.  The ribbon re-enters the CPU to be executed.  There is a dotted arrow from the CPU to an application icon (a clock) which is labelled APPLICATION.](../Images/04_interpreting_bash.png)
**Figure 6** Running bash code

Because it will repeat this for every instruction in a program, loops can be slow 

## Open Source vs Closed Source

### Closed Source

You have written a program that you wish to sell.  If you buy my program, I will sell you the executable binary compiled version.  My high level instructions that yielded that executable are a trade secret!!! I will never disclose my "source code". You will only get the binary. 

More importantly, if you make a new and improved version, you want to be able to sell your upgraded program. So your company would take the source code, make the changes at the high level, recompile, and sell the executable. 

If the source code is leaked to the public, then everyone who has it and can go wild with changes, make their own improvements, and never have to buy from you again.  This is why commercial products rarely release their source code, which is *guarded*. 

### Open Source

The programming community likes to share ideas and code.  *Open source code* is code where anyone can view the source code at will.  Many programs that you are familiar with (`Linux operating system` `bash` `perl` `python` `ruby` `gcc (gnu c compiler)`) are open source.  

The advantages of open source software are:

* can be more secure because so many people are looking at the code, if there is a security flaw that is noticed, it is quickly fixed
* sometimes code can do weird things, but at least with open source code, you can search the code to figure out what it is doing, and maybe come up with a work around

> Not all open source code is free, but usually it is.  

#### Modification and Redistribution

Most open source program allow anyone to modify the code at will, but they may not be allowed to distribute the modified code using the licensed name.  Example, you may modiy the 'Tex' program, but you may not call it 'Tex' if you are giving it to someone else.

You may not always be allowed to redistribute open source software.  Always check the license agreements


## Program Development Cycle

Design the program → Write Code → Correct Syntax → test executable → debug the code→ (and wrap around) 

It is best to only write a small portion of code, test that code, before continuing.

If I have written 100 lines of code, I may have many mistakes, and it is hard to find them, because even if I find one mistake, my program will still not run properly because of other mistakes.

However, if I have written only 10 lines of code, hopefully I will not have more than one mistake.  Ideally no mistakes, but that is unlikely.