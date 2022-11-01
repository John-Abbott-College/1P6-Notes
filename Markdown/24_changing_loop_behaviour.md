
# break & continue: changing Looping Behaviour

It's possible to change the normal behaviour of a loop with the `break` and `continue` keywords.

## `break`

> `break` is a reserved keyword used to **break out of the current code path**.
> - Typically used with loops.
 >- It will exit immediately, regardless of any test conditions.
 >- Flow breaks for the **current loop only** - not all loops. 


```csharp
for(int i = 0; i <= 5; i++)  // Should print 0 to 5
{
	if (i == 3)
	{
		break;  // breaking the loop when i = 3
	}
	Console.Write(i + " ");
}
```

*Output*

```
0 1 2
```

**Notes**
- The `break` throws you **out of the loop, not out of the `if-statement`**.

 `break` is also used in the switch statement to break out of the case block.

```csharp
string color = Console.ReadLine();
switch(color) 
{
    case "blue":
        // code block
        break;
    case "red":
        // code block
        break;
    default:
        // code block
        break;
}
```
 

Both the `if` statement and the `for-loop`  end with  `}` (curly brace), which can be confusing.
Therefore, some it's common to add comments after a closing `}` (curly brace) describing which code block it is referring to.

*Example* 
```csharp
for(int i = 0; i <= 5; i++)
{
	if (i == 3)
	{
		break;
	}  // if i == 5
	Console.Write(i + " ");
}  // for i<=5
```

### Ferris wheel analogy

![Ferris wheel in the Olp Port of Montreal](https://images.thestar.com/0KQN3FYjuDF7UEVX4E5dybdEuf4=/480x270/smart/filters:cb(2700061000)/https://www.thestar.com/content/dam/thestar/life/travel/2017/11/10/montreals-new-waterfront-ferris-wheel-affords-great-view-for-a-price/ferris_wheel5.jpg ":size=300")
*Source: [The Toronto Star](https://www.thestar.com/life/travel/2017/11/10/montreals-new-waterfront-ferris-wheel-affords-great-view-for-a-price.html)*

Imagine that you are on a ferris wheel, and it breaks. Unfortunately, the wheel will not complete its regular loop so that you can exiting normally.
You are going to have to exit the wheel "as is".  It is up to the designer of this wheel (loop) to ensure that there will be no unwanted consequences for not completing the loop.  

## `continue`

The keyword `continue` causes the code to:
- **Skip the current loop iteration** and go back to **checking the looping condition.**
- If the looping condition is still valid, the code **will loop again**.

In other words - stop what the loop is  doing, and jump immediately to the beginning of the loop. 

```csharp
for(int i = 0; i <= 5; i++)
{
	if (i == 3)
	{
		continue;  // Will skip i == 3
	}
	Console.Write(i + " ");
}
```

*Output*

```
0 1 2 4 5  // missing 3!
```


## Guarded by ifs

`break` and `continue` must be ‘guarded’ by an if statement within the loop otherwise they apply to every single loop iteration and have no real benefits.

Some programmers frown upon their usage and see these as techniques for “patch code” 

**Bad use of break**

```csharp
for (int w=0; w<100; w++) 
{
  // do some code
  break;              // break will always execute, exiting the loop
  score = score + 20; // this line and below will never execute
  lives--;
}
```

This is why the `break` (or `continue`) should be 'protected' inside the loop with an if statement. 

For example: 

```csharp
while (lives > 0) 
{
	// assume code here
	if (enemies == 0) {
	    break;	// ok, break is protected by the 'if' statement
	}
	difficulty++;
	score++;
}
```


## Common uses for `break`

1. Stop looping once you get the information that you want:

```csharp
while (true) {
  Console.Write("Guess my name: ");
  guess = Console.Readline();
  if (guess == SECRET_NAME) {
    break
  }
  ConsoleWriteLine("Nope, still haven't guessed it")
}
```

2. Bailing out when the data received makes no sense:

```csharp
for (int i=0; i<100; i++) {
	x = read_data_fromfile();
  
	if (! validate_data(x)) {
		Console.WriteLine("ERROR: Cannot parse your file");
		break;
	}
// more code
}
```

3. After a test, once it's clear that data does not need further processing.

```csharp
Console.WriteLine("Prime numbers between 1 and 100");
for (int i = 1; i < 100; i++)
{
  bool prime = true;
  for (int j=2; j<= Convert.ToInt32(i/2); j++)
  {
    if (i%j == 0)
    {
      prime = false;
      // no need to test further, it is not a prime number
      break; // break out of the 'j' loop
    }
  }
  if (prime)
  {
    Console.WriteLine(i);
  }
}

```

## Common uses for `continue`

1. Getting rid of bad input, but still continuing with processing

```csharp
for (int i=0; i<100; i++) {
	x = read_data_fromfile();
  
	if (! validate_data(x)) {
		Console.WriteLine("ERROR: invalid data point");
		continue;  // continue processing the file
	}
// more code
}
```

2. Keep looping until you get the information that you want

```csharp
while (true) {
	Console.Write("Guess my name: ");
	guess = Console.Readline();

	if (guess != SECRET_NAME) {
	    ConsoleWriteLine("Nope, still haven't guessed it")
	continue
	}
  // more code
}
```


## Exercises

1. Write a loop using the `break` keyword in order to calculate the average of multiple numeric inputs:
	- Continuously collect a number from the user (assume only valid numbers are entered).
	- Add all entered numbers to an accumulator and keep track of how many numbers are added.
	- Once the user enters the word "stop", output the average of all numbers previously entered.
