# Typecast and Mixed Types



Sometimes you need to temporarily convert a number into another type so that is matches. 

**example**: 

 ```csharp
  int apples = 25; 
  double grapes = 3.35; 
 
  grapes = grapes * apples; // will this work??? I'm mixing types….. uh oh….not sure. 
 
  // what about: 
  apples = apples * grapes; // not sure either 
 ```



 Now what is you want to multiply these? An integer and a Double??? Will you get into trouble here? 

Some languages are "loosely typed" and some are very "strictly typed". C# is finnicky with its types, so we need to typecast 

## Explicit Casting

> **General Rule** - to avoid relying on the system to "maybe" do something for you - you should "typecast" your variables to the type on the left hand side of the equals. 

 **Rules**

* You want everything on the right hand side of the equals sign to match the type of the variable on the left hand side of the equals sign.
* to change type, enclose the type name in parenthesis before your variable. 
  * *Example*: ` (int) var1 `
    * this means, convert `var` to an `int` for this calculation only!

**Example**: 

 ```csharp
 int abc = 2; 
 double def = 6.8; 
 
 abc = abc * (int) def; 
 
 // similarly 
 def = def * (double) abc; 
 ```



Remember - typecast is only temporary for that equation or line of code. Typecast does not change they type of the variable which was assigned at birth.  

FYI - if you typecast a `double` to an `int`, it will be TRUNCATED !

> **Truncated**: the decimal portion of the real number will be chopped off.  
>
> This has the affect that the real number will always be rounded towards zero to the nearest integral value.
>
> *Positive numbers*: `(int) 45.9 = 45`,  `(int) 45.0 = 45`, `(int) 45.1 = 45`
>
> *Negative numbers*: `(int) -45.9 = -45`,  `(int) -45.0 = -45`, `(int) -45.1 = -45`

## Type Converstion Methods

[reference](https://www.w3schools.com/cs/cs_type_casting.php)

It is also possible to convert data types explicitly by using built-in methods, such as `Convert.ToBoolean`, `Convert.ToDouble`, `Convert.ToString`, `Convert.ToInt32` (`int`) and `Convert.ToInt64` (`long`):

```csharp
int myInt = 10;
double myDouble = 5.25;
bool myBool = true;

Console.WriteLine(Convert.ToString(myInt));    // convert int to string
Console.WriteLine(Convert.ToDouble(myInt));    // convert int to double
Console.WriteLine(Convert.ToInt32(myDouble));  // convert double to int
Console.WriteLine(Convert.ToString(myBool));   // convert bool to string

```

### What is the difference between explicit type casting and converting?

Converting a real number to integer uses *rounding* instead of *truncation*.  See example below:

```csharp
double a = 45.7;
int b = (int)a;
int c = Convert.ToInt32(a);

Console.WriteLine("original number: " + a);
Console.WriteLine("integer cast: " + b);
Console.WriteLine("convert to Int32: " + c);

```


# Functions

Why?

### Do NOT repeat code!

Sometimes it is necessary to repeat some code, over and over and over again.  This is **bad**.  If you have a mistake in your logic, you need to fix it in more than one place.  If you forget one bit of code, you will still. have a bug.

```text
// Pseudo code:
// Assume that verifying numbers take at least 10 lines of code

Ask user for their age
Verify that the number is a positive integer, and not a string
... many lines of code ...

Ask user for the number of years they have been working
Verify that the number is a positive integer, and not a string
... many lines of code ...

Ask user for the number of children that they have
Verify that the number is a positive integer, and not a string
... many lines of code ...

... more code
```

So, what we can do?

We can take the repeated code, and place it into a single function.

Think of a function as a temporary detour. And when the function is complete you go back to where you were called from. 

```text
// Pseudo code:

Ask user for their age
call GetNumber // does all the verification for us, and then goes to line 6 when done

Ask user for the number of years they have been working
call GetNumber // does all the verification for us, and then goes to line 9 when done

Ask user for the number of children that they have
call GetNumber // does all the verification for us, and then goes to line 12 when done

... more code ...

// define a funtion GetNumber
Verify that the number is a positive integer, and not a string
... many lines of code ...

```

Now, if we have a mistake in our logic for verifying positive numbers, we only have to change the code starting at line 14.

### Keep Code Tidy!

Once your programs become very large, it can be difficult to find the bits of code that you are looking for.  All modern code editors allow you to see an 'outline', i.e. every function that you define, and you can skip to each function at will.

So take a long bit of code, and break it up to manageable chunks.

**Assignment 3 - before**

```text
// ==============
// User chose option 1
// ==============
if option 1
	// =================
	// comments describing what this game is
	// =================
  ... do a bunch of stuff
  // comment describing what we are doing
  ... some stuff
  // more comments
  ... more stuff
  
// ==============
// User chose option 2
// ==============
if option 2
	// =================
	// comments describing what this game is
	// =================
  ... do a bunch of stuff
  // comment describing what we are doing
  ... some stuff
  // more comments
  ... more stuff
  
... etc...
```

**Assignment 3 - after**

So for lab #2 you have several questions - it would be cool to put them into functions. This gives a very modular look/feel to your code. Every routine is broken into a function and is discrete and independent as opposed to being all mixed up together. 

```text
// ==============
// Process user options
// ==============
if option 1
  call game1
if option 2
	call game2

... etc ...

// =================
// game 1
// comments describing what this game is
// =================
define game 1 function
	... do a bunch of stuff
	// comment describing what we are doing
	... some stuff
	// more comments
	... more stuff

// =================
// game 2
// comments describing what this game is
// =================
define game 2 function
	... do a bunch of stuff
	// comment describing what we are doing
	... some stuff
	// more comments
	... more stuff

```



### Re-usability

If you create *good* methods, that can be used by you, or other people, for similar tasks, thus reducing the amount of coding that is required.

### Rules

* Functions should do ONE thing, and ONE thing only!
* Function names should be meaningful (so you don't have to guess at what it does if you are using it)
* Functions should be generic as reasonably possible.  Don't write functions that depend on the specifics of the overall program that you are writing.

## Void Functions

Functions have different flavours - for now we are only looking at void functions with no arguments being passed. 

### How to create and call a void function

You must use the keywords `static` and `void` before the function name!

The reasons why will be explained at a later date.

```csharp
using System;

namespace testing
{
    class MainClass
    {
        public static void Main(string[] args)
        {
            // call function gracie.
            // the paranthesis after the name 'gracie' indicates that it is
            // a function
            gracie();
            Console.WriteLine("Hello");

            larryfunc();    // Calling larry

            gracie();

            Console.ReadLine();
        }

        // =============================================================
        // larryfunc()
        //      - talks a lot
        // =============================================================

        // I create the larryfunc function in the same bracket level as Main

        static void larryfunc()     // you MUST use "static"
        {
            // every function must open using squiggly brackets

            Console.WriteLine("bla bla bla");
            
        }   // every function must close using squiggly brackets

        // =============================================================
        // gracie()
        //      - asks for food
        // =============================================================
        static void gracie()
        {
            Console.WriteLine("meeeooooowwwww!!!!");
        }
    }

    // DO NOT CREATE FUNCTIONS HERE !!!!
}

```

**Note - the fact that larryfunc is above gracie is of NO RELEVANCE. Functions can be in any order. They are only invoked when they are explicitly called **

### Checklist

**Checklist for proper function creation** 

- Create your function in the proper place - below Main, and in the same level of depth as Main. 

- Always name your functions uniquely - do not name your functions with silly characters, do not name your functions with reserved words. 

  **Example:**

  ```csharp
  // this is invalid, because `while` is a reserved word.
  static void while () 
  {  
  }
  ```

- Do NOT name your functions the same as variable names 

- Make sure you have an opening and closing brace for the function 

* Make sure you have the open and close round brackets after the function name 

  ```csharp
  static void goodfunc()		// no semicolon !
  {
    // code here
    // code here
  }
  ```
  
* When you call (or invoke, or run) the function you must call it using the round brackets as well 

   ```csharp
   static void Main(string[] args) 
   {
     goodfunc();
   }
   ```

* Remember, your current function will return to where it was called. 

* Do not call function `Main()` from within another function. Matter of fact - **NEVER** call `Main`. `Main` is automatically called ONCE AND ONLY ONCE when you start executing your code. 

 



 

