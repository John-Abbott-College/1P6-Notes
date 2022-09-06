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

However, there is another function, `Console.Write()`, which will print text **without breaking the line**.
This meas that everything will be placed in the same line of text.

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

In computer science it's common to see the term "**to prompt for input**" when asking for user to provide information.

You already know how to accomplish **step 1** using  `Console.WriteLine()` or  `Console.Write()`. There are a few different ways to accomplish step 2, `Console.ReadLine()` is one of them.

#### Console.ReadLine()

The function `Console.ReadLine()` will pause the program and wait until the user has typed something and hit the <kbd>Enter</kbd> key.

The information collected by `Console.ReadLine()` is returned is a `string`. This means you must:
1. First create a `string` variable, and
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

int difference = myAge - userInput;    // ERROR! Operator '-' cannot be applied to operands of type 'int' and 'string' 
Console.WriteLine($"I am {difference} years older than you.");
```

If you would like to capture user input as a number, you must **first convert the input from string to integer.** 

### From Strings to Integers with `int.Parse()`

Remember that computers, internally, cannot tell the difference between numbers and strings (text).  The string `"35"` is stored in the computer in a **_very_** different way than the integer `35`.

> Remember that the word *parse* refers to reading text, and inferring specific information.

There are a few different ways to convert a `string` to `int`, for now we will use the function: `int.Parse()`:

```csharp
string variableOne = "35";
int variableTwo;
variableTwo = int.Parse(variableOne);
```

NOTE: If the computer cannot convert the string to a number, then it will crash the program.

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

### Integers Truncation

```csharp
int unitsPerPallet = 10;    // Units insite a pallet.
int qtyPallets = 5;

int totalUnits = unitsPerPallet * qtyPallets;
// Output: 50
```

However, we can problems if we divide integers:

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

Notice that trying to assign the integer `35` to a `double` will result in error.

```csharp
double age = 35;    // Error! 
```


## Mixing `integer` and `double` arithmetic

If you use a number in an equation, and that number does not have a decimal point, then it will be considered to be an `integer`. (**Ex** `5`, `6`)

If you want the equation to use a real number, you _must_ add the decimal point, followed by at least one number (**Ex** `5.0` is a valid `double` and  `5.` is NOT a valid number).

> Mathematical formulas are executed **from left to right**.

Rules:

1.  If an `integer` multiplies or divides an `integer`, the result will be an `integer`
2.  If an `integer` adds or subtracts an `integer`, the result will be an `integer`
3.  If an `integer` multiplies or divides a `double`, the result will be a `double`
4.  If an `integer` adds or subtracts a `double`, the result will be a `double`

Look at the code below, and at the result. _Can you figure out why the results are what they are?_

```csharp
Double age;

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

`line 3`: `5 / 9 * 60` = `int( 5/9 )` `* 60` = `int( 0 * 60 )` = `0`

`line 5`: `60 / 9 * 5` = `int( 60/9 )` `* 5` = `int( 6 * 5 )` = `30`

`line 7`: `60 * 5 / 9` = `int( 60*5 )` `/ 9` = `int( 300 / 9)` = `33`

`line 10:`, by using `5.0/9.0` we are forcing the calculations to be done with real numbers, not integers.

#### Implicit casting

When a type of variable is "converted" into another type, in computer science we call this **casting**.

> Note that by mixing `int` and `double` in the same calculation (example above) we are relying on C# to convert variables behind the scenes.
> 
> This behind the scenes conversion that happens "automatically" is called **implicit casting**.

As you can see in the previous section, how implicit conversion happens is not always obvious and can easily lead to bugs.

It is far better to be explicit about type casting.

> 💣 Implicit casting is considered a bad coding practice and will have marks deducted.


## Converting `int` to `double`

It is possible (and recommended) to explicitly convert data types by using the `Convert` built-in functions:

- `Convert.ToDouble()`: Converts an `int` to `double`.
- `Convert.ToString()`: Converts an `int` or `double` to `string`.
- `Convert.ToInt32()`: Converts a `double` to `int32`, which is the standard `int` type (32 bits long).

```csharp
int myInt = 10;
double myDouble = 5.25;

Console.WriteLine(Convert.ToString(myInt));    // convert int to string
Console.WriteLine(Convert.ToDouble(myInt));    // convert int to double
Console.WriteLine(Convert.ToInt32(myDouble));  // convert double to int
```

Using the `Convert` functions also avoid **truncation** (see previous section).

