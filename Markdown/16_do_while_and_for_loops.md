# Do While & For Loops

## Do While Loop

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

Do while loop is particularly usefull when validating user input.

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


## For loops

For loops are best used when the number of iterations (how many times to loop) is known before hand. 

Example:
	- Print 10 aliens across the screen.
	- Ask the user to provide exactly 4 numbers.

### Syntax

```csharp
for (initialization ; condition ; recurring)
{
	// Code block
}
```

Where:

* `initialization` is code that gets executed before the loop begins. Must be a single statement.
	* Acceptable:
		* `int i = 0;`
		* `int i=0, j=0;`  (declaring and initializing two variables of the same type).
	* Not acceptable:
		* `int i=0;k=1;`

* `condition` is used to check when to end the loop (ends if false)
* `recurring` is code that is executed at the end of every loop. Must be a single statement
* `code block` is the code that gets executed for every loop.


### For Loop Flowchart

![Flowchart of a `for loop`. On the printed figure, box 'a' is "i=0", box 'b' is "i<10", box 'c' is "i++", box 'd' is "code"](../Images/17_for_loop_deconstructed.png)


### Typical For Loop Usage

Below is the most common usage of the for loop:

* `initialize`: set a counter to zero
	* *e.g.* `int i = 0`
* `condition`: set max number of iterations
	* *e.g.* `i < 5`
* `recurring`: increment the counter
	* *e.g.* `i++`

```csharp
// The most common style of a for loop

for (int i=0; i<5; i++) {

  Console.WriteLine("i = " + i);
}

// another common style
int j;
for (j = 0; j < 5; j++) {
  Console.WriteLine("j = " + j);
}
Console.WriteLine("Final j value is: " + j);
```


### Don't modify the iterator

The variable `i` is the **iterator variable** being controlled entirely by the for loop.
It is **not recommended** to modify the iterator `i` inside the loop's code block.

```csharp
for (int i=0; i<5; i++) {

  Console.WriteLine("i = " + i);
  // Not recommended to modify the iterator inside the looop
  i += 2;
}
```

### Iterator availability (scoping)

By declaring `i` inside the for loop initialization (`int i = 0;`), `i` is only available inside the if loop. Trying to access the iterator `i` from outside of the loop will result in an error.

This happens because of **code scope** which will be covered later in the course.

```csharp
for (int i=0; i<5; i++) {

  Console.WriteLine("i = " + i);
}

Console.WriteLine("i = " + i);  // Error! 'i' does not exist outside the loop
```

### Decreasing Loops

For loops can also be iteraed in a decreasing manner:

```csharp
for (int apples = 10; apples > 6 ; apples --) 
{ 
		Console.WriteLine("hello"); 
} 
```

*Question*: How many times is 'hello' printed?

> **NOTE** Always make sure that your the will end eventually. 
>
> * When **decrementing** the loop, the condition is usually  **greater than**.
> * When **incrementing** the loop, the condition is usually **less than**.

### Bad For loop Examples

It's possible to initialize the iterator variable before the loop. However, this will make the for loop harder to read and is not recommended.

 ```csharp
int grape = 0; 
// in the for loop, we have no initializer, and no recurring code
// notice we still need two semi-colons.
for ( ; grape < 3; ) 
{ 
	Console.WriteLine("hello"); 
  	grape ++; 
} 
 ```

The above is **bad style**. The for loop is being used as a while loop.


## Exercises

1. Rewrite the code from lab 3 using a `do-while` loop instead of a regular `while` loop.
2. Print 10 20 30 40 50 on the screen using a for loop.
3. Print the even numbers between 24 and 38 inclusive.

