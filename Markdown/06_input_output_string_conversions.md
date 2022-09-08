# 06: Input-Output & Conversions
📑 In this lesson will:

- Review information output with `Console.WriteLine()` and `Console.Write()`.
- Collect user input using `Console.ReadLine()`.
- Convert strings to integers using `int.Parse()`.
- Use basic mathematical operations `*`, `/`, `+`, `-`.
- Introduce the `double` numerical type.
- Convert `double` to `int`.

📢 Announcements:

- Next class there will be a small lesson and a lab on the content taught so far.
- The lab is worth 0.5% and must be submitted be the end of the session.

## Program Input & Output

In this course we are using the console as the primary interface to interact with the user.

> The console is also know as the **command line interface (CLI)** or **terminal**.

Using the console we must be able to collect user input and communicate program output.

### Output

We've already seen how to write (also know as print) something to the console window with the `Console.WriteLine()` function.

#### Console.WriteLine()

`Console.WriteLine()` prints to the screen whatever is enclosed by the parenthesis `()`.

```csharp
Console.WriteLine("Hello World"); // Notice the quotes around the string
Console.WriteLine(357);           // Print the number 357, (no quotes needed)

// Writing to the console using variables
string myVariable = "Goodbye World";      // Create a string variable
int myOtherVariable = 35;                 // Creating an integer variable

Console.WriteLine(myVariable);            // Print the contents of the variable
Console.WriteLine(myOtherVariable);       // Print the contents of the variable

// OUTPUT:

// Hello World  
// 357
// Goodbye World  
// 35
```

As the name suggests, `Console.WriteLine()` will output its information in a single line and then "break" the line. This means that subsequent text will always be in a new line.

#### Console.Write()

There is yet another function, `Console.Write()`, which will print text **without breaking the line**.
This means that everything will be placed in the same line of text.

Consider the previous example but using `Console.Write()`:

```csharp
Console.Write("Hello World");
Console.Write(357);

string myVariable = "Goodbye World";
int myOtherVariable = 35;

Console.Write(myVariable);
Console.Write(myOtherVariable);

// OUTPUT:

// Hello World357Goodbye World35
```

### Input

To ask a user for information, you need to do **two steps**:

1. Tell the user what information you want typed.
2. Read that information from the console window.

In computer science it's common to use the term "**to prompt for input**" when asking the user to provide information.

You already know how to accomplish **step 1** using  `Console.WriteLine()` or  `Console.Write()`.
Step 2, can be accomplished by using `Console.ReadLine()`.

#### Console.ReadLine()

The function `Console.ReadLine()` will pause the program and wait until the user has typed something and hit the <kbd>Enter</kbd> key.

The information collected by `Console.ReadLine()` is returned is a `string`. This means you must:
1. First declare a `string` variable.
2. Then read user input with  `Console.ReadLine()` by assigning its return value to the `string` variable you created.

```csharp
string name;        // create a string variable called 'name';
Console.Write("Please enter your name: "); // prompt the user
name = Console.ReadLine();         // read what the user typed and store in 'name'

Console.WriteLine($"Hello {name}, how are you?");   
```

> ⚠ `Console.ReadLine()` **always returns a string**, even if the user enters a number.

 If a numeric character is entered by the user, `Console.ReadLine()` returns it as a string. See example below.

```csharp
int myAge = 41;
string userInput;

Console.WriteLine("Enter your age: ");
userInput = Console.ReadLine();

int ageDifference = myAge - userInput;    // ERROR! Operator '-' cannot be applied to operands of type 'int' and 'string' 
Console.WriteLine($"I am {ageDifference} years older than you.");
```

If you would like to capture user input as a number, you must **first convert the input from string to integer.** See below.

#### What is the Console?

A console is also know as the terminal or command line interface. 

It's basically a how for humans to interact with the computer using purely text.

> **The console** is an operating system window where users interact with the operating system or with a text-based console application by entering text input through the computer keyboard, and by reading text output from the computer terminal.
> 
> For example, in the Windows operating system, the console is called the Command Prompt window and accepts MS-DOS commands.
> 
> In C#, the [Console](https://docs.microsoft.com/en-us/dotnet/api/system.console?view=net-6.0) class provides basic support for applications that read characters from, and write characters to, the console.

*Source: Microsoft [documentation on Console class](https://docs.microsoft.com/en-us/dotnet/api/system.console?view=net-6.0).*

See the section Diving Deeper at the end of the notes for a detailed video on what is a command line interface.

### From Strings to Integers with `int.Parse()`

Remember that computers, internally, cannot tell the difference between numbers and strings (text).  The string `"35"` is stored in the computer in a **_very_** different way than the integer `35`.

> Remember that the word ***parse*** refers to reading text, and inferring specific information.

There are a few different ways to convert a `string` to `int`. For now, we'll use the function `int.Parse()`:

```csharp
string variableOne = "35";
int variableTwo = 10;

int varOneAsInt;
varOneAsInt = int.Parse(variableOne);

Console.WriteLine($"Subtracting two from one gives: {varOneAsInt - variableTwo}");
```

> **Note:** If the computer cannot convert the string to a number, then it will crash the program. 💥

```csharp
// THIS WILL CRASH THE PROGRAM, BECAUSE 'HELLO WORLD' CAN NOT
// BE INTERPRETED AS AN INTEGER !
string variableOne = "hello world";
int variableTwo;
variableTwo = int.Parse(variableOne);
```


## Basic Math Operations

Like in most languages, in C#, you can perform basic mathematical operations using the symbols below:

| Symbol | Meaning  |
| ------ | -------- |
| `*`    | multiply |
| `/`    | divide   |
| `+`    | add      |
| `-`    | subtract |

Example 1:

```csharp
int unitsPerPallet = 10;    // Units insite a pallet.
int qtyPallets = 5;

int totalUnits = unitsPerPallet * qtyPallets;
// Output: 50
```

Example 2:

```csharp
int varA = 10;
int varB = 2;

Console.Write($"Multiplication: {varA * varB}, Division: {varA / varB}, Subtraction: {varA - varB}");

// Output
// Multiplication: 20, Division: 5, Subtraction: 8
```

>Note that when using string interpolation (`$" "` syntax), we can write a **full expressions** inside the `{ }`, not just variable names.


### Integer Truncation 🔪

The math shown above conveniently used numbers that divide "nicely" into whole numbers.

However, we can run into problems when dividing integers that result into decimals:

```csharp
int a = 1;
int b = 2;

int half = a / b;
Console.WriteLine($"One divided by two is: {half}");
// Output: 0
// Why?!
```

We expected the code above to yield "0.5"! Why zero?!

Integers cannot represent decimal places, therefore, **any decimals get discarded**, this is also known as **truncation**.

>**Truncated**: the decimal portion of the real number will be chopped off. 
>
> This has the affect that the real number will always be rounded towards zero to the nearest integral value.
>
> *Positive numbers*:
> `45.9 to int -> 45`,
> `45.0 to int -> 45`,
> `45.1 to int -> 45`
>
> *Negative numbers*:
> `-45.9 to int -> -45`,
> `-45.0 to int -> -45`,
> `-45.1 to int -> -45`

To avoid truncation, we'll need a type of variable that can handle decimals: the `double` data type.


## Double Numeric Type

Unlike the `int` numeric type, the `double` type **can store decimal places**.

The `double` data type has a precision of approximately 16 digits and is represented by 64 bits (for comparison, `int` uses 32 bits).

There are limitations for the precision and the size of the numbers that a `double` can represent. If you are curious, you can try printing `double.MinValue` or `double.MaxValue`.

```csharp
int age = 22;
double itemPrice = 5.99;
double pi = 3.141592;
```

If you are curious, in C# there are 10 [integral types](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types) (similar to `int`) and 3 [floating-point numeric types](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/floating-point-numeric-types) (similar to `double`).

Notice that trying to assign the integer `35` to a `double` will work, however, C# is **automatically converting** (aka. *implicitly casting*) the `int` to a `double`.

```csharp
double age = 35;    // Bad practice! 35 is an int converted to double "behind the scenes".
```

As you will see below, automatic conversion can sometimes lead to unexpected results and is considered bad practice.

Instead, explicitly assign a `double` number to your `double` variable:

```csharp
double age = 35.0;    // Much better. 35.0 is a "real" double.
```


## Mixing `integer` and `double` arithmetic

If you use a number in an equation, and that number does not have a decimal point, then it will be considered to be an `integer` (ex.: `5`, `6`).

If you want the equation to use a real number, you _must_ add the decimal point, followed by at least one other number (ex.: `5.0` is a valid `double` and  `5.` is NOT).

> Remember: mathematical formulas (not variable assignment) are executed **from left to right**.

Rules:

1.  If an `integer` multiplies or divides an `integer`, the result will be an `integer`
2.  If an `integer` adds or subtracts an `integer`, the result will be an `integer`
3.  If an `integer` multiplies or divides a `double`, the result will be a `double`
4.  If an `integer` adds or subtracts a `double`, the result will be a `double`

Look at the code below, and at the result. _Can you figure out why the results are what they are?_

```csharp
double age;

age = 5 / 9 * 60;
Console.WriteLine(age);
age = 60 / 9 * 5;
Console.WriteLine(age);
age = 60 * 5 / 9;
Console.WriteLine(age);

age = 5.0 / 9.0 * 60.0;
Console.WriteLine(age);
age = 60.0 / 9.0 * 5.0;
Console.WriteLine(age);
age = 60.0 * 5.0 / 9.0;
Console.WriteLine(age);
```

_Result_

```text
0
30
33
33.3333333333333
33.3333333333333
33.3333333333333
```

**Explanation of above**

Line 3: `5 / 9 * 60` = `int( 5/9 )` `* 60` = `int( 0 * 60 )` = `0`

Line 5: `60 / 9 * 5` = `int( 60/9 )` `* 5` = `int( 6 * 5 )` = `30`

Line 7: `60 * 5 / 9` = `int( 60*5 )` `/ 9` = `int( 300 / 9)` = `33`

Line 10: by using `5.0/9.0` we are forcing the calculations to be done with real numbers, not integers.

### Implicit Casting

When a type of variable is "converted" into another type, in computer science we call this **casting**.

> Note that by mixing `int` and `double` in the same calculation (examples above) we are relying on C# to convert variables "behind the scenes".
> 
> This behind the scenes conversion that happens "automatically" is called **implicit casting**.

As you can see in the previous section, the way how implicit conversion happens is not always obvious and can easily lead to bugs.

It is far better to be explicit about type casting.

> 💣 Implicit casting is considered a bad coding practice and will have marks deducted.


### Explicit Casting

It is possible (and recommended) to explicitly convert data types by using the `Convert` built-in functions:

- `Convert.ToDouble( value )`: Converts an `int` value to `double`.
- `Convert.ToString( value )`: Converts an `int` or `double` value to `string`.
- `Convert.ToInt32( value )`: Converts a `double` value to `int32`, which is the standard `int` type (32 bits long).

```csharp
int myInt = 10;
double myDouble = 5.25;

Console.WriteLine(Convert.ToString(myInt));    // convert int to string
Console.WriteLine(Convert.ToDouble(myInt));    // convert int to double
Console.WriteLine(Convert.ToInt32(myDouble));  // convert double to int
```

Using the `Convert` functions also avoid **truncation** 🔪

```csharp
int varA = 1;
int varB = 2;

Console.WriteLine( varA / varB );  // Output: 0
Console.Write( Convert.ToDouble(varA) / Convert.ToDouble(varB) );  // Output: 0.5
```


## Diving Deeper (optional)

Why do we use command line interfaces (aka. the console) to interact with the computer?

<iframe width="560" height="315" src="https://www.youtube.com/embed/4RPtJ9UyHS0?start=325" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>




