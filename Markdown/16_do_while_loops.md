# Do While Loops

The `do-while` loop is similar to the `while-loop`, however, **the condition is checked at the end of the loop** rather than at the beginning.

This means that the loop is guaranteed **iterate at least once - even if the condition is false.**

Structure:

```csharp
do 
{ 
	// code block - always executed
	
} while (boolean_expression);  // loop only restarts if boolean_expression is True

```

C# example:

```csharp 
int counter = 0; 

do 
{ 
	Console.WriteLine($"Counter value: {counter}");
	counter++;
	
} while (counter < 3);    // Notice the semicolon

/*
Output:
Counter value: 0
Counter value: 1
Counter value: 2
*/
```

Notes:
- Any variables used in the `do while` boolean expression must be defined **before the while condition is evaluated**.

### `while` vs `do-while`

Let's compare the `do-while` loop above with a version using a regular `while` loop:

```csharp
int counter = 0; 

while (counter < 3) {    // No semicolumn used
	Console.WriteLine($"Counter value: {counter}");
	counter++;
}

/*
Output:
Counter value: 0
Counter value: 1
Counter value: 2
*/
```

When using counters and iterators, both loops produce the same result.

However, when creating menus or validating user input, the `do-while` loop offers real advantages. 

### Creating Menus

The `do-while` loop is excellent for creating menu choices. 

Consider the pseudo code below: 

```text
int menuChoice
do
{
	print "Main Menu"
	print "1. option one"
	print "2. option two"
	print "3. option three"
	print "4. Quit Menu"
	
	print "please enter choice"
	input menuChoice
	
	if (menuChoice == 1) {
		code for option 1
	}
	else if (menuChoice == 2) {
		code for option 2
	}
	else{
		code for option 3
	}
}
// QUIT
while (menuChoice !=4);
```

This menu system will keep looping offering the user choices and doing the choices until the user chooses 4, when the menu system stops.


### Validating User Input

Do while loop is particularly useful when validating user input.

Consider the case where we want the user to provide an integer input between 4 and 9 (inclusive). If they provide the wrong input, the program will ask again until they've provided a valid input.

**Remember:** *A `do-while loop` checks the `condition` AFTER the code block has been executed!*

```csharp
int inputNumber;
const int MIN_NUM = 4;
const int MAX_NUM = 9;

do
{
	Console.Write($"Enter a number between {MIN_NUM} and {MAX_NUM} inclusive: ");
	// Never define a variable inside a loop if you need it to be
	// accessible outside of the loop (scoping limiations are covered later)
	inputNumber = int.Parse(Console.ReadLine());
	
	// error message if invalid input
	if (yourNumber < MIN_NUM || yourNumber > MAX_NUM) {
	    Console.WriteLine("Please read instructions carefully!!!")
	}
}

// validation: loop as long as input is not in allowed range
while (yourNumber < MIN_NUM || yourNumber > MAX_NUM);

Console.WriteLine("Yes, you have typed in a valid number: " + inputNumber);

// keep the console window open until the user hits "return" key
Console.ReadLine();
```




## Exercises

1. Rewrite the code from lab 3 using a `do-while` loop instead of a regular `while` loop.

