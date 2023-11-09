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

1. Print 10 20 30 40 50 on the screen using a for loop.
2. Print the even numbers between 24 and 38 inclusive.

