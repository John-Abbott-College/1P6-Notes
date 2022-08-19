# Argument Passing

First thing: Argument passing is TOTALLY INDEPENDENT of function return values. They work with or without each other. Sometimes you get a function that has no arguments and a return value, and sometimes not. 

## Definitions

*parameters* - The variables used in the definition of the function

*arguments* - The values passed to the function

i.e. `g(x,y) = 3x + 4y`, `x`, `y` are parameters

`g(5,2)`,  `5`, `2` are arguments used when executing `g`.

## Functions and math

Remember grade 10 math? You did things like this: 

```text
f(x) = 2x^2 + 3x + 1
```

What exactly is `x`?  

What if I re-wrote the above to this

```text
f(w) = 2w^2 + 3w + 1
```

Same?  *yes! the function name is `f`*

What about ?

```text
f(chair) = 2(chair)^2 + 3(chair) + 1
```

So then what is the value of `f(2)`

```text
f(2) = 2(2)^2 = 3(2) + 1
```

It's as if the `2` sat on the chair.

So: `f(2) = 15`

No matter which function definition I use.



You can think of the symbol in the brackets as a placeholder for a real number to sit on. 

It is a "dummy" variable waiting to be filled in. 

So your math teacher might write it this way: 

 `f(x) = 7x + 14` 

I write it as 

 `f( `*`parameter `*`) = 7 * `*` parameter`*`   + 14` 

A *parameter* is the name of a variable to hold data that is *passed* to the function.

Now I can evaluate 

 `f(3) = 35` 

`f(2) = 28` 

### Let’s do some basic math 

Consider this:  `f(x) = 3x +5` 

what is `x`?  

Could it have been re-written `f(w) = 3w + 5` ?

Is this the same function? 

 What is the name of this function? 

Can you think of `x` as a temporary placeholder? 

Why was `x` chosen? 

Could I have chosen the happy face symbol?  Is this the same function? 

`f(😀) = 3😀 + 5`  

#### Example 1

`g(x,y) = 3x + 4y` 

lets send a five and a two to this function 

`g(5,2) = 3(5) + 4(2)= 23`     

Here the function name is `g` and it has 2 parameters

>  It is important to note that `5` goes where `x` was and `2` goes where `y` was. 

`g(2,5) = 3(2) + 4(5) = 26`

**NOTE: `g(5,2) != g(2,5)`**

#### Example 2

`g(x,y) = 3x + 4y` 

`g(10,20) = 3x + 4y`      // the ten and twenty are arguments.  They will sit on the x and y respectively. 

`g(10,20) = 3(10) + 4(20)` 

`g(10,20) = 110` 

**notice that the order matters!** 

**`g(10,20)` is not the same as `g(20,10)` !!!!! **

#### Example 3

`g(x,y) = 3x + 4y` 

`g(3,4,9)` = WHOH! this is an ERROR!!!

Your `g` function is designed to hold 2 arguments, you're trying to pass 3!

## C# Functions

Functions in C# work almost the same way! 

The first thing to understand is argument passing is totally independent of return values - meaning they have nothing to do with one another and are totally separate and independent concepts. 

### Syntax

declare function:

`static `*`return_type function_name `*`(`*`type parameter1, type parameter2, ... `*`)` `{ ... }`

calling the function:

*`function_name`*` ( `*`argument1, argument2, ...`*` )`

where the value of `argument1` will be saved in `parameter1`, `argument2` will be saved in `parameter2` etc, before the code in the function is executed.

**VERY IMPORTANT**

The number of arguments *must* match the number of parameters

> unless there are optional parameters, which we are ignoring at this point



### Example 4

```csharp
static int myfunc (int a, int b, int c) {
  return 2*c + 4*a + 9*b;
}
```

Evaluate:

```csharp
int answer = myfunc( 3, 3, 4);
// NOTICE:
// a = 3, b = 3, c = 4
// 2*(4) + 4*(a) + 9*(3)
```

### Example 5

Order of the parameters and arguments are important, not the name.

Consider:

```csharp
static void foo() {
  int a = 3;
  int b = 7;
  int answer = bar(a, b);
  Console.WriteLine("Answer is " + answer);
}

static int bar (int b, int a) {
  return b*2 + a*3;
}
```

The output is:

```text
Answer is 27
```

Do you understand why?

### Exercise

Evaluate the following:

```csharp
static int mycrazy (int i, int j, int k) { return (k + i) * 2 + j; }
```

```csharp
int answer;
answer = mycrazy(2,2,2); // what is the value of answer?
answer = mycrazy(1,2,3); // what is the value of answer?
answer = mycrazy(4,0,2): // what is the value of answer?
```

What if I changed the order of the parameter in my function definitions?

```csharp
static int mycrazy (int j, int i, int k) { return (k + i) * 2 + j; }
```

Would this change anything?  ABSOLUTELY!

... reevaluate `answer = mycrazy(1,2,3)`, where now `j=1`, `i=2` and `k=3`.

Not the same as before. 

## Rules

* Order of the parameters is very important!
* Order of the arguments is very important!
* When you call a function:
  * The caller must call the function with the correct number and type of arguments

* When a function receives arguments:
  * A function receives arguments into its parameters.  The number and type of parameters must match the incoming arguments.

### Type Matching Example

```csharp
static void Main() {
  int a = 10;
  double b = 3.4;
  bool bignum = false;
  
  // Note that a MUST be an 'int' since that is how it is defined in myfunc,
  // Likewise, 'bignum' must be 'bool', and 'b' must be a 'double'
  myfunc (a, bignum, b);
  Console.ReadKey()
}

// the return type is VOID, because this function does not return anything,
// it has nothing to do with what parameters are defined.
static void myfunc (int da, bool db, double dc) {
  int anothervar;
  anothervar = da* 2;
  // more code here
} // end of void myfunc
```



## Exercises

Without compiling and running the code, determine the output.  Then, *and only then*, run the code to see if you were correct.

If you got the wrong answer, use the **debugger** to step through the code to see where you went wrong.

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

## Write your own Functions

Write the function and a driver program to implement. Each one is separate 

- `a = multiply(n1, n2);` 
- `biggernum = findbiggest(n1,n2);` 
- `exp = pow(4,2);` 

