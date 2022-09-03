

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





 

 

 

 

