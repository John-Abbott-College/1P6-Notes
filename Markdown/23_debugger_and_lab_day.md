# Debugger

We have played with the debugger a bit, but today we are going to go over it again.

## Setup

Create some code with at least one function, and some global variables.

Not sure what to do?  Then use the code below.

```csharp
using System;

namespace testing
{
    class MainClass
    {
        // Global constants
        const int RETIREMENT_AGE = 65;
        static int global_var;

        // main
        public static void Main(string[] args)
        {
            // local vars
            string answer;

            // code
            bar();
            do
            {
                Console.Write("Do you want to continue? ");
                answer = Console.ReadLine();
                global_var = global_var + 1;
                foo();

            } while (answer.ToLower().StartsWith("y"));
        }

        static void foo()
        {
            // local vars
            string answer;

            // code
            bar();
            Console.WriteLine("global_var = " + global_var);
            Console.Write("What is your name? ");
            answer = Console.ReadLine();
            Console.WriteLine("Hello " + answer);
        }

        static void bar()
        {
            // no local vars
            // code
            Console.WriteLine(" You are in Bar");
         }
 
    }
}

```

### Compile

#### Visual Studio

Make sure that your solution configuration is set to `Debug` (not `Release`). This drop down is located in the top bar of the application

`Build`

#### Mdgb (command line)

`csc /debug+ /d:DEBUG;TRACE `*`   program.cs`*

## Setting Breakpoints

### Visual Studio 

* Click in the far left column next to the line where you want to set a breakpoint (it must be an executable line)
* Select a line.  To toggle a breakpoint, `F9` (PC), `cmd+\` (Mac)
* Conditional breakpoints
  * Windows: right click a break point, and select "conditions..."
  * Mac: select a line. Using the menu, `Run` -> `New Breakpoint ...`

### Mdbg (command line)

* I cannot figure out how to set breakpoints, but the debugger will automatically stop at the first executable line

### In the code directly

```csharp
using System.Diagnostics;

// ... code ...

Debugger.break();
```



## Navigate your code (VS and Mdgb)

* `next` or **`step over`** 
  * Navigates to the next line of code
  * If the current line of code is a function, it will execute that function without stopping (unless you have set a breakpoint in that function)
* `step` or **`step into`**
  * Navigates to the next line of code
  * If the current line of code is a function, it will stop at the first executable line within the function being called
* `out` or **`step out`** 
  * If you are in a function, 
    * will finish executing the function without stopping (unless you have a breakpoint), and returns to the line of code that called this function
* `go` or **`continue`**
  * Program will continue as normal, until it reaches a breakpoint, or the end of execution.
* `setip`*` line_number`*  (Mdbg only)
  * Set the current line to execute to *`line_number`*.  
    * Note, this is not the same as a breakpoint, because none of the code, from where you currently are, to where you want to be, will be executed

## Where are you? (Stack Trace)

What is the call stack?

Everytime you call a function, the executable needs to keep track of 

* which line you were on before you called the function
* what function and line are you currently on

**Example**

For line 46 in our sample program, did we get there from line 18, or from line 35?

Let's inspect the call stack:

```text
testing.MainClass.bar() in Program.cs:46
testing.MainClass.foo() in Program.cs:35
testing.MainClass.Main(string[] args) in Program.cs:24
```

Line 1: Tells us where we currently are (line 46, in function `bar`)

Line 2: Tells us that `bar` was called from `foo` at line 35

Line 3: Tells us that `foo` was called from `Main` at line 24



### Visual Studio

* Open the stack trace window
  * PC: `Debug`->`Windows`->`Call Stack`
  * MAC: `View`->`Debug Windows`->`Call Stack`

### Mdbg

* `where`



## Setting and Inspecting Variables

### Visual Studio 

* Run the debugger

* If you do not see the `immediate` window, open it.
  * Mac: View -> Debug Windows -> Immediate
  * PC: Debug -> Windows -> Immediate
  
* To see the contents of a local variable, simply type the variable name

* To set the contents of a local variable (*` variable `*`=`*`value`* )

* To see the result of an expression, simply type the expression

  `global_var > 10`

  `global_var + 10`

  Note that the above does not change the value of `global_var`

### Command Line (Mdbg)

* Set the source path to the path where your source code is

* Set the symbol path to where the .dbf file is

* Run your executable

* use `print` to see all local variables and their values
	* use `print`*` variable`* to see content of specific local variable
* use `set`*` variable `*`=`*`value`*  to set a variable to a specific value





