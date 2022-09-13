# The `if` Statement

Useful programs typically need to make make decisions based on inputs and conditions.

The `if` statement is used to alter flow of a program **if a specific condition is met**.
The answer to this condition **must be** either `true` or `false`.

> The format of and `if statement`  in C# is: 
>
>`if( expression )`<br/> 
>&emsp; &emsp; `code block`

Where:

* *`expression`*  is the condition that must be met.
	* This condition *must* be surrounded by parenthesis `(...)` and is anything that evaluates to `true` or `false` .
* `code block` is a can either be:
  * multiple lines of code, enclosed in squiggly braces `{ ... }`,
  * a single line of code, ending in a semi-colon.

Note:

- * `if` is NOT capitalized
- There is no semi-colon after the code block ( `{ ... }` )
- Line indentation is not required by the compiler, but it is important for humans. Without this clue (indentation), human readers might not realize there is a code block.
	- You may use **auto-format** option in Visual Studio to add indentation with the shortcut key is `CTRL`+`E`, `D`

### `if` Example 1
*(assume the variable temperature is declared and defined)*

```csharp
//  If statement including multiple lines of code

if (temperature > 27)
{   // beginning of code block

 	Console.WriteLine("It's hot!");
 	Console.WriteLine("Please open the window");
 	
}   // end of code block

Console.WriteLine("Cheers!");
```

In the example, above, if `temperature` is greater than (`>`) 27, then the two lines of code (inside the `code block`) will be executed. 

The **condition** would be: "is the temperature greater than 27?". Note how this question is answered with `yes` or  `no`, in other words `true` or `false`.

If the **condition** evaluates to `false`, we **do not** run the two lines inside the code block.

Notice that the `Console.WriteLine("Cheers!");` will **always run** because it is not dependent on the if statement.


## Code Blocks

As mentioned above, a `code block` is one or more code statements enclosed in `curly braces` "{ }" ).  

Example of a `code block`:

```csharp
int x;
int y;    // These declarations are outside of the code block

{   // begining of code block
	Console.WriteLine("This is a code block");
	x = 12;
	// Code blocks can have one or many lines of code
	y = x * 2;
	Console.WriteLine(y);
}   // end of code block
```


### `if` Example 2

**Pseudo code**

> Ask user for age.<br>
> Is our user an adult?<br>
> &emsp;&emsp; If yes, display R-rated movie choices<br>
> Display family friendly movies<br>
> Ask user for movie choice

**Code**

```csharp
// Do not allow children to watch R-rated movies

// declare constants
int ADULT_AGE = 18;

// declare variables
int userAge;
int movieNumber;

// get user's age
Console.Write("Please enter your age: ");
userAge = int.Parse ( Console.ReadLine() );

// if old enough you can watch any movie you want
if (userAge >= ADULT_AGE) 
{       // start of "if" block
  Console.WriteLine("1 - Terminator");
  Console.WriteLine("2 - DeadPool");
}       // end of "if" block

//  No age requirement to watch these movies
Console.WriteLine("3 - Lion King");
Console.WriteLine("4 - Encanto");

// choose a movie
Console.WriteLine("Please enter the number of the movie you want to watch");
movieNumber = int.Parse ( Console.ReadLine() );
```


## `bool` Type: True - False

In computer science, there is a data type created specifically to represent the state of being `true` or `false`: the **boolean data type**.

Similarly to `int`, `double`, and `string`, the `bool` must be declared and assigned.

```csharp
bool goodWeather;      // variable declaration
goodWeather = true;    // variable assignment
goodWeather = false;   // we quickly changed our mind
```

If the idea of something being `true` or `false` confusing, you can think of them as being synonymous to  `yes` and `no`.

For instance we may have a variable **`isRaining`** and state that this represents if it is raining outside or not. The value of **`isRaining`** would be: 

- **`true`** if it is raining outside. 
- **`false`** if it is not raining outside. 

**Other examples**: 

- **`workCompleted`** represents if I have completed my work or not. 
- **`soundAlarm`** represents whether or not the alarm should be on.


### Boolean Expressions

When we introduced the `if` statement, we mentioned it follows the format below:

>`if ( expression )`<br>
> &emsp; &emsp; `code block`

In the examples given, we used the following expressions (see complete examples above):

```csharp
// First example
if (temperature > 27)
{
	... // ignore code block for now 	
}   

// Second example
if (userAge >= ADULT_AGE) 
{  
	...  // ignore code block for now 
}
```

The expressions `temperature > 27` and `userAge >= ADULT_AGE` are boolean expressions because their result evaluates to `bool`. In other words, the result is either `true` or `false`.

We could have printed these expressions to the console:

```csharp
int temperature = 28;
int ADULT_AGE = 18;
int userAge = 17;

Console.WriteLine( temperature > 27 );   // Output: True
Console.WriteLine( userAge >= ADULT_AGE );   // Output: False
```

To create boolean expressions and compare multiple elements we need to use **logic operators**.

## Logic operators in C#

Below is a list of operators we can use to compare things.

We will revisit them in more detail in a future lesson.

| C#   | English                  |
| ---- | ------------------------ |
| <    | less than                |
| <=   | less than or equal to    |
| >    | greater than             |
| >=   | greater than or equal to |
| ==   | equals to                |
| !=   | not equals to            |
| \|\| | or                       |
| &&   | and                      |


##  The `if-else` Statement

The `else` statement is an optional extension of the `if` statement (it must be part of an `if` statement).

> The format of and `if-else statement`  in C# is:
>
> `if ( boolean conditional )`<br/>
>&emsp; &emsp; `code block`<br/>
> `else`<br/>
> &emsp; &emsp; `code block`

Note:

- The `else` is part of an `if` statement. It is OPTIONAL 
- An `if` statement can have only one `else` part 
- The `else` is performed if the `condition` is FALSE
- It's **either** the first code block in the `if` that is performed when the condition is true **or** the second code block in the `else` that is performed if the condition is false. **NEVER BOTH** 

### `if-else` Example 1

```csharp
// assume there is code to manage the lives in the game

if (lives == 0)
{
  	Console.WriteLine("you died");
  	Console.WriteLine("better luck next time");
}
else
{
  	Console.WriteLine("you made it");
  	Console.WriteLine("you are still alive");
}
Console.WriteLine("Thank you for playing");
```

### `if-else` Example 2

**Psuedo Code** 

> Is the user retired or not?
> Display "How old are you" ?
>
> Input user's age  
>
> is the user's age 65 or over?
> 	if yes 
> 		then display "you are retired" 
> 	else 
> 		Display "you can still work" 
>
> rest of code

**Code**

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
{        // start of if code block
	Console.WriteLine("You are retired");
}        // end of if code block
else     // else statement
{        // start of else code block
	Console.WriteLine("You are NOT retired");
}        // end of else code block

// Whether user is retired or not, this code will 
// be executed because the if and else code blocks are complete
Console.WriteLine("Thank you for your patience");

```

## Best Practices for `if-else` code

**Readability**:

Your questions should be as simple as possible - and as English like as possible so that you can read properly. 

```csharp

// keep this as English as possible
// Now do you see the importance of naming variables properly 
if  (lives == 0 )
{	 
	Console.WriteLine ("Game is over!");
} 
```

**Only true/false or yes/no questions**

A valid question would be *“Are you hungry?”* - because the answer is either yes or no. 

An invalid (illegal) question would be *“What would you like to eat?”* because the answer is too varied - it could a number of things.


 

