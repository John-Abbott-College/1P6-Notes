# String Concatenation

(or adding strings together)

> Concatenate:  the action of linking things together in a series

In C#, `strings` (a series of characters surrounded by quotes (`"`)) can be *concatenated* by using the plus (`+`) sign.

**Examples**

```csharp
"Hello" + "World";				// equivalent to "HelloWorld"
"Hello " + "World";				// equivalent ot "Hello World"
"Hello" + " " + "World";	// equivalent ot "Hello World"

// Forgot the '+' between the two strings
"Hello" "World";					// ERROR - INVALID SYNTAX

// The plus is inside of the quotes, so is part of the string, so there
// is still no + sign between the two strings
"Hello + " "World";				// ERROR - INVALID SYNTAX

// You cannot have a trailing plus (+) sign.
"Hello " + "World " +	;		// ERROR - INVALID SYNTAX

// Add more than two strings together
"Goodbye"+"Cruel"+"World"; // equivalent to "GoodbyeCruelWorld"

// Spaces outside of the quotes have no affect on the final string
"Goodbye" + "Cruel" + "World"; // equivalent to "GoodbyeCruelWorld"

// Spaces inside the quotes become part of the string
"Goodbye    " + "Cruel   " + "World"; // equivalent to "Goodbye    Cruel   World"
  
```

## String Concatenation using variables

Do *not* enclose the variable name within quotes.  The compiler will not treat anything within quotes as a variable.

**Examples**

```csharp
string name="Sandy";
Console.WriteLine("Hello " + name);		// prints "Hello Sandy"
Console.WriteLine("Hello"   + name);  // prints "HelloSandy"  ... why?
Console.WriteLine("Hello + name");		// prints	"Hello + name" ... why?
Console.WriteLine("Hello " + "name");	// prints "Hello name" ... why?
```

### Concatenating Strings and Numbers

Although it is not considered best-practice to mix strings and numbers together, C# does it quite readily.

**Examples**

```csharp
int age = 35;
string name = "Sandy";
// Prints "Hello Sandy, your age is 35"
Console.WriteLine("Hello " + name + ", your age is " + 35);
```



> **Hidden Data Type Conversions**
>
> Whenever you have a statement that looks like...
>
> ```csharp
> variable = something_expression
> ```
>
> ... this is an `assignment` statement.  The right side of the equals sign (`RHS`) is evaluated first, and the result (`value`) is placed into `RAM` at the memory address associated with the `variable`.
>
> **If the left-hand (`LHS`) side of the assignment statement is a string, and there are plus (`+`) operators on the `RHS`, then everything on the `RHS` is converted to a string before it is concatenated.**

**MAJOR WARNING**

In spite of the documentation from Microsoft, the behaviour of mixing `strings` and `int` types in a statement which includes the `+` operator can be different depending of the construction of the expression.

Example:

```csharp
            output = "Hello " + (35 + 42);
            Console.WriteLine(output);

						output = "Hello " + 35 + 52;
            Console.WriteLine(output);

            output = 35 + 42 + " Hello";
            Console.WriteLine(output);

// OUTPUTS:
//			Hello 77
//			Hello 3552
//			77 Hello
```

#### Best Way to Mix `String` and `int`

To avoid ambiguity in your code, and to improve the readability of code, it is suggested that you use the `ToString()` function to convert any number into a string, *before* using and `+` operators.

```csharp
            output = "Hello " + (35 + 42).ToString();
            Console.WriteLine(output);

            output = "Hello " + 35.ToString() + 52.ToString();
            Console.WriteLine(output);

            output = 35.ToString() + 42.ToString() + " Hello";
            Console.WriteLine(output);

						output = (35 + 42).ToString() + " Hello";
            Console.WriteLine(output);

// OUTPUTS:
//			Hello 77
//			Hello 3552
//			3542 Hello
//			77 Hello
```



# Logic

Programs really boring unless we can add some decision making to them.

## True / False 

For the moment we are going to limit our decision making based on questions that can only be answered by `true` or `false`.  Any question that cannot be answered by `true`/`false` must use a different command then the `if`/`else` construct.

### Basic structure of `if / else statement`

In programming, the idea behind the `if`/`else` block of code works as follows:

**"if statement"**: `if`   `( expression )` ` code block ` 

where the `expression` evaluates to either `true` or `false`

* Example: `if (x > 10)`  `code block`

* a `code block` is one or more code statements enclosed in `curly braces` "{}" ).  

  This code will be executed **only** if the  `expression` in the `if statement` evaluates to `true`

  * Example of a `code block`

    ```csharp
    {
    	// This entire code block will only execute 
    	// if (and only if), x is greater than 10
    
    	Console.WriteLine("This is a code block");
    	x = 12;
      
    	// I can have as many lines of code in a code block as I want
    	y = x * 2;
    }
    ```

**"else"**: (*optional*) 

* Must be followed by another `code block`

  This `code block` will be executed **only** if the expression in the `if statement` evaluates to `false` 

### Examples

#### `if` Example:

**pseudo code**

> Ask user for age.
> Is our user an adult?
> If yes, display adult only movie choices
> Display family friendly movies
> Ask user for movie choice

**flowchart**

<img src="./Images/08_if.png" alt="Flowchart of the code shown below" style="zoom:67%;" />

**code**

```csharp
// Do not allow children to watch adult content

// declare constants
int ADULT_AGE = 18; // at least in quebec

// declare variables
int userAge;
int movieNumber;

// get user's age
Console.Write("Please enter your age: ");
userAge = int.Parse ( Console.ReadLine() );

// if old enough you can watch any movie you want
if (userAge >= ADULT_AGE) 
{																				// start of "if" block
  Console.WriteLine("1 - Terminator");
  Console.WriteLine("2 - DeadPool");
}																				// end of "if" block

// notice that there is no 'else' statement
// that is because both adults and children can watch children's movies
Console.WriteLine("3 - Lion King");
Console.WriteLine("4 - Beauty and the Beast");

// choose a movie
Console.WriteLine("Please enter the number of the movie you want to watch");
movieNumber = int.Parse ( Console.ReadLine() );

```

#### `if-else` example

**Psuedo Code** 

> Is our user retired or not?
> Display "How old are you" 
>
> Input user's age  
>
> is the user's age 65 or over?
> 	if yes 
> 		then display "you are retired" 
> 		else 
> 			Display "you can still work" 
>
> rest of code

**flowchart**

<img src="./Images/08_if_else.png" alt="A flowchart diagram of the code shown below" style="zoom:67%;" />

**code**

```csharp
// Program to test if the user is retired or not

// use a constant for retirement age
int RETIREMENT_AGE = 65;

// declare our variables first
int userAge;

// get user input
Console.Write("Please enter your age ");
userAge = int.Parse ( Console.ReadLine() );

// is the user retired?
if (userAge >= RETIREMENT_AGE)		      // if statement
{																				// start of if code block
	Console.WriteLine("You are retired");
}																				// end of if code block
else															      // else statement
{																				// start of else code block
	Console.WriteLine("You are NOT retired");
}																				// end of else code block

// Whether user is retired or not, this code will 
// be executed because the if and else code blocks are complete
Console.WriteLine("Thank you for your patience");

```

## Best Practices for `if/else` code

**Readability**:

Your questions should be as simple as possible - and as English like as possible so that you can read properly. 

Example: 

```csharp
	// Note that || means 'or'

	// keep this as English as possible
	// Now do you see the importance of naming variables properly 
	if  (lives <= 0 ) ||  ( health  <= 0 )  
	{	 
		Console.WriteLine ("Game is over!");
	} 
```



**Only true/false or yes/no questions**

A valid question in a diamond would be *“Are you hungry?”* - because the answer is either yes or no. 

  An invalid (illegal) question would be *“What would you like to eat?”* because the answer is too varied - it could be hot dog, hamburger, chips, or a million other things.  

### Bad Examples

#### redundant questions

**Psuedo Code**

> pick a random number  
> Question - *is your number bigger than 48 ?*
> 	*then set colour to red*
> *Is your number less than or equal to 48*?
> 	*then set colour to blue*

 **Why is this bad?**

Because, if the number is bigger than 48, we know for absolute certainty that it is *not* less than or equal to 48.

Likewise, if the number is *not* bigger than 48, we know for absolute certainty that it *is* equal or less than 48.

So the second question is redundant.

**Better way**

> pick a random number  
> Question - *is your number bigger than 48 ?*
> 	*then set colour to red*
> **_else_**
> 	*set colour to blue*

## Logic operators in C#

| C#   | English                  |
| ---- | ------------------------ |
| \|\| | or                       |
| &&   | and                      |
| <    | less than                |
| <=   | less than or equal to    |
| >    | greater than             |
| >=   | greater than or equal to |
| ==   | equals                   |
| !=   | not equals               |





 

 

 

 

