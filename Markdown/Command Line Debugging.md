



# Command Line Debugging

Before you begin, you need to know how to create an executable that is compatible with debugging.

 ### Compiling for debug mode

```dos
csc /debug+ /d:DEBUG;TRACE mysource_code.cs
```

 ### Compiling for release mode

```dos
csc /debug- /optimize+ /d:RELEASE mysource_code.cs
```



## Using print statements

### the `MyDebug` class

Use the `System.Diagnostics` library

```csharp
using System.Diagnostics;
```

Include the following class in your code.

```csharp
// ========================================================================
// debug class for debugging via print statements
// ========================================================================
// NOTE: does nothing if your code is compiled in RELEASE mode.
//
// NOTE: to compile in debug mode
//    csc /debug+ /d:TRACE;DEBUG
//
// NOTE: to compile in release mode
//    csc /debug- d:/RELEASE /optimize+
// -----------------------------------------------------------------------
// Constructor:  var debug = debug()
//
// Methods:
// output (msg, conditional, pause, stacktrace)
// -----------------------------------------------------------------------
public class MyDebug
{
    // ===================================================================
    // Constructor for MyDebug... sets up a listener, where things will
    // be printed to the console
    // ===================================================================
    public MyDebug()
    {
        Debug.Listeners.Add(new TextWriterTraceListener(Console.Out));
        Debug.AutoFlush = true;
    }

    // ===================================================================
    // methods: output(msg, conditional, pause, stacktrace)
    //    msg - message to print
    //    conditional - only prints if this is true (default true)
    //    pause - if true, wait for user to press a key on the keyboard before
               continuing (default false)
    //    stacktrace - if true, print the stacktrace (default false)
    // ===================================================================
   public void output(
			string msg, 
			bool conditional = true, 
			bool pause = false, 
			bool stacktrace = false)
   {
        if (conditional)
        {
				    Debug.Indent();
            Debug.WriteLine("");
            Debug.WriteLine("DEBUG INFO: " + msg);
            if (stacktrace)
            {
                Debug.Indent();
                Debug.WriteLine(Environment.StackTrace);
                Debug.Unindent();
            }
            if (pause)
            {
                Debug.WriteLine("");
                Debug.WriteLine("DEBUG: Press any key to continue");
# if DEBUG
                Console.ReadKey();
# endif
            }
            Debug.WriteLine("");
		    		Debug.Unindent();

        }
    }
}
```

### using `MyDebug` class

#### create a `MyDebug` class

```csharp
MyDebug debug = new MyDebug();
```

#### printing stuff out

> NOTE: Nothing will be printed *unless* you have compiled your code in debug mode.  

To just print stuff to the console

```csharp
debug.output("x = " + x);
```

To print stuff out, and the stack trace

```csharp
debug.output("x = " + x, stacktrace:true);
```

To print stuff out, and wait before continuing?

```csharp 
debug.output("x = " + x, stacktrace:true, pause:true);
debug.output("x - " + x, pause:true);
```

To print stuff out, based on a given condition

```csharp
debug.output("x = " + x, conditional: x < 10 );
```


### Example

#### Code

```csharp
using System;
using System.Diagnostics;

namespace ahha
{

    // ========================================================================
    // This is our main class.  All of our functions will be in this class
    // ========================================================================
    class MainClass
    {
        // global variables (available in every function in this class)

        // ********* MUST DO THIS IF YOU WANT TO USE THE debug CLASS
        static MyDebug debug = new MyDebug();


        // ========================================================================
        // This is our main program.  It doesn't do much
        // ========================================================================
        public static void Main(string[] args)
        {
            double yourNumber;
            Console.Write("Please enter a number: ");
			
            string answer = Console.ReadLine();
            debug.output("User entered : " + answer);

            double.TryParse(answer, out yourNumber);
            debug.output("yourNumber = " + yourNumber);

            // conditional debug
            debug.output("You entered a large number", 
                         conditional: yourNumber > 100, pause:true);


            Console.WriteLine("Your number is: " + yourNumber);
            foo();
        }

        // ========================================================================
        // This is just a function that does not do much either
        // ========================================================================
        public static void foo()
        {
            debug.output(msg: "Starting foo", stacktrace: true, pause: true);
            Console.WriteLine("hello foo");
            debug.output(msg: "foo is finished", pause: true);
        }

    }

    // ========================================================================
    // debug class for debugging via print statements
    // ========================================================================
    // NOTE: does nothing if your code is compiled in RELEASE mode.
    //
    // NOTE: to compile in debug mode
    //    csc /debug+ /d:TRACE;DEBUG
    //
    // NOTE: to compile in release mode
    //    csc /debug- d:/RELEASE /optimize+
    // -----------------------------------------------------------------------
    // Constructor:  var debug = debug()
    //
    // Methods:
    // output (msg, conditional, pause, stacktrace)
    // -----------------------------------------------------------------------
    public class MyDebug
    {
        // ===================================================================
        // Constructor for MyDebug... sets up a listener, where things will
        // be printed to the console
        // ===================================================================
        public MyDebug()
        {
            Debug.Listeners.Add(new TextWriterTraceListener(Console.Out));
            Debug.AutoFlush = true;
        }

        // ===================================================================
        // methods: output(msg, conditional, pause, stacktrace)
        //    msg - message to print
        //    conditional - only prints if this is true (default true)
        //    pause - if true, wait for user to press a key on the keyboard before
        //           continuing (default false)
        //    stacktrace - if true, print the stacktrace (default false)
        // ===================================================================
        public void output(
				string msg, 
				bool conditional = true, 
				bool pause = false, 
				bool stacktrace = false)
        {
            if (conditional)
            {
								Debug.Indent();
                Debug.WriteLine("");
                Debug.WriteLine("DEBUG INFO: " + msg);
                if (stacktrace)
                {
                    Debug.Indent();
                    Debug.WriteLine(Environment.StackTrace);
                    Debug.Unindent();
                }
                if (pause)
                {
                    Debug.WriteLine("");
                    Debug.WriteLine("DEBUG: Press any key to continue");
# if DEBUG
                    Console.ReadKey();
# endif
                }
                Debug.WriteLine("");
								Debug.Unindent();

            }
        }
    }

}

```

#### Compiling and Running

##### Debug Mode

```text
> csc /debug+ /d:DEBUG;TRACE debug_example.cs
Microsoft (R) Visual C# Compiler version 3.7.0-6.20375.2 (34202cc2)
Copyright (C) Microsoft Corporation. All rights reserved.


> debug_example.exe
Please enter a number: 250

    DEBUG INFO: User entered : 250


    DEBUG INFO: yourNumber = 250


    DEBUG INFO: You entered a large number

    DEBUG: Press any key to continue

Your number is: 250

    DEBUG INFO: Starting foo
   at System.Environment.GetStackTrace(Exception e, Boolean needFileInfo)
   at System.Environment.get_StackTrace()
   at ahha.MyDebug.output(String msg, Boolean conditional, 
   									Boolean pause, Boolean stacktrace) in debug_example.cs:line 102
   at ahha.MainClass.foo() in debug_example.cs:line 45
   at ahha.MainClass.Main(String[] args) in debug_example.cs:line 37

    DEBUG: Press any key to continue

hello foo

    DEBUG INFO: foo is finished

    DEBUG: Press any key to continue


c:\Users\compsci\JAC\JAC\1P6\1P6\code>

```

## Using a command line debugger

[Microsoft documentation](https://docs.microsoft.com/en-us/dotnet/framework/tools/mdbg-exe)

### Install Mdbg.exe onto your machine

#### The hard way

Create a project in Visual Studio.

Using a `cmd` window, navigate to the directory where the `.csproj` file is located for your project.

Type the following in the `cmd` window

```dos
dotnet add package MDbg 
```

Now you have to find the path where `Mdbg` was installed.  I found mine in my user directory `C:\Users\compsci`, in the subfolder ```.nuget\packages\mdbg\0.1.0\tools```

#### The easy way

Download `CLIDebugger.zip` from LEA, and extract the contents someplace where you can find it easily.

#### Setting up the path

In your user directory (again, mine is `\Users\compsci`, but find your own!), create a directory called `MyTools`

Navigate to your user directory (yours, not mine!)

```dos
cd \Users\compsci
mkdir MyTools
```

Permanently add this directory to your `PATH` environment variable (again be careful to use your OWN username, not mine!)

```dos
SET Key="HKCU\Environment" 
FOR /F "usebackq tokens=2*" %A IN (`REG QUERY %Key% /v PATH`) DO Set CurrPath=%B

SETX PATH "%CurrPath%;C:\Users\compsci\MyTools"

```

#### Copy `mdbg` to `MyTools`

Navigate to your `MyTools` directory and copy all the files that came with `mdgb` to this directory

```dos
cd MyTools
copy c:\Users\compsci\.nuget\packages\mdbg\0.1.0\tools\*.* .
```

*Expected result*

```text
c:\Users\compsci>cd MyTools

c:\Users\compsci\MyTools>copy c:\Users\compsci\.nuget\packages\mdbg\0.1.0\tools\*.* .
c:\Users\compsci\.nuget\packages\mdbg\0.1.0\tools\CorApi.dll
c:\Users\compsci\.nuget\packages\mdbg\0.1.0\tools\CorApiRaw.dll
c:\Users\compsci\.nuget\packages\mdbg\0.1.0\tools\Mdbg.exe
c:\Users\compsci\.nuget\packages\mdbg\0.1.0\tools\Mdbg.pdb
c:\Users\compsci\.nuget\packages\mdbg\0.1.0\tools\MDbgEng.dll
c:\Users\compsci\.nuget\packages\mdbg\0.1.0\tools\MDbgExt.dll
c:\Users\compsci\.nuget\packages\mdbg\0.1.0\tools\MdbgUtility.dll
c:\Users\compsci\.nuget\packages\mdbg\0.1.0\tools\NativeDebugWrappers.dll
        8 file(s) copied.

c:\Users\compsci\MyTools>
```

#### Tidy up

Close the `cmd` window and open a new `cmd` window.

Test

```dos
mdbg
```

*Expected Result*

```text
C:\Users\compsci>mdbg
MDbg (Managed debugger) v0.0.0.0 started.
Copyright (C) Microsoft Corporation. All rights reserved.

For information about commands type "help";
to exit program type "quit".

mdbg> quit

C:\Users\compsci>

```

### How to use `Mdgb`

#### Compile the sample code below in debug mode

Save the file in `debug_example.cs`

```csharp
using System;

namespace ahha
{

    // ========================================================================
    // This is our main class.  All of our functions will be in this class
    // ========================================================================
    class MainClass
    {
        // global variables (available in every function in this class)


        // ========================================================================
        // This is our main program.  It doesn't do much
        // ========================================================================
        public static void Main(string[] args)
        {
            int x = 33;
						double yourNumber;
            Console.Write("Please enter a number: ");
			
            string answer = Console.ReadLine();
            double.TryParse(answer, out yourNumber);
            Console.WriteLine("Your number is: " + yourNumber);

            // call some silly function
						foo();
			
						yourNumber = x * 33;
			
						Console.WriteLine("Good bye!");
			
        }

        // ========================================================================
        // This is just a function that does not do much either
        // ========================================================================
        public static void foo()
        {
						int j = 21;
						int i = 56;
            Console.WriteLine("hello foo");
						i = i * j;
						j = i * j;
						Console.WriteLine("all done!");
        }
    }
}

```



Compile:

```dos
csc /debug+ /d:DEBUG;TRACE debug_example.cs
```

*Expected Result*

```dos
C:\Users\compsci\JAC\JAC\1P6\1P6\code>csc /debug+ /d:DEBUG;TRACE debug_example.cs
Microsoft (R) Visual C# Compiler version 3.7.0-6.20375.2 (34202cc2)
Copyright (C) Microsoft Corporation. All rights reserved.

```

Verify that you have an executable (`debug_example.exe`, and you have the debugging information `debug_example.dbg`)

```dos
dir
```

*Expected Result*

```text
C:\Users\compsci\JAC\JAC\1P6\1P6\code>dir
 Volume in drive C is Windows
 Volume Serial Number is AC7E-33AA

 Directory of C:\Users\compsci\JAC\JAC\1P6\1P6\code

10/16/2021  02:06 PM    <DIR>          .
10/16/2021  02:06 PM    <DIR>          ..
10/16/2021  05:40 PM             1,535 debug_example.cs
10/16/2021  05:40 PM             4,608 debug_example.exe
10/16/2021  05:40 PM            11,776 debug_example.pdb
               3 File(s)         17,919 bytes
               2 Dir(s)  279,354,396,672 bytes free

C:\Users\compsci\JAC\JAC\1P6\1P6\code>

```

#### Running `Mdbg` and setting the appropriate paths

Start `Mdgb`

```dos
Mdgb
```

*Expected Result*

```dos
C:\Users\compsci\JAC\JAC\1P6\1P6\code>Mdbg
MDbg (Managed debugger) v0.0.0.0 started.
Copyright (C) Microsoft Corporation. All rights reserved.

For information about commands type "help";
to exit program type "quit".

mdbg>

```

Define the path where to find the source code

```dos
path .
```

*Expected Result*

```text
mdbg> path .
Path set to: .
mdbg>

```

Define the path where to find the symbol files (the `pdb` file that was produced when you compiled your code)

```dos
symbol path .
```

*Expected Result*

```text
mdbg> symbol path .
Current symbol path: .
mdbg>
```

#### Debugging your code

Run the executable that you wish to run (remember that it needs to be compiled in debug mode for this to work)

```mdgb
run debug_example.exe
```

*Expected Result*

```text
mdbg> run debug_example.exe
STOP: Breakpoint Hit
18:        {
[p#:0, t#:0] mdbg>

```

To see where you are in the code, use the `show` command.  The line that will be executed next will be preceded by an astericks (`*`)

```mdbg
show
```

*Expected Results*

```text
[p#:0, t#:0] mdbg> show
15          // This is our main program.  It doesn't do much
16          // ========================================================================
17          public static void Main(string[] args)
18:*        {
19              int x = 33;
20                      double yourNumber;
[p#:0, t#:0] mdbg>

```

> Note: the reason the code is not properly indented is because my code has a mix of tabs and spaces.  Don't use tabs in your source code.

#### Navigating your code

To proceed to the next line of code, you have the following options

* `next`:  step over (if the line of code to be executed is a function, that function will be executed without pausing)
* `step`: step into (if the line of code to be executed is a function, the debugger will pause at the first line of code in the function)
* `out`: step out (if you are currently executing with a function, the debugger will finish process the function without pausing, and pause only once the function has returned)
* `go`: continue until the next breakpoint, or your program exits.

Notice that with every step, the line number and the code for the next line to be executed is displayed.

You forgot where you are... how did you get there, etc.  To see the stack trace

```mdgb 
where
```

*Example Output*

```text
[p#:0, t#:0] mdbg> s
43:                     int j = 21;
[p#:0, t#:0] mdbg> where
Thread [#:0]
*0. ahha.MainClass.foo (C:\Users\compsci\JAC\JAC\1P6\1P6\code\debug_example.cs:43)
 1. ahha.MainClass.Main (C:\Users\compsci\JAC\JAC\1P6\1P6\code\debug_example.cs:30)
[p#:0, t#:0] mdbg>

```



**Example**

Pay close attention to the code, and whether `n`, `s` or `o` was used.  You might want to go back'n'forth between this window and your editor with the code in it.

```text
[p#:0, t#:0] mdbg> show
15          // This is our main program.  It doesn't do much
16          // ========================================================================
17          public static void Main(string[] args)
18:*        {
19              int x = 33;
20                      double yourNumber;
[p#:0, t#:0] mdbg> n
19:            int x = 33;
[p#:0, t#:0] mdbg> n
21:            Console.Write("Please enter a number: ");
[p#:0, t#:0] mdbg> n
Please enter a number: 23:            string answer = Console.ReadLine();
[p#:0, t#:0] mdbg> n
33
24:            double.TryParse(answer, out yourNumber);
[p#:0, t#:0] mdbg> n
25:            Console.WriteLine("Your number is: " + yourNumber);
[p#:0, t#:0] mdbg> n
Your number is: 33
28:                     foo();
[p#:0, t#:0] mdbg> s
40:        {
[p#:0, t#:0] mdbg> show
37          // This is just a function that does not do much either
38          // ========================================================================
39          public static void foo()
40:*        {
41                      int j = 21;
42                      int i = 56;
[p#:0, t#:0] mdbg> n
41:                     int j = 21;
[p#:0, t#:0] mdbg> n
42:                     int i = 56;
[p#:0, t#:0] mdbg> show
39          public static void foo()
40          {
41                      int j = 21;
42:*                    int i = 56;
43              Console.WriteLine("hello foo");
44                      i = i * j;
[p#:0, t#:0] mdbg> o
hello foo
all done!
28:                     foo();
[p#:0, t#:0] mdbg> show
25              Console.WriteLine("Your number is: " + yourNumber);
26
27              // call some silly function
28:*                    foo();
29
30                      yourNumber = x * 33;
[p#:0, t#:0] mdbg> n
30:                     yourNumber = x * 33;
[p#:0, t#:0] mdbg> n
32:                     Console.WriteLine("Good bye!");
[p#:0, t#:0] mdbg> n
Good bye!
34:        }
[p#:0, t#:0] mdbg> n
STOP: Process Exited
mdbg>

```

#### Viewing local variables

To see the value of all local variables,

```mdgb
print
```

*Sample output*

```text
mdbg> run debug_example.exe
STOP: Breakpoint Hit
18:        {
[p#:1, t#:0] mdbg> print
x=0
yourNumber=0
answer=<null>
args=array [0]
[p#:1, t#:0] mdbg> n
19:            int x = 33;
[p#:1, t#:0] mdbg> n
21:            Console.Write("Please enter a number: ");
[p#:1, t#:0] mdbg> print
x=33
yourNumber=0
answer=<null>
args=array [0]
[p#:1, t#:0] mdbg>

```

To see the value of a specific variable

`print `*`variable_name`*

*sample output*

```
[p#:1, t#:0] mdbg> print x
x=33
[p#:1, t#:0] mdbg> print not_a_variable
Error: Variable not found
[p#:1, t#:0] mdbg>

```

#### Setting Local Variables

`set `*`variable_name`*`=`*`new value`*

*sample output*

```text
[p#:2, t#:0] mdbg> print x
x=33
[p#:2, t#:0] mdbg> set x=55
x=55
[p#:2, t#:0] mdbg> print x
x=55
[p#:2, t#:0] mdbg>
```

Note that the change in the variable value will persist

#### Breakpoints

*I am very sad to say, that I was unable to set breakpoints using `Mdbg`, in spite of googling the heck out of the topic.*

To set break points, set them in your code.  Where ever you want to set a breakpoint, add the following line of code.

```csharp
Debugger.break();
```

Note that you must have `using System.Diagnostics` at the beginning of your code

> NOTE: This line of code will have *no* effect if you are not using a debugger when you run your code.

**Example Code**

```csharp
using System;
using System.Diagnostics;

namespace ahha
{

    // ========================================================================
    // This is our main class.  All of our functions will be in this class
    // ========================================================================
    class MainClass
    {

        // ========================================================================
        // This is our main program.  It doesn't do much
        // ========================================================================
        public static void Main(string[] args)
        {
            int x = 33;
						double yourNumber;
            Console.Write("Please enter a number: ");
			
            string answer = Console.ReadLine();
            double.TryParse(answer, out yourNumber);
            Console.WriteLine("Your number is: " + yourNumber);

	       	// call some silly function
					foo();
			
					yourNumber = x * 33;
			
					Console.WriteLine("Good bye!");
			
        }

        // ========================================================================
        // This is just a function that does not do much either
        // ========================================================================
        public static void foo()
        {
						int j = 21;
						int i = 56;
            //**************************** BREAK POINT *****************************
    				Debugger.Break();
            Console.WriteLine("hello foo");
						i = i * j;
						j = i * j;
						Console.WriteLine("all done!");
        }

    }

}

```

*Example Output*

```text
C:\Users\compsci\JAC\JAC\1P6\1P6\code>csc /debug+ /d:TRACE;DEBUG  debug_example.cs
Microsoft (R) Visual C# Compiler version 3.7.0-6.20375.2 (34202cc2)
Copyright (C) Microsoft Corporation. All rights reserved.


C:\Users\compsci\JAC\JAC\1P6\1P6\code>mdbg debug_example
MDbg (Managed debugger) v0.0.0.0 started.
Copyright (C) Microsoft Corporation. All rights reserved.

For information about commands type "help";
to exit program type "quit".

run debug_example
STOP: Breakpoint Hit
located at line 17 in debug_example.cs
[p#:0, t#:0] mdbg> path .
Path set to: .
14          // This is our main program.  It doesn't do much
15          // ========================================================================
16          public static void Main(string[] args)
17:*        {
18              int x = 33;
19                      double yourNumber;
[p#:0, t#:0] mdbg> symbol path .
Current symbol path: .
[p#:0, t#:0] mdbg> go
Please enter a number: 33
Your number is: 33
STOP UserBreak
43:             Debugger.Break();
[p#:0, t#:0] mdbg> where
Thread [#:0]
*0. ahha.MainClass.foo (C:\Users\compsci\JAC\JAC\1P6\1P6\code\debug_example.cs:43)
 1. ahha.MainClass.Main (C:\Users\compsci\JAC\JAC\1P6\1P6\code\debug_example.cs:27)
[p#:0, t#:0] mdbg> print
j=21
i=56
[p#:0, t#:0] mdbg>

```

