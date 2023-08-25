# Functions

A function is a **reusable block of code** that we can call whenever necessary. It avoids repeating the same code multiple times in a program.

You can thing of a function as a **code recipe** that can be executed at virtually any point in your program.

It has the following advantages:

- **Avoids repetitive code**.
	- Keep it DRY: Don't Repeat Yourself.
- **Creates reusable code.**
	- Think of a function as a temporary detour. When the function is complete, the program goes back to where it was when the function was called.
- **Helps keep code modular and organized**.
	- Take long bits of code and break it up to manageable chunks.
	- It can be difficult to find specific functionality in larger programs. All modern code editors allow  navigation by moving between functions.


## Starting Example

Consider a program that prompts the user for 3 questions. Each input needs to be validated as a positive integer number. The questions are:

- Age.
- Number of family members in their household.
- How many years of professional experience they have.

For each question, the code might look like the following:

```csharp
int age;
string question1 = "Age";

do
{
	Console.WriteLine($"Please enter the following information: {question1}.");
	age = int.Parse( Console.ReadLine() );

	if (age < 0 || age > 100) Console.WriteLine ("Invalid input. ");
}
while (age < 0 || age > 100);
```

Copying and pasting the same 9 lines of code 3 times in the same program is harder to maintain. In order to fix or improve the code, a developer would have to change the same 9 lines on all 3 locations.

We will learn to convert the code above into a function.


## Rules for Function Design

* Functions should **do only one thing**.
* Function **names should be meaningful** (name should describe functionality).
* Don't use reserved keywords as function names (e.g. `while` or `if`)
* Functions should be **as generic as possible** in order to be easily replaceable.
* In this course functions should be declared **outside of the Main program**.


## Inputs and Outputs

Functions typically take inputs and based on its code block (the recipe), will generate an output.

> The **type** of inputs and output that a function can handle must be defined.

However, some functions don't receive any inputs and don't generate any inputs.

![Cartoon of a function machine with inputs and outputs](https://cdn-learn.adafruit.com/assets/assets/000/023/235/original/raspberry_pi_io_machine.png?1424110415 ":size=400")
*Source: [Adafruit learning system](https://learn.adafruit.com/assets/23235) *

## Function Structure

In C#, functions have the following structure:

```csharp

static return_type FunctionName(input_type inputA)
{
	// code block
	return variableToReturn;
}
```

Where:

- `static` - Keyword that defines how to reach this function. For now, `static`  means this function can be accessed from anywhere in your `Program` class.
- `return_type` - The type of variable that this function will return (provide as it's output).
	- Examples of return types:
		- `int`, `string`, `double`, `bool`
		- `void` - this means that nothing will be returned.
- `FunctionName` - Name of the function. Convention is to user UpperCamelCase.
- `inputA` - An input variable (also called an **argument**) that this function is receiving and will be used inside the function's code block.
- `input_type` - The **data type** of variable  `inputA`.
	- Examples of input data types:
		- `int`, `string`, `double`, `bool`

- `return` - Keyword indicating that the following value will be returned by the function as its **output**.
- `variableToReturn` - Is the value or variable that the function will return (provide) as it's **output**.

> **Notes**
> - In it's simplest form, functions can receive zero inputs and return zero outputs.

We'll start by looking at the simplest form of functions: no inputs and no outputs.


## Declaring & Calling Functions

### Declaring Void Functions

Void functions do not receive any inputs (inputs are also called arguments).

Since the function is not returning any data, it must be declared with the keyword `void`.

The function declaration would look like the following:

```csharp
static void SayHello()
{
	Console.WriteLine("Hello");
}
```

This function:

- Does not receives any inputs. Therefore, nothing is listed between the parenthesis.
- Does not returns anything as it's output. Therefore, it's return value is `void` (nothing).


### Calling a Function

In order for a function to be executed, it must be first declared and then **called** (invoked).

To call a function we simply use it's name followed by parenthesis.

```csharp
Console.WriteLine("Saying hi to a friend...");

SayHello();    // function being called.
```


### Declaration & Call in a Program

If writing a complete program, the function would be declared and called in the following manner:

```csharp
using System;

namespace testing
{
    class MainClass
    {
        public static void Main(string[] args)
        {
			Console.WriteLine("Saying hi to a friend...");
			
			SayHello();    // function being called.
        }

        // =============================================================
        // SayHello()
        // Prints a standard greeting to console
        // =============================================================
		
		static void SayHello()   // Declaration outside Main function
		{
			Console.WriteLine("Hello");
		}
    }
    // Do not create functions outside the class block
}
```


### Checklist

* [ ] Never call function `Main()`. It is automatically called **only once**, when the program is executed.
- [ ] Do NOT name your functions the same as variable names.
- [ ] Make sure there are opening and closing parenthesis for the function declaration and call.

```csharp
// Function declaration

static void GoodFunction()		// no semicolon !
{
	// code block
}
```
  
```csharp
// Function call (or invocation)

static void Main(string[] args) 
{
	GoodFunction();
}
```


## Function Inputs

Functions typically take **arguments** (special name for an input variable).

Arguments are listed in the function declaration and must have specify their data type.
Once the argument is listed, it can be used inside the function as a regular variable.

```csharp
static void HelloName(string name)    // name is an input of type string
{
	Console.WriteLine("Hello " + name);
}
```

When the function is called, the input would be passed inside the parenthesis:

```csharp
using System;

namespace testing
{
    class MainClass
    {
        public static void Main(string[] args)
        {
			Console.WriteLine("Saying hi to a friend...");

			HelloName("Mauricio");    // Calling function with an input of type string
        }
		
		static void HelloName(string name)   // Declaration outside Main function
		{
			Console.WriteLine("Hello " + name);
		}
    }
}
```


### Multiple inputs

Functions can receive multiple inputs, which are separated by a comma (`,`)
```csharp
// Declaration
static void CustomGreeting(string greeting , string name)   // two inputs separated by comma
{
	Console.WriteLine(greeting + " " + name + "!");
}
```

Both inputs (arguments) must be provided when calling the function.

They are also separated by a comma:

```csharp
// Call
Console.WriteLine("Saying hi to a friend...");

CustomGreeting("Yo", "Mauricio");   // Two arguments of type string separated by comma
```


## Exercises

### Exercise 1
Complete the [W3School exercises 1 to 4](https://www.w3schools.com/cs/exercise.php?filename=exercise_methods1) from C# methods.
*PS. the word "method" is a synonymous for function.*

### Exercise 2
Create a function called `PrintSum` that takes two integers as inputs and prints their sum (addition) to the console.

### Exercise 3
Create a function called `IsValid` which receives an integer and prints to console whether or not this integer is valid according to the following rule:
- The integer is valid if it is more than 0 and smaller than 100;
 
### Exercise 4 (challenge)
Create a function called `Validator` which receives 3 integers:
- The first integer is the number to be validated. Call this input `number`.
- The second integer is the minimum possible value that `number` can be. Call this input `minimum`.
- The third integer is the maximum possible  value that `number` can be. Call this input `maximum`.

Make this function return `true` if `number` is between `minimim` and `maximum` (not inclusive). Otherwise the function should return `false`.

*PS. This lesson has not covered return values, however, you can figure this out by looking at the general structure of a function (previous section in the notes).*
and prints to console whether or not this integer is valid according to the following rule:
- The integer is valid if it is more than 0 and smaller than 100;
