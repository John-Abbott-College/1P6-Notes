# If Else-If Statement


## If Else-if Statement

We previously looked at the `if-else` statement which has the following structure:

> Structure of the `if-else statement`:
>
> `if ( boolean conditional )`<br/>
>&emsp; &emsp; `code block`<br/>
> `else`<br/>
> &emsp; &emsp; `code block`

However, this is limiting. Notice how there is **only one** boolean condition that can be included.

The `if else-if` statement enables us to check for multiple boolean conditions within the same `if` statement

```csharp
if ( boolean condition 1)
{
	// code block 1
}
else if ( boolean condition 2 )
{
	// code block 2
}
else
{
	// code block 3
}
```

There could be an unlimited number of `else-if` statements, each with it's own boolean condition.

> In a `if else-if` statement, each boolean condition is checked is order (top to bottom).
> 
> 👉 **As soon as one condition is true, the associated code block will be executed, and no further conditions will be evaluated**


### `if else-if` Example 1

The user enters their grade and the program determines the equivalent letter grade.

```csharp
int gradePercent;
Console.WriteLine("Please enter your grade %");
gradePercent = int.Parse( Console.ReadLine() );

Console.Write("Letter grade is: ");

if (gradePercent >= 90)
{
	Console.WriteLine("A");
}
else if (gradePercent >= 75)
{
	Console.WriteLine("B");
}
else if ( gradePercent >= 60)
{
	Console.WriteLine("C");
}
else
{
	Console.WriteLine("F");
}
```

### `if else-if` Example 2

The user selects their meal from a menu.

```csharp
Console.WriteLine(@"
    A- Pizza
    B- Hamburger
    C- Hotdog
");
Console.Write("Please select your meal from the menu above: ");

string selection = Console.ReadLine();

Console.Write("Thank you. Your ");

if (selection == "A")
{
	Console.Write("Pizza");
}
else if (selection == "B")
{
	Console.Write("Hamburger");
}
else
{
	Console.Write("Hotdog");
}

Console.WriteLine(" will be ready shortly");
```

*Did you notice the @ in the multi-line string?*

## Verbatin Strings

> The `@` symbol inside a string  `" "` is one way to create strings with multiple lines.
> 
> This is called [Verbatim String](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/strings/#verbatim-string-interpolation) and reads all **new lines and spaces exactly like it's written** in the code (verbatim).
>
>Verbatim strings can be combined with **string interpolation** using the syntax `$@" "` in order to add variables inside curly braces`{ }`
> 
> [Raw string literals](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/strings/#raw-string-literals) (`""" """`) also support strings over multiple lines, however, we cannot include variables inside the string (string interpolation).


## Comparing to `if-if-if-else`

A common question a beginner might as is:

> *Why use a `if else-if` statement when I can just write multiple single `if` statements?*

If multiple individual `if` statements were used instead of a `if else-if`, then **every `if` condition** would be evaluated and possibly executed (instead of only the first match).

Compare the letter grade program from example 1 (above) which used `if else-if` blocks with only using repeated `if` blocks:

```csharp
int gradePercent = 80;   // Assume the user entered 80

Console.Write("Letter grade is: ");

if (gradePercent >= 90)
{
	Console.Write("A");
}
if (gradePercent >= 75)
{
	Console.Write("B");
}
if ( gradePercent >= 60)
{
	Console.Write("C");
}
else
{
	Console.Write("F");
}

```

*Result*
```text
Letter grade is: BC
```

Why two grades? The condition the second `if` (`gradePercent >= 75`) is `true`, so its `code block` is executed, and then proceeds to evaluate the next `if` statement (since it's not an `else if`).  The next `if` (`gradePercent >= 60`) is also true, so its `code block` is also executed.

### Irrelevant If Statements

It is a common mistake to write irrelevant if statements that **will never be reached**.

Consider the following **code snippet 1**

```csharp
if (a > 10)
{
	// code block 1
}
if (a <= 10 )
{
	// code block 2 
}
```

Imagine that `a` is greater than 10, then `code block 1` would be executed. However, `code block 2` would never be executed. Either `a` is `greater than` 10, or it is NOT. The second `if` would never be reached.

The following **code snippet 2** is marginally better, but still not good practice.

```csharp
if (a > 10) { /* code block 1 */ }
else if (a <= 10) { /* code block 2 */ }
```

If we have either/or conditions, we should be using `if-else`, show in **code snippet 3** below.

```csharp
if (a > 10) { /* code block 1 */ }
else { /* code block 2 */ }
```

Why?
* In code snippet 1, *both* conditionals must be calculated *every time*!
* In code snippet 2, you have to calculate the comparison again (`a <=10`) if the first condition (`a>10`) is false, even though it is *not* necessary.
* In code snippet 3, the calculation is only done once.

These extra comparisons slows down your program, and makes the user's experience less enjoyable.

> This *slowing down* of the execution might not be noticeable in small programs. However, in professional programming, it can make a significant difference.
> Better to learn *now* how to code correctly


## Generating Random Integers

There is a special function in C# that can generate a random `int` between a low and a high value (including the low but not including the high values).

This function belongs to a `Random` object so this object needs to be created first. Objects are not covered in this course so consider the code below a "recipe" to be copied.

```csharp
int min = 10;    // lowest random value to be generated (included)
int max = 50;    // highest random value to be generated (not included)

Random randomizer = new Random();    // create an object of type Random
int randomInt = randomizer.Next(min, max);   // generates a random int between min and max.
```


## Exercise

🎲 Use the random number generator above to create a dice roll game with the following rules:

- The player rolls 2 dice at a time.
- If the two dice have the same number, it's an instant win.
- If the sum of the dice is 7, it's an instant loss.
- Otherwise, the sum of the dice is the user's score for that round.

For now the program should play a single round, inform the user of the dice roll, the score and exit. The user can manually tally the score if they want.

*We'll eventually improve this game to have multiple players with several rounds.*


