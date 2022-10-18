# Functions That Returns a Value

## Return values

Up to this point, we've only looked at functions that returned `void`, in other words, they did things in the background but they did not produce any outputs that could be captured or assigned by another variable.

Functions typically **return a value** (produce an output) that can be **assigned** (or "captured") in another variable.

We've been doing this for many weeks now. Consider the following functions below:

- `Console.ReadLine()` is a function that takes **zero arguments** (inputs) and returns a value of type `string`
```csharp
string userInput
// Assigning (aka storing) the returned string to the variable userInput
userInput = Console.ReadLine();
```

- `Convert.ToDouble( )` is a function that takes **one argument** and returns a value of type `double`
```csharp
double wallWidth;
// Assigning the return value to userInput
wallWidth = Convert.ToDouble( userInput );
```

- `int.Parse( )` takes one argument and returns an `int`
```csharp
int gymVisits;
// Assigning the return value to gymVisits
gymVisits = int.Parse( userInput );
```

> Remember that in an **assignment operation**, the **right hand side is evaluated first** and then assigned to the variable on the left.
> 
> This means that the function will:
> 
> 1. receive it's inputs
> 2. run to completion, and then
> 3. return it's output
> 4. the output will be assigned to the variable on the left.


## Defining the Return Values 

In the previous lesson we introduced the general structure of a C# function:

```csharp
static return_type FunctionName(input_type inputA)
{
	// code block
	return variableToReturn;
}
```

Where:

- `static` - Keyword that defines how to reach this function.
- `return_type` - The type of variable that this function will return (provide as it's output).
	- Examples of return types:
		- `int`, `string`, `double`, `bool`
		- `void` - this means that nothing will be returned.
- `FunctionName` - Name of the function. Convention is to user UpperCamelCase.
- `inputA` - An input variable (also called an **argument**) that this function is receiving and will be used inside the function's code block.
- `input_type` - The **data type** of variable  `inputA`.
	- Ex.: `int`, `string`, `double`, `bool`
- `return` - Keyword indicating that the following value will be returned by the function as its **output**.
- `variableToReturn` - Is the value or variable that the function will return (provide) as it's **output**.

> To define a function that returns a value, two conditions must be met:
>
> 1. **The function declaration must specify what kind of data type will be returned.**
> 	1. *(see `return_type` in the structure above)*
> 	2. A function that returns information is not a `void` function.  The programmer must inform the compiler what type of data will be returned (`double` in this example).
> 
> 2. **The function's code block must have at least one `return` statement, which matches the `return_type` specified in step 1.**
> 	1. If a function is NOT `void`, it **must** have a return statement, where a value, or variable of the correct type is returned.
> 	2. If the calling program wants to save this information in an assignment statement, the variable used to save the data must be of the appropriate data type.
> 	3. It is not necessary for the calling program to save the returned value.  It will still be used if necessary.


### Example 1: Sum of Two Numbers

Consider a function that receives two numbers and returns their sum:

- Inputs are two different `double` numbers. 
	- Let's call these input variables `number1` and `number2`
- Output is a single `double` number.

```csharp
static double SumTwoNumbers(double number1, double number2)
{
	// declaring a temporary variable inside the function.
	double result = number1 + number2;
	// returning the result as the function's final output.
	return result
}
```

The function would then be called as follows:

```csharp
double mySum;
mySum = SumTwoNumbers(1.2, 3.4);

Console.Write(mySum);
// Output: 4.6
```

**Notes:**

- The variable `mySum` does not "cares" about what is happening inside `SumTwoNumbers()`, as long as it returns a value of type `double`.

- You can declare new variables inside the function, however, they are not available outside the function unless they are `returned`.


### Example 2: Saving the return value

Below is other example on how to save the return value of a non-void function.

```csharp
static void Main(string[] args)
{
  int userInput;  
  // the function returns an integer which must match the variale "storing" it.
  userinput = GoGetIt();

  Console.WriteLine("I see your number as "+ userinput);
  Console.ReadLine();
}

static int GoGetIt()
{
  int apple;
  Console.Write("What is your number? ");
  apple = int.Parse(Console.ReadLine());
  return apple;
}
```

#### Example 3: No inputs with Output

Here the function is being used multiple times.

```csharp
static void Main(string[] args) 
{
	int result;
  
	// program to add 2 numbers and print result
	result = gogetit() + gogetit(); // yes, you can use the return value of a function
	// inside an equation
	Console.WriteLine("The total of is equal to " + result);
	Console.ReadLine();
}

static int gogetit() {
  int number;
  Console.Write("what is your number? ");
  number = int.Parse(Console.ReadLine());
  return number
}
```


#### Example 4: Boolean Functions

Below is an example of using functions in game programming - note this is a very partial program, it is missing a lot of variables. But look at the boolean function calls to get an idea of what is going on. 

```csharp
static void Main(string[] args)
{
  // some code ...
  do 
  {
    if (targethit()) // using a boolean function call
      // display explosion graphics
      // increase score
      // play sound
      // remove bullet, remove target 
  } while (! gameouver()); // what is the return type of gameover?
}

static Boolean targethit()
{
  Boolean gotit = false;
  if (xship == xbullett && yxhip == ybullet) // need globals for these, etc
  {
    gotit = true;
  }
  return gotit;
}

static Boolean gameover()
{
  Boolean gamedone = false;
  if (gametimer < 0)
  { 
    gamedone = true;
  }
  // another condition for game over
  if (lives < 0) 
  {
    gamedone = true;
  }
  return gamedone;
}
```
