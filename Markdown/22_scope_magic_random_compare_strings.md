

# Scope

*Larry's notes*

> This is a very important topic, but it is not difficult if you think of "houses". And each variable is born in a house!  Also - I want you to remember that you are a psychopathic arsonist and you burn down your houses as you leave them! Remember the rule: first look for a variable in your house (Local Variables), if you can't find it there, then look on the street (Global Variables) 
>
> All variables "born" in a house are local to that house - they can only be seen/used if you are currently STANDING in that house. These are called "local variables" in that function. You call them Kids in your house. 
>
> Global Variables are born outside of functions and can be accessed from ANY house because those variables (Global ones) are born "on the street" and you can see everything on the street from ANY house. 
>
> But remember - first look the variable locally, if you cannot find it, look on the street. If you cannot find it, your program crashes - "undefined variable". 
>
> Yes - you can have local variables with the same name as globals - but remember - first your house, then the street. 

*Sandy's Explanation*

* Variables *hide* in curly braces where they are declared!

* Variables are available to anything within their curly braces, even embedded curly braces.

* Once the code *sees* a close curly brace, all the variables declared within that code block will be erased from memory, as if they never existed.

If the variable is declared in the class, but not a function, they are called **global variables**. If they are defined within a function, they are called **local variables**.  If they are defined within a loop, sometimes they are called **temporary variables**.

**Defining Global Variables**

To define global variables, you must specify `static` in front of the name

**Example** (with error)

```csharp
    class MainClass
    {	// curly brace #1
				static int x = 0 ;   // available everywhere in this class
      
        public static void Main(string[] args)
        { // curly brace #2
          
          	double yourNumber;	// available everywhere in this function

            // === Do while ===
          	do 
            { // curly brace #3
	            Console.Write("Please enter a number: ");
              // answer is only availabe inside curly brace #3 set
            	string answer = Console.ReadLine(); 
            } // end curly brace #3
          	// the while statement will not compile because
            // answer is not available outside of curly brace #3
            while(double.TryParse(answer, out yourNumber));
            
            Console.WriteLine("Your number is: " + yourNumber);
          
            x = yourNumber; // x is global, so I can use it here
          
        } // end curly brace #2
    } // end curly brace #1

```

**Example** (fixed)

```csharp
    class MainClass
    {	// curly brace level 1
				static int x = 0 ;   // available everywhere in this class
      
        public static void Main(string[] args)
        { // curly brace level 2
          
          	double yourNumber;	// available everywhere in this function
            string answer;      // available everywhere in this function

          	do 
            { // curly brace level 3
	            Console.Write("Please enter a number: ");
              // answer not declared here, but can be used here
            	answer = Console.ReadLine(); 
            } // end curly brace level 3
            while(double.TryParse(answer, out yourNumber));
              
            Console.WriteLine("Your number is: " + yourNumber);
            x = yourNumber; // x is global, so I can use it here
            foo();
        } // end curly brace level 2

        public static void foo()
        { // curly brace level 2
            // x is in curly brace level 1, so is good here
						Console.WriteLine("x = " + x);
        } // end curly brace level 2

    } // end curly brace level 1



```

#### Do NOT declare a local variable with the same name as a global variable.  It is possible, but it leads to mass confusion!

**Example of using same name for local and global variables**

```csharp
using System;

namespace ahha
{
    class MainClass
    {
        // global variable
        static int variable = 1234;

        public static void Main(string[] args)
        {
            int grapes = 3;
            int variable = 9; // *** BAD NAME BECAUSE GLOBAL EXISTS

            foo();

            // will show the local variable, NOT the global
            Console.WriteLine("In Main()");
            Console.WriteLine("variable is " + variable);
            Console.WriteLine("grapes is " + grapes);
        }

        public static void foo()
        {
            // I cannot access grapes that was defined in Main
            // because it was not defined
            // within my current squiggly brace set

            // however, I can create my own version of grapes
            int grapes = 15;

            // Since there is no local variable 'variable', look
            // for global 'variable'.  It exists, so use it.
            variable = variable + 25;

            Console.WriteLine("In Foo()");
            Console.WriteLine("variable is " + variable);
            Console.WriteLine("grapes is " + grapes);
        }
    }
}
```

*Results*

```text
In Foo()
variable is 1259
grapes is 15
In Main()
variable is 9
grapes is 3
```

## Class Exercise

Go through the code manually, and tell me what the output is

```csharp
using System;
using System.Diagnostics;

namespace ahha
{
    class Program
    {
        static int myglobal; // this is global 

        // don't screw around and name local variables  
        // the same as globals - don't ask for trouble! 

        static void Main(string[] args)
        {
            int a = 6;
            Console.WriteLine("in the main before function I see a equals " + a);
            myfunc();           // call the function 

            Console.WriteLine("in main after function I see a is "
                + a + " and global is " + myglobal);
            Console.WriteLine("Program Done Hit any key to continue");
            Console.ReadLine();
        }

        // make sure you create - open and close - your functions in the class!!!! 
        static void myfunc()
        {
            int a;
            myglobal = 99;  // notice how myglobal was declared at the class level 

            a = 300;
            a = a + 10;
            Console.WriteLine("In the function I see a as " + a);
        }
    }
}

```

# Magic Numbers and Constants

In your code it is not a good idea (or style) to hard code numbers into it. For example: 

```csharp
do 
{ 
// bla bla bla 
// more code 
} while (x < 4584);
```

Yes, the above is legit code but what's the deal? What is the number `4584`???

It seems 4584 is a "magic number" you've pulled out of thin air. Even if you comment it and explain it. Later you may have code like this: 

```csharp
for (j=0; j< 4584; j++) // what is this?? 
{ 
// more code 
} 
```

 We may see this in actual code: 

```csharp
static void Main(string[] args)
{
  // game to display 10 targets and have a maximum of 3 bullets
  // being fired in the game
  // partial pseudo code below...
  /*
  for (i = 0; i<10; i++)
  {
  	// code to move target number i
  	for (b = 0; b<3; b++) 
  	{
  		// check if target i hits bullet b, is so, call function
  		// to explode
  	}
  	
  	// now draw targets
  	for (w = 0;  w<10; w++)
  	{
  		// draw target w
  	}
  }
  */
  
  Console.ReadLine();
}
```

Okay but what if you boss tells you - I want 14 targets in this game. You say Okay no problem and you fix it below: 

```csharp
static void Main(string[] args)
{
  // game to display 10 targets and have a maximum of 3 bullets
  // being fired in the game
  // partial pseudo code below...
  /*
  for (i = 0; i<14; i++) //**** OK I FIXED IT *****
  {
  	// code to move target number i
  	for (b = 0; b<3; b++) 
  	{
  		// check if target i hits bullet b, is so, call function
  		// to explode
  	}
  	
  	// now draw targets
  	for (w = 0;  w<10; w++) // **** OH DEAR, FORGOT THIS ONE ****
  	{
  		// draw target w
  	}
  }
  */
  
  Console.ReadLine();
}
```

Look how easy it is to forget and/or miss one little detail!  What about all the departments who work with graphics and sound - I'm not the only one in the company. The entire company has to change their code from 10 to 14 and not miss one itty bitty detail. This is tedious. 

This is why we use constants. This is why "Quality Assurance" or "QA" may throw your code back at you and say fix it, follow our coding procedures. 

## How to use Constants: 

- `const` is a reserved word 
- look on google as to the exact syntax of using a constant 
- notice how a constant must be DEFINED as it is declared - there is no other way to do it. 

**This way won't work**

```csharp
const int upperlimit;
upperlimit = 100; // error here!
// you cannot assign a value to a constant
```

**Good and only way**

```csharp
const int upperlimit = 100;
// yes the only way to do it
// give it a value when you declare the constant
```

**Example**

```csharp
static void Main(string[] args)
{
  const int apples;
  const int numtargets = 14;
  
  apples = 3;  // THIS IS AN ERROR
  
  // game to display 10 targets and have a maximum of 3 bullets
  // being fired in the game
  // partial pseudo code below...
  /*
  // NO MORE HARDCODING '14' (or '10')
  for (i = 0; i<numtargets; i++) 
  {
  	// code to move target number i
  	for (b = 0; b<3; b++) 
  	{
  		// check if target i hits bullet b, is so, call function
  		// to explode
  	}
  	
  	// now draw targets
		// NO MORE HARDCODING '14' (or '10')
    	for (w = 0;  w<numtargess; w++) 
  	{
  		// draw target w
  	}
  }
  */
  
  Console.ReadLine();
}
```



### Other methods to declare constants or variables

Ever heard of an .ini file? Ever heard of a steam level editor file? ever heard of config the game file? Well this is simple - put all your constants at the top of your program. Declare/define them - and comment them. Then use throughout your program. Want to get fancy? Put all these into a text file. Have them "included" into your code (you will see this in Programming II). Allow the user to edit this text file through a web page. 

## Global Constants

"This is how you do it" - sorry for sounding like rap music….. 

* Global variables are declared outside of functions but within the class brackets. 

* They are visible, useable, changeable by every function within that class.  

```csharp
class Program
{
  const int enemies = 300; // global constant
  static int lives = 0;
  int energy = 100; // valid, but you don't know how to use it yet
  
  static void Main(string[] args)
  {
    // these are only visible in 'Main'
    const int numbtargets=14, numbullets =3 ;
  }
}
```

**Example**

We did not learn arrays yet, but here is another example below

```text
//ubisoft game code...
... bla bla bla ...
... bla bla bla ...
... bla bla bla > 27 ...
... bla bla bla ...
for (i=0; i<27; i++)
{
	... bla bla bla ...
}

int myarray[27];

while (z<27)
{
	... bla bla blaa
}
```

WTF is this 27??? It is a magic number pulled out of thin air!  Do not code with *magic numbers*.  What if Ubisioft says instead of 27 I want 30, and you only change half of the 27?  What if you made some 30, and forgot one or two and left them at 27?  Wil your code work??

Look how much nicer the code is with a constant.

You change it once at the top,and it 'ripples' throughout the code - no need to play search and replace games with an editor.

```text
//ubisoft game code...
const int numtargets = 27;
... bla bla bla ...
... bla bla bla ...
... bla bla bla > numtargets ...
... bla bla bla ...
for (i=0; i<numtargets; i++)
{
	... bla bla bla ...
}

int myarray[numtargets];

while (z<numtargets)
{
	... bla bla blaa
}
```

**Do not put any hard coded number into your code. The only acceptable ones to be found in code would be zero, one, and maybe two**

**Example**

```csharp
(while x>0) 
{ 
	// zero in code is okay - you don’t need a constant for that 
	// only use constants for weird numbers, like 27 
}
```

  

# Pretty Code

Below is a "pretty" way to organize your code. I recommend you do something similar to what I have below 

```csharp
using System;
using System.Diagnostics;

namespace ahha
{
    class Program
    {
        // this is the class
        // I can create global constants and variables here

        // ===========================
        // Global Constants Section
        // ===========================
        const int MAXSIZEOFSCREEN = 1024; // this is a constant
        const int MAXHEIGHT = 60;
        // bla bla bla more constants

        // ===========================
        // Global Variables Section
        // ===========================
        static int lives = 5;          // this variable will decrease as you get shot
        static int numEnemies = 60;    // you start with 60 targets and you shoot them
        // bla bla bla more variables

        // ===========================
        // Entry point to the program
        // ===========================
        static void Main(string[] args)
        {
            // In this function I can see/use/read/alter any of the global
            // variables.
            // I can only read, use (but not change) andy of the global constants
        }

        // ==========================
        // myfunc()
        // - description of myfunc()
        // ==========================
        static void myfunc()
        {
            // In this function I can see/use/read/alter any of the global
            // variables.
            // I can only read, use (but not change) andy of the global constants
        }

        // ==========================
        // yourFunc()
        // - description of yourfunc()
        // ==========================
        static void yourfunc()
        {

        }
    }
}

```

# Random Numbers

Consider this snippet - you figure out how to use random numbers. 

```csharp
 Random r = new Random(); 
 i = r.Next(1,100); 
```

 The above two lines of code generate a number between 1 and 100…. or is it 99…. uhmm…. I'm not sure… how can I be sure? 

*Answer*: Check Google and / or use the debugger. 

 For all the savvy people out there! how would I generate a random number between 52 and 57? 

Answer: Well I don't really know but I can use the above as a template

 ```csharp
  Random r = new Random(); 
  i = r.Next(52,57); 
 // based on above example - I can say this will yield a number between 52 and 56 
 ```

Copying the pattern is not really learning. But it does work… 

 ## Explanation of the Code

What is really going on - you will learn/understand more of this as you take Programming II and Programming III .  You will not be tested on this material.

```csharp
 Random r = new Random(); 
 i = r.Next(1,100); 
```

`Random` is the name of a class

`Random r` says, let us define variable `r` to be an object of type `Random`

`Random()` is a function (method) that creates the object

`Random r = new Random()` creates a new Random object and saves it in the variable `r`

`r.Next(1,100)` call method `Next` with the parameters `1` and `100` on the object `r`.

 ## Challenge

Simulate the roll of two die (a pair of dice). 

Each die goes from 1 to 6 

Roll the dice 1000 times and show me how many times your 'rolled' 2, 3, 4, ... 12.

# String Input and Compare

```csharp
   string myStr; 
   myStr="Jane";  // you can, but the ReadLine, even if blank will over ride this value 
   
	Console.WriteLine("Who are you?"); 
   myStr = Console.ReadLine(); 

   if (myStr == "Ted")  // Case must match exactly 
   { 
	     Console.WriteLine ("Yahoo it is TED!!!!"); // if it is ted you say yahoo! 
   } 

   Console.WriteLine("Hello there "+myStr); 

```

 Consider the above - the person types in their name and we want to see if it is Ted. 

### Question

* Did the user type upper case, or lower case?

* Will it work if I typed Ted? or tEd? or some crazy combination? 
* Your job - test this to tell me if casing is an issue. 

 How do I tell, how do I know? Answer: You can surf, or rip it apart with the debugger! 

So, lets use the debugger:

#### Use the VS Debugger to answer the question

![screenshot of VS Debugger](../Images/22_Debug_compare_strings.png)

Open the `immediate window` via Debug->Windows. The immediate window allows you to inspect variables, and expressions

* To see the value of a variable, you simply type the variable name, or expression

Type the following

```code
myStr
myStr == "Ted"
myStr = "Ted"
myStr == "ted"
myStr.ToUpper()
myStr.ToLower()
```

*Expected results shown in `Immediate Window`*

```dos
myStr
"ted"
myStr == "Ted"
false
myStr = "Ted"
"Ted"
myStr == "Ted"
true
myStr.ToUpper()
"TED"
myStr.ToLower()
```

 I proved that 

*`ted` is not the same as `Ted`*

#### Use the command line debugger to answer the question

The command line debugger does *not* allow you to test code like the `intermediate` window in VS Debugger, but you can 

* See the value of the variables, `print `*` variable_name`*
* Set variables to specific values

* Set the next line to be executed `setip = `*` line number`*

Since line 19 corresponds to the statement: ` if (myStr == "Ted")`, we can keeping testing the `if` condition over and over again. If the code enters the `if block` then the condition is true, otherwise it is false

Run `mdbg` and enter the following commands

```
mdbg string_compare.exe
path .
symbol path .
set myStr="ted"
setip 19
next
set myStr="TED"
setip 19
next
set myStr="Ted"
setip 19
next
next
exit

```

*Expected Output*

```text
[p#:0, t#:0] mdbg> path .
[p#:0, t#:0] mdbg> symbol path .
Current symbol path: .
[p#:0, t#:0] mdbg> set myStr="ted"
myStr="ted"
[p#:0, t#:0] mdbg> setip 19
STOP EvalComplete
19:            if (myStr == "Ted") // Case must match exactly
[p#:0, t#:0] mdbg> n
25:            Console.WriteLine("thanks");
[p#:0, t#:0] mdbg> set myStr="TED"
myStr="TED"
[p#:0, t#:0] mdbg> setip 19
STOP EvalComplete
19:            if (myStr == "Ted") // Case must match exactly
[p#:0, t#:0] mdbg> n
25:            Console.WriteLine("thanks");
[p#:0, t#:0] mdbg> set myStr="Ted"
myStr="Ted"
[p#:0, t#:0] mdbg> setip 19
STOP EvalComplete
19:            if (myStr == "Ted") // Case must match exactly
[p#:0, t#:0] mdbg> n
20:            {
[p#:0, t#:0] mdbg> n
21:                Console.WriteLine("********************hhhhhheeeee haaaaa!!!!! It is Ted !!!!!");
[p#:0, t#:0] mdbg> exit
Terminating current process...

```



## How to properly compare strings

I can convert the user input to lower case and compare it to `ted` OR I can convert the user input to upper case and compare it to `TED`. Your choice. 

I can convert the user input to lower case and compare it to `ted` OR I can convert the user input to upper case and compare it to `TED`. Your choice. 

Aha! Now I can redo line 19 to look like this: 

```csharp
if (myStr.ToUpper() == "TED") // Now it works with any case!
```

Now I am bullet proof! 

I could also do this:

```csharp
if (myStr.ToLower() == "ted")
```

 

Note that:

```csharp
if (myStr.ToLower == "tEd")
```

is an error - because the above will never ever be true - I'm converting the user input to lower case and I'm comparing it to something with an upper case "E" in it. This can never be true. 

