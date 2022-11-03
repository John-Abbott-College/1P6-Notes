# Function Parameters & Arguments

We've already covered functions with return values and functions that receive multiple inputs.
In this lesson we will focus on how functions receive those inputs (aka. arguments.)

## Parameters vs Arguments

Parameters and arguments refer to function inputs. However, they refer to  different stages of using a function:
- Function definition, vs Function call.

**Parameters** are the variables used in the **definition of a function**.

```csharp
// Receices two numbers and returns the first divided by the second.
static double Division(double parameter1, double parameter2)
```

In the function above, `double parameter1` and `double parameter2` are the **two parameters** this function is setup to receive.

**Arguments** are the values passed to the function **when the function is called**.

```csharp
double numberA = 2.0;
double numberB = 3.0;

double result = Division(numberA, numberB);
```

The values of `numberA` and `numberB` are the arguments being passed to the function `Division()`.

> **Important to understand:**
> 
> - Argument names don't need to match parameter names.
> - The variables declared as parameter names exist only inside the function.
> - Parameters and arguments are completely independent of the function return value.

The arguments and parameters listed above would be used together to define and call the function like shown below:

```csharp
internal class Program
{
    private static void Main(string[] args)
    {
        double numberA = 2.0;
        double numberB = 3.0;
        
        double result = Division(numberA, numberB);
    }
    // Receices two numbers and returns the first divided by the second.
    static double Division(double parameter1, double parameter2)
    {
	    // Using typecasting to perform division.
        return paramter1/parameter2
    }
}
```


## Math Functions

To better understand how C# function parameters are received, let's look at math functions.

In High-school, you learned about simple functions such as:

$f(x)=2x^2 + x +1$

In this case, the name of the function is `f` and `x` is the parameter being passed.

It could be re-written as:

$f( \triangle )=2\triangle^2 + \triangle +1$

The function name is still `f`

What is the value of `f(2)` ?

$f(2)=2*2^2 + 2 +1$
$=8 + 2 +1 = 15$

Therefore: `f(2) = 15`

> The symbol inside the brackets as a **placeholder for a real value that will be passed** to the function.
> - In other words: it is a "dummy" variable waiting to be filled in.


### Comparing Math and C# Functions

While a math function has the form of

```csharp
F( x ) = 3x + 2
```

A C# function has the form of:

```csharp
F( parameter ) { 3* parameter + 14 } // return value omitted
```

> A *parameter* is the name of a variable to hold data once it is **passed** to the function.

## Parameter Order

Just like in math functions, **the order of the passed arguments matters.**

#### Parameter Order w/ Math

The math function below has multiple parameters:

`g(x,y) = 3x + 4y` 

The function name is `g` and it has 2 parameters. Passing the arguments `x=5` and `y=2`:

`g(5,2) = 3*(5) + 4*(2)= 23`     

>  It is important to note that `5` goes where `x` was and `2` goes where `y` was. 

`g(2,5) = 3(2) + 4(5) = 26`

**Therefore:**
`g(5,2) != g(2,5)`

#### Parameter Order w/ C\#

The result of the `Division` function (see above) would be very different if the order of the arguments were swapped:

```csharp
// Function definion. 
static double Division(double parameter1, double parameter2)
{
	return paramter1/parameter2
}
```

```csharp
// Function call
double result1 = Division(1, 2);  // result1 = 0.5
double result2 = Division(2, 1);  // result2 = 2.0
```

>**Important**
>The number of arguments must match the number of parameters.
>*(unless using optional parameters, which will be covered later)*

The following will result in error:

```csharp
double result3 = Division(1, 2, 3);  // Error! Too many arguments
```


In order to pass 3 parameters, you need to declare them in the function declaration:

### Example: passing 3 parameters

```csharp
static int myfunc (int a, int b, int c) {
  return 2*c + 4*a + 9*b;
}
```

Evaluate:

```csharp
int answer = myfunc( 1, 3, 5);
// a = 1, b = 3, c = 5
// 2* c + 4* a + 9* b
// 2*(5) + 4*(1) + 9*(3)
// 10 + 4 + 27
// = 41
```


## Order and Types, Not Names

The **order and the types** of the parameters must match with the arguments.
However, their **names are completely independent**.


Consider:

```csharp
static void foo() {
  int a = 1;
  int b = 2;
  int answer = bar(a, b);
  Console.WriteLine("Answer is " + answer);
}

static int bar (int b, int a) {
  return b*2 + a*3;
}
```

The output is:

```text
Answer is 8 // If you can't see why, trace the program
```

Function `bar()` does not cares or knows about the names of the variables holding the arguments passed to it.

In other words, during the function call

```csharp
int answer = bar(a, b);
```

Function `bar()` only sees:

```csharp
bar(1, 2);
```


#### Example: Type Matching

Another example were the variable names change, however, the order and types of variables being passed must match exactly.

```csharp
static void Main() {
  int age = 10;
  double price = 3.4;
  bool isRaining = false;
  
  // age must be an 'int' to match myfunc definition,
  // Likewise, isRaining must 'bool', and price must be 'double'
  myfunc (age, isRaining, price);
}

// return type is VOID, since function returns nothing,
// it has nothing to do with what parameters are defined.
static void myfunc (int intVar, bool boolVar, double doubleVar) {
  int localVar;
  localVar = intVar* 2;
  // more code here
} // end of void myfunc
```


## Summary

1. Order of the parameters must match the order of the arguments.
	* The function call must use the correct number of arguments, their types, and order.

2. When a function receives arguments:
	- A function receives arguments into its parameters.
	- Parameters names are independent of argument names, they don't need to match.


## Exercises

1. Evaluate the following function calls

```csharp
// Function definition
static int mycrazy (int i, int j, int k)
{
	return (k + i) * 2 + j;
}
```

```csharp
// Function calls
int answer;
answer = mycrazy(2,2,2);
answer = mycrazy(1,2,3);
answer = mycrazy(3,2,1):
```

2. Re-evaluate the same function as above with the following change (function body remains the same):

```csharp
// Function definition
static int mycrazy (int j, int i, int k) {
	// Same function body
}
```


3. For each code snipped below, determine the output without running the code (trace the code). Only after coming up with an answer, run the code to see if you were correct.

	- If you got the wrong answer, use the **debugger** to step through the code to see where you went wrong.

*Program 1*
```csharp
static void Main(string[] args) {
  int a = 2, b = 3, c = 4;
  snowing (a, b, c);
  snowing (c, b, b);
  snowing (a, c, a);
}

static void snowing (int r, int grapes, int g) {
  int mylocal;
  mylocal = (r + grapes) * g;
  Console.WriteLine("You passed in " + r + " and " + grapes + "and" + g);
  Console.WriteLine("Your output is: " + mylocal);
}
```

*Program 2*
```csharp
static void Main(string[] args)
{
    int x = 2, y = 4, z = 7;
    double a = 0, b = 0;

    a = crazy(z, y, y);
    b = crazy(y, x, z) + crazy(x, y, z);
    Console.WriteLine("I see 'a' as " + a + " and 'b' as " + b);
}

static double crazy (int y, int x, int z)
{
    double mylocal;
    mylocal = x - y;
    mylocal *= 2;
    mylocal += z;
    return mylocal;
}
```

*Program 3*
```csharp
static void Main() {
  int a = 5, b = 4, c = 9; 
  a = addemup(b, c, c); 
  c = a + addemup(a, c, b); 
  b = addemup(a, a, a) + b; 
  Console.WriteLine("a = " + a + " b = " + b + " c = " + c); 
  Console.ReadKey(); 
} // end of Main

       static int addemup (int da, int db, int dc) 
       { 
	int anothervar; 
  anothervar = (da * 2) + db - dc; 
  // more code here 
            return anothervar; 
       } // end of void myfunc 
```


4. Below are 3 function calls without a function definition. Write the implementation of each function so that they can be called from your `Main` program.
	- You will have to deduce the functionality from the function name and how it's being used.

- `a = multiply(n1, n2);` 
- `biggernum = findbiggest(n1,n2);` 
- `exp = pow(4,2);` 

