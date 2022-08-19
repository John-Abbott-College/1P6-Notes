# Functions That Returns a Value

Imagine that you are at a restaurant.  The cook, who is the person who makes your meal, needs to know what you want to eat (your order).

The cook asks the server to go get your order.  The cook does not care how the server achieves this goal.  The server could be polite, or not, could lie, or not, the cook doesn't care.  The cook assumes that the server will do the job correctly.

Once the server `returns` to the cook, the server gives the cook the information that is needed, i.e., the customer's order.

```csharp
static void cook() {
  Order order; 
  for (i=0; i<NUM_CUSTOMERS; i++) {
    // ask for the server to get the order, save the
    // returned information (value) in variable order
    order = server_gets_order();
    prepare_food();
  }
}

// assume "Order" is a valid data type
static Order server_gets_order() {
  Order myOrder;
  // mystery code
  
  // give this information back to the code that 
  // asked for it.
  // You MUST have a return statement
  return myOrder;
}
```

Things to note:

* a function that returns information is not a `void` function.  The programmer must inform the compiler what type of data will be returned

* If a function is NOT `void`, it **must** have a return statement, where a value, or variable of the correct type is returned

  * ex: in server_gets_order(), you cannot return anything other than an "Order"

* If the calling program (ex: cook) wants to save this information in an assignment statement, the variable used to save the data must be of the appropriate data type

* It is not necessary for the calling program to save the returned value.  It will still be used if necessary

  ```csharp
  if (server_gets_order() == "fries") {...}
  ```

  

## Details

There are a few concepts that are very important to understand 

- Keep your functions outside of your Main. …(for those about to pick up their hands…..yes … I know...but keep in mind this is Programming 1…. you will learn that later in Object Oriented Programming).  Keep them in series, and don’t nest them.  Watch your indentation and bracketing to ensure they open and close properly. 
- **Name your functions uniquely**, and meaningfully. No reserved words, no spaces, no funny characters. **Do not name your functions the same as variable names!!!** 
- know the idea and independence of return values and argument passing (soon) 
- know the difference between pass by reference and pass by copy (soon) 

```csharp
static void Main(string[] args)
{
  int score;
  myfunct(); // this calls the void function
  
  score = anotherfunct();  // whats going on here?
  // we have a function call on the right hand side of an equals!!!
  // it looks like lthe function is "returning something" back to socre!
  // you be the detective: What TYPE do you think anotherfunc will 
  // return?  Tell me this now, without looking down below at the answer.
  Console.ReadLine();
}

static void myfunc()
{
  // bla bla bla
  // code here
}
```

 Before I go further, I see with certainty that `anotherfunc` gives back an `int`, becaut it is going to be saved into the variable `score` (line 6) which declared as an `int`

*So I can deduce that the function called anotherfunc() is a function that returns an Int32. I know this without any further information.*

```csharp
// no I know that anotherfunc must return an int based on the code above, so:

static int anotherfunc()
{
  int localgrapes = 10;
  // code here
  // bla bla bla
  localgrapes++;
  return localgrapes; // this happens on non-void functions
}
```

* Before you end the function, you must return a value of the appropriate type

### Examples

#### Example 1

In a function that returns something - you can "remove the call" and replace it with the return value. 

```csharp
static void Main(string[] args)
{
  int orange=8, blueberry = 10;
  // mynumber() will return the number 9!
  orange = blueberry + mynumber(); // orange = 19
  blueberry = mynumber() + orange;
  mynumber(); // logial error, where is the return value going
  Console.ReadLine();
}

// now I know that mynumber must return an int, because
// on line 4, orange is an int, as is blueberry, and an int
// plus an int is an int, so mynumber must return an int
static int mynumber() {
  int banana = 10;
  // ... code ...
  banana--;
  return banana;
}
```



#### Example 2

How to save the return of  non-void function

```csharp
static void Main(string[] args)
{
  int userinput;
  f1(); // look a the way this is called - 
  			// f1 is all alone on the line.  There is not equals anywhere
  f1(); // f1 is NOT used in an equation or if statement.  It is all alone, void
  
  userinput = gogetit(); 	// aha! something is different than void! 
  												// I am using the function in an equation
  												// the function returns something... what do you think the return type will be?
  Console.WriteLine("I see your number as "+ userinput);
  Console.ReadLine();
}

static int gogetit()
{
  int applepie;
  Console.Write("What is your number? ");
  appliepie = int.Parse(Console.ReadLine());
  return applepie;
}
```

#### Example 3

how to use an `int` function in an equation

```csharp
static void Main(string[] args) 
{
	int result;
  
  // program to add w numbers and print result
  result = gogetit() + gogetit(); // yes, you can use the return value of a function
                                  // inside an equation
  Console.WriteLine("The total of is equal to " + result);
  Console.ReadLine();
}

static void f1() {
  Console.WriteLine("happy");
}

static int gogetit() {
  // here in the function you can decorate with TryParse() and loops and
  // error messages, so that you can call it frome ANYWHERE within your
  // program, and don't have to repeat the code over and over
  int number;
  Console.Write("what is your number? ");
  number = int.Parse(Console.ReadLine());
  return number
}
```



#### Example 4

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
// I am going to write targethit below
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

## Exercise

Create a function that will return a valid integer from the user 

Pseudo code below:

```text
int GetValidInt() 
{
	prompt user for input
	do 
	{
		success = TryParse
	} while not success
	return the number
}
```

With the above code you can use it something like this: 

```csharp
static void areaofrectangle() 
{ 
  int side1, side2; 
  Console.WriteLine ("enter value for side 1"); 
  side1 = GetValidInt(); 
  
  Console.WriteLine("enter value for side 2"); 
  side2 = GetValidInt(); 
  
  // and so on. 
} 
```

 Here we see the beauty of functions - they're re-usable!!!! and you can use them to answer all your questions in Lab #2 

## Summary

Function return values can be just about anything! They are not limited to integers. 

So you can have this: 

 ```csharp
// definition of a Double function 
static Double getprecision() 
{ 
	Double calculatednumber; 
	// bla bla 
	return calculatednumber; 
} 
 ```

Remember: your return type has to match who is receiving it! 

 

**Function return Values** 

A function in C# always returns something - even if that something is nothing….. do I sound like a politician? 

A function that returns nothing is called a void function. This explains why there is no return command before the function closes in a void function.  Remember, the word void is reserved and part of C# language 

You return from your called function back to your caller with nothing in your hands in the case of a void function! So there doesn't have to be a variable to receive this. 

 