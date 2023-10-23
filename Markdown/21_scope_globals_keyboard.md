# Scope, Globals & Keyboard tips

## Keyboard Tips: Auto format (indent)
Make sure to **constantly** use automatic code formatting:

**Default hotkeys** for Visual Studio (Windows):

- **Ctrl+E, Ctrl+D** to format the entire document.
- **Ctrl+E, Ctrl+F** to format the selection (whatever is highlighted).

**Some versions** of Visual Studio (Windows):

- **Ctrl + K, D**  to format entire document.
- **Ctrl + K, F** to format the selection (whatever is highlighted).

**To find out which key bindings apply in _your_ copy of Visual Studio**:
In menu _Edit_ → _Advanced menu_ - the keys are displayed to the right of the menu items, so it's easy to discover what they are on your system.

**Customize the keyboard shortcuts** in menu _Tools_ → _Options_ → _Environment_ → _Keyboard_ (either by selecting a different "keyboard mapping scheme", or binding individual keys to the commands "Edit.FormatDocument" and "Edit.FormatSelection").

## Scope

Variable and function scope is an important concept that applies to most C-based languages.

> Scoping is used to avoid variable and function names defined in one location of your code from being confused with another variable or function defined in another isolated location.

### Basic Scoping Rules

There are the basic scoping rules:

1. Variables *belong* in the scope of the code block (curly braces) where they are declared.

```csharp
{
	string myVariable = "String variable";  // available anywhere inside these curlies
}
```

2. Variables are available to anything within their code block (curly braces), even embedded (child) code blocks.
	- Alternative way to interpret this rule: when a variable is called, if it was not declared in the current scope, the compiler is allowed to look for it in an ancestor scope (ei. parent, grand-parent, great-grand-parent, etc.).

```csharp
{
	string myVariable = "String variable";

	while(true)
	{
		Console.Write(myVariable);  // myVariable is available in this child scope
	}
}
```

3. Once the code block is closed (a close curly brace), all the variables declared within that code block will be "erased from memory", as if they never existed.

```csharp
{
	string myVariable = "String variable";
}
Console.Write(myVariable);  // myVariable never existed here 😢
```


### Local vs Global Variables

Variables that are available anywhere in your `Main` program are called **global variables**.
When a variable is declared within a function, they are called **local variables**. 
If a variable is declared within a loop (`while`, `for`, `do-while`, etc), they are called **temporary variables**.

Consider the basic program structure that we've been using:

```csharp
namespace ConsoleApp
{  // top level scope
    internal class Program
    {  // class scope
        static void Main(string[] args)
        {  // main function scope
	        string myVariable = "String variable";
        }
    
		static void CustomGreeting()
		{  // custom function scope
		
		}
    }
}
```

Each pair of curly braces defines a new scope.

With the exception of the `namespace ConsoleApp` scope, all other scopes belonged to a parent scope where they were declared.

- `class Program` is a child of the `namespace ConsoleApp` scope.
- `Main function` is a child of the `class Program` scope.
- Variable `string myVariable` is a child of the `Main function` scope.
- Function `CustomGreeting` is a child of the `class Program` scope.

![embedded russian dolls animation](https://media.tenor.com/jY8sdNxWUhIAAAAC/matrioska-loop.gif ":size=500")
*Source: [tenor.com](https://tenor.com/view/matrioska-loop-bored-tired-russian-gif-7433508)*


> Using the basic scoping rules, where would you declare a variable so that it is available in the following locations:
> 
> - Inside your `Main` function, and
> - Inside any custom function you might declare?


#### Defining Global Variables

To define global variables, you declare them in the `class Program`'s scope and must specify `static` in **front of the variable name**.

> ⚠ Your variable can now be accessed **and modified** from any function, loop, or `if` statement inside your program.

> **Avoid** using global variables, they make your code more complicated to understand and debug.


```csharp
namespace ConsoleApp
{  // top level scope
    internal class Program
    {  // class scope

		static string myVariable = "String variable";  // global variable

        static void Main(string[] args)
        {  // main function scope

        }
    
		static void CustomGreeting()
		{  // custom function scope
		
		}
    }
}
```


#### Example 1: Annotated Scope Levels

Below is a simple example where 3 variables are declared and accessed in different scope levels.
The beginning and end of each scope is described in comments.

```csharp
    class MainClass
    {	// scope level 1
		static int x = 0 ;   // available everywhere in this class
      
        public static void Main(string[] args)
        { // scope level 2
          
          	double yourNumber;	// available everywhere in this function
            string answer;      // available everywhere in this function
 
          	do 
            {   // scope level 3
	            Console.Write("Please enter a number: ");
                // answer not declared here, but can be used here
            	answer = Console.ReadLine(); 
            }   // end of scope level 3
            while(!IsNumber(answer));

            yourNumber = Convert.ToDouble(answer);
            Console.WriteLine("Your number is: " + yourNumber);
            x = yourNumber; // x is global, so it can be used here
            foo();
        } // end scope level 2

        public static void foo()
        { // scope level 2
            // x is declared in scope level 1, so it's accessible here
			Console.WriteLine("x = " + x);
        } // end scope level 2

    } // end scope level 1
```

### Avoid Naming Collisions

> **Do not** declare a local variable with the same name as a global variable.
> It is possible, but can easily lead to confusion.

#### Example 2: Same name for local and global variables

```csharp
using System;

namespace example
{
    class MainClass
    {
        // global variable
        static int myNumber = 1234;

        public static void Main(string[] args)
        {
            int grapes = 3;
            int myNumber = 9; //  BAD NAME BECAUSE GLOBAL EXISTS

            foo();

            // will show the local variable, NOT the global
            Console.WriteLine("In Main()");
            Console.WriteLine("myNumber is " + myNumber);
            Console.WriteLine("grapes is " + grapes);
        }

        public static void foo()
        {
            // It cannot access grapes that was defined in Main,
            // however, it can create a new variable with same name.
            int grapes = 15;

            // Since there is no local variable 'myNumber', look
            // for global 'myNumber'. If it exists, it will be used.
            myNumber = myNumber + 25;

            Console.WriteLine("In Foo()");
            Console.WriteLine("variable is " + myNumber);
            Console.WriteLine("grapes is " + grapes);
        }
    }
}
```

*Output*

```text
In Foo()
myNumber is 1259
grapes is 15
In Main()
myNumber is 9
grapes is 3
```

## Global Constants

Similarly to how we declared global variables, we can also declare **global constants** using the following rules:

1. Global variables are declared within `class Program` scope and outside of functions.
2. Include the keyword `const` in front of the variable declaration.
3. Do not include the keyword `static`. Global variables of type `const` are made static by default.

```csharp
using System;

namespace RandomExample
{
    class Program
    {
        const int MIN = 10;    // lowest random value to be generated (included)
        const int MAX = 50;    // highest random value to be generated (not included)

        static int repeats;
        static void Main(string[] args)
        {
            Console.WriteLine("How many random number to generate?");
            repeats = Convert.ToInt32( Console.ReadLine() );
            Console.WriteLine($"Printing {repeats} random numbers between {MIN} and {MAX}.");
            PrintRandomNumbers();
        }

        static int GetRandomInt()
        {
            Random randomizer = new Random();    // create an object of type Random
            int randomInt = randomizer.Next(MIN, MAX);   // generates a random int between min and max
            return randomInt;
        }

        static void PrintRandomNumbers()
        {
            for(int i = 0; i < repeats; i++)
            {
                int randomNumber = GetRandomInt();
                Console.WriteLine( randomNumber );
            }
        }

    }
}
```

*Output*

```text
How many random number to generate?
5
Printing 5 random numbers between 10 and 50.
22
19
43
37
31
```


## Pretty Code

Below is a "pretty" way to organize your code with sections for global constants and variables as well as sections for functions.

For larger code projects (ex. assignment 3 or your final project), you are strongly encouraged to do something similar.

```csharp
using System;

namespace pretty
{
    class Program
    {
        // this is the class
        // Create global constants and variables here

        // ===========================
        // Global Constants Section
        // ===========================
        const int MAXSIZEOFSCREEN = 1024; // this is a constant
        const int MAXHEIGHT = 60;

        // ===========================
        // Global Variables Section
        // ===========================
        static int lives = 5;          // this variable will decrease as you get hit
        static int numEnemies = 60;    // start with 60 enemy targets

        // ===========================
        // Entry point to the program
        // ===========================
        static void Main(string[] args)
        {
            
        }

        // ==========================
        // MyFunc()
        // - description of what MyFunc does
        // ==========================
        static void MyFunc()
        {
            
        }

        // ==========================
        // YourFunc()
        // - description of what YourFunc does
        // ==========================
        static void YourFunc()
        {

        }
    }
}
```


## Exercises

Trace the code below and write down what the outputted text will be.

```csharp
using System;

namespace exercise
{
    class Program
    {
        static int myGlobal; // this is global 

        // don't mess around and name local variables  
        // the same as globals - don't ask for trouble! 

        static void Main(string[] args)
        {
            int a = 6;
            Console.WriteLine("In main, before MyFunc, I see 'a' as " + a);
	        MyFunc();           // call the function 

            Console.WriteLine("In main, after MyFunc, I see 'a' as "
                + a + " and myGlobal is " + myGlobal);
            Console.WriteLine("Program Done");
            Console.ReadLine();
        }

        // make sure you create - open and close - your functions in the class! 
        static void MyFunc()
        {
            int a;
            myGlobal = 99;  // notice how myGlobal was declared at the class level 

            a = 10;
            a = a + 20;
            Console.WriteLine("In MyFunc I see 'a' as " + a);
        }
    }
}
```

*Output*

```text
In main, before MyFunc, I see 'a' as __  
In MyFunc I see 'a' as __  
In main, after MyFunc, I see 'a' as __ and myGlobal is __
Program Done
```
