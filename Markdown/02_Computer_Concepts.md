# Day 2 - Computer Concepts



Wednesday - August 25, 2021

- **Hardware** - the physical devices that make up a computer 
  - Keyboard. Mouse, input devices 
  - Monitor, and output devices 
  - Secondary storage devices 
  - Main memory 
- **Software** - logiciel 
  - Series of instructions stored on hardware that carries out a specific task. 
    - Ex: games, programs that do inventory, programs that manage things, etc etc. 
- **Firmware**
  - Firmware is also a set of instructions, but instead of living in some kind of hard-drive or memory, the instructions are written into the hardware itself (by changing the nature of the transistors within the chip)
- **C.P.U.** Central Processing Unit - it is effectively the brain and/or decision maker in a computer. The CPU has two components within it - they are called the Control Unit and the ALU (arithmetic logic unit).  
  - Flashy names ex: intel Core i7, Celeron, Pentium, AMD Athlon 
  - Each CPU has a model number and a speed - measured in GHz.  
- **MMU** Memory Management Unit - manages the memory by reading/writing data to RAM at the request from the CPU (i.e. CPU asks the MMU to read from a certain memory address)
- **I/O** Input / Output - manages the flow of data between periphials and the Main memory (RAM) 
- Main Memory - computer’s work area - where the computer stores a program as it is being run. Also called **RAM** - random access memory. Memory has addresses. 
- Secondary storage devices - hard drives, USB drives (memory sticks) 
- Your Operating System - this is software!!!! - brand names include Windows, iOS etc….. They make juvenile names like “El Capitain” and code names for versions. 
  - In reality - an operating system tells the CPU how to manage the peripherals. Peripherals are things connected to the computer. 
  - O/S (Operating System) does a lot of things including boot up, memory management, drivers etc... 
- Your operating system does many things - including manage memory, allocating who can do what when (scheduling), scan for hardware interrupts, run programs etc.  
- Low level programming deals directly with hardware and binary signals. It deals with very primitive code. We are using/examining Binary codes. Languages that are CPU specific such as Assember and other. 
- High level programming are “English Like” languages that are converted to binary for you. Examples: C#, Perl, ASP, Python, etc… 
  - Hi level programming is not "better" than low level programming!!!!! Low level could be sending binary signals to a piece of hardware. High level could be writing a database application. Low level deals with binary codes and not English like words. 

 

## Translating human language to computer hardware language

- Everything begins at a plug or power source!!!! Electricity goes along a wire! 

- In computers we send pulses of electricity along a wire. These pulses are either zero or five volts. 

![A graph of voltages along a wire.  The y-scale is from LOW to HIGH, and the title for the y-scale is 'Logic Levels'.  The x-scale is time, although it is divided into equal slices, where each slice represents a bit.  Under each bit (or pulse) the *value* of the bit is listed as either a 1 or zero.  If the graph height is *height* then the value of the bit is '1'.  If the graph height is 'low', the bit value is given as '0'.  It is typical that *heigh*t is 5 volts, and *low* is zero volts.](../Images/02_voltage.png)

There are two states along the wire. Nothing else. 

### Characters

Each letter of the English alphabet is mapped to a series of 7 UNIQUE pulses of electricity that form a pattern.  This mapping is called ASCII - American Standard Code for Information interchange. With addition of more pulses, all language symbols can be represented on a computer.  This encoding is called 'unicode'.

In textbook it would be very hard to write that the letter 

>  A = zero volts, five volts, zero volts, zero volts, zero volts, zero volts, zero volts, five volts 

This is tedious….. Wouldn't it be nice if we used the number "1" to represent 5 volts, and the number "0" to represent zero volts. 

So now I can say 

> A = 01000001  and this the unique sequence for the letter A. 

This use of "0" and "1" to represent voltage is what is used in computers. It is a **BINARY** system. Note that each letter uses 8 pulses. 



Take a look at this ASCII CHART https://www.ascii-code.com/ 

| Decimal | Octal | Hex | Binary | Character | HTML | Description |
| ---- | ---- | ---- | -------- | ---- | ----- | ----------- |
| 65   | 101  | 41   | 01000001 | A    | &#65; | Uppercase A |
| 66   | 102  | 42   | 01000010 | B    | &#66; | Uppercase B |
| 67   | 103  | 43   | 01000011 | C    | &#67; | Uppercase C |
| 68   | 104  | 44   | 01000100 | D    | &#68; | Uppercase D |
| 69   | 105  | 45   | 01000101 | E    | &#69; | Uppercase E |

From <https://www.ascii-code.com/> 

 

So you see A = 01000001  and D = 01000100 - notice how each letter is 8 pulses. 

### Terminology

In Computer Science we call a "1" or a "0" a **BIT**. 8 Bits together makes up a letter of the English language from the ASCII chart. 

We have "words" to denote quantities as well: 

 

8 bits is a **byte**, In French we call this "un octet" 
> A byte is the minimum amount of bits you need to represent a character or letter of the alphabet 

4 bits is a **nibble** (half a *byte*)

1024 bytes is a **K** or **KB** **Kilobyte** 

1024 **KB** is a **Megabyte MB** 

1024 MB is a **Gigabyte** or a "**Gig**" 

1024 GB is a **Terabyte** **TB** - etc etc look it up after this…. 

people blur this line and sometimes say 1000 GB is a TB….reality is it is 1024... 


### Numbers

Another thing to think about is we have to use these BITS to represent numbers as well….. Think about this….. We use 0, 1 to represent voltages and we agreed that 8 pulses together could form a letter of the English language….  

But…. What if I need to put in a real number???? How would I represent the number 8 on a computer? Or any number for that mattter? 

The answer is we use the Binary number system 

| Real English Number | Binary Pattern |
| ------------------- | -------------- |
| 0                   | 0 (Zero Volts) |
| 1                   | 1 (5 volts)    |
| 2                   | 10             |
| 3                   | 11             |
| 4                   | 100            |
| 5                   | 101            |
| 6                   | 110            |
| ….and so on         | And so on…     |

 

This is our binary number system and it is often called BASE 2 number system. 

Bit patterns don't always represent letters! Sometimes we need them to represent numeric quantities as well. For example the numeric quantity one hundred and fifty seven. How would I represent this in binary? 

*Answer*: 

10011101 = 157 here we interpret the bit pattern as a number and it equals one hundred and fifty seven. 

  

7   6   5  4  3  2 1  0   bit – notice how you begin by ZERO position   

1   0   0  1  1  1 0  1 = 157 - but how??? Why? 

  

Well let’s think about “regular” numbers or our own decimal system. Think back to what you were taught about regular "decimal numbers" - You were taught that 

  

4352 = The 2 is in the ones column, the 5 is in the tens column, and the 3 is in the hundreds column and 4 is in the thousands column. So it’s 2x1 +  5x10  + 3 x100  + 4 x 1000 which equals 4352! 

In reality you could look at it like this: 

| Digit | Base or Number System | Digit Position <br>– which becomes exponent | Math expression      | Value |
| ----- | --------------------- | --------------------------------------- | -------------------- | ----- |
| 2     | 10 (decimal)          | 0                                       | = 2 x 10<sup>0</sup> |   2 |
| 5     | 10 (decimal)          | 1                                       | = 5 x 10<sup>1</sup> | 50 |
| 3     | 10 (decimal)          | 2                                       | = 3 x 10<sup>2</sup> | 300   |
| 4     | 10 (decimal)          | 3                                       | = 4 x 10<sup>3</sup> | 4000  |
|       |                       |                                         | Total sum:           | 4352  |



So now let’s get back to the “how is binary 10011101 = 157 decimal??” issue 

| Digit | Base or Number System | Digit Position <br>– which becomes exponent | Math expression | Value |
| ----- | --------------------- | --------------------------------------- | --------------- | ----- |
| 1     | 2 (binary)            | 0                                       | = 1 x 2<sup>0</sup>        | 1     |
| 0     | 2 (binary)            | 1                                       | = 0 x 2<sup>1</sup>        | 0     |
| 1     | 2 (binary)            | 2                                       | = 1 x 2<sup>2</sup>        | 4     |
| 1     | 2 (binary)            | 3                                       | = 1 x 2<sup>3</sup>        | 8     |
| 1     | 2 (binary)            | 4                                       | = 1 x 2<sup>4</sup>        | 16    |
| 0     | 2 (binary)            | 5                                       | = 0 x 2<sup>5</sup>        | 0     |
| 0     | 2 (binary)            | 6                                       | = 0 x 2<sup>6</sup>        | 0     |
| 1     | 2 (binary)            | 7                                       | = 1 x 2<sup>7</sup>        | 128   |
|       |                       |                                         | Total sum:      | 157   |

  

Don’t panic if you don’t fully understand binary to decimal and decimal to binary conversion. This will be covered in more detail in your other courses. You should observe that fourth column of the table above is 2 to the power of zero, one, two, three, four, five, and so on. This is why we have “funny” numbers in computer science like 0, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024, etc…. 

1024 Bits is a “**K**” and often people think a “**K**” means a thousand (like “kilo”). But in Computer Science a “K” is 1024. It has to do with the binary base 2 being raised to the power of 10 

