NOTE: Copied stuff from day 17 which we did not get to in class



# Coding in C# Review

This is for review only, we will not be going over this stuff in class.

## Visual Studio

VS creates **solutions**, which can contain one or more **projects**. In this semester, you should never have more than one project in a solution.

* **solutions** should be for Console Applications
* VS creates a **solution** file, which contains the directories and other information about all the projects in the solution, *therefore*
  * Do NOT change the filenames or directory names once you have created a solution.  You can move the entire directory to someplace else, but do not change any name within that directory.  NEVER!
* VS will create a **project** file for every project (a single project will create an executable).  This file contains information about some of your preferences, and also file structure
  * Do NOT modify the project file by hand.  NEVER!
* You can change the name of your **program.cs** file, if you do it within the VS environment.

# C# - Declaration of Variables

**Examples**

```csharp
Int32 apples; // declaration lines end with semicolon; 
apples = 10; // you CAN do the above on one line 

// yes you can do define & declare ONCE together. 
Int32 apples = 10; 

// you can declare multiple variables at the same time like this: 
Int 32 a,b,c; // you separate with commas; 

// you can declare & define on the declaration line 
Int32 d,e=5, f, g=9;  // separate by commas
 
// pay very close attention to the comma between f and g 
// what if you accidentally put a semicolon in there? 
Int32 d,e=5, f; g=9;  // Assumes the end of command after 'f',
                      // so g=9; is a new command.
                      // but 'g' is not defined, so we have error

```

**more examples**

```csharp
Int32 p,q,r; // yes you can do this 

// you can set multiple variables with one assignment 
p=q=r=0; // yes this is legal - one value 
// goes from rigth to left (r=0, q=r, p=q)

// Or you could do it this way: 
Int32 p=0, q=0, r=0;   // declare & define one line 
 
```

**even more examples**

Do you see the error in the statement below? 

```csharp
int grapes = 4, bubbles = 3; 
bubbles ++; 
grapes = bubbles + 3; 

int bubbles = grapes + 1; // error notice how int is recreating 
// bubbles has already been defined, you are redefining

int newvar = grapes + 3; // this is okay - as long as grapes is 
// declared and defined. 

```

# C# - Writing to the Console

```csharp
namespace myClassDemo
{
  class Program
  {
    static void Main(string[] args)
    {
      Console.WriteLine("hello world"); // this prints to the terminal
      Console.ReadLine();								// this reads from the terminal
    }
  }
}
```

### How do you print out variables? 

```csharp
 Console.WriteLine("Hello the value of bubbles = “ + bubbles + “ Wow!")
```

String literals: enclosed in double quotes, written 'as is' to the terminal, including all the spaces

* `"Hello the value of bubbles = "`

* `" Wow!"`

Variables: the value of the variable (converted to a string) is printed to the screen

* `bubbles`

Putting it together: 

* concatenation operator `+`.  Spaces around the `+` have no effect.

**Examples**

```csharp
int grapes = 4, bubbles = 3; // declare define
Console.WriteLine("Hello the value of bubbles = " + bubbles + " Wow!");
Console.WriteLine("This will cause an error " + ); // expecting something after the +
Console.WriteLine("This will be an error = " + bubbles  " Wow!"); // missing '+'
Console.WriteLine("What do you see here? bubbles = bubbles" + " Wow!");
```

### Difference Between `Console.Write()` and `Console.WriteLine()`

`Console.WriteLine()` does the *write* and then moves to the next line. `Console.Write()` will do the write but *wait on the same line*.  Notice in the run below there is a blinking cursor after `Whassup` because did a `Console.Write()` and if I was to do any more *writes* it would appear on the same line.  Remember - the computer is a ROBOT and will do EXACTLY what you tell it to do.  Literally.  So be careful with `Write()` and `WriteLine` - **know the difference**.

```csharp
Console.WriteLine("hello");
Console.Write("Bonjour!");
Console.Write("Hola");
Console.WriteLine("Ciao");
Console.Write("Whatssup");
Console.ReadLine(); // Waiting for user input
```

*Result*

![Output from above coding, showing the cursor immediately after the string "Whatssup"](/Users/compsci/workspace/JAC/1P6/Images/17_writeline.png)

```text
hello
Bonjour!HolaCiao
Whatssup
```

# C# - Reading from the Console

```csharp
namespace MyClassDemo
{
  class Program 
  {
    static void Main(string [] args)
    {
      String yourname;
      Console.Write("What is your name? ");
      yourname = Console.ReadLine();
      Console.WriteLine("Hello " + yourname + ", welcome to C#");
      Console.ReadLine();
    }
  }
}
```

*Result* 

```text
What is your name? Sandy
Hello Sandy, welcome to C#
```

### Reading non-strings from console

To read Int32 or other numeric (non-String) types, things get a little bit more tricky 

```csharp
Int32 yourscore; 
String yourname; 

yourname = Console.ReadLine(); // no problem for String types 
yourscore = Convert.ToInt32(Console.ReadLine()); 

// the .ToInt32 above can be ToInt16 …. or any other type 

```

Make sure to use `Convert.To`*`XXXXXX`*`(Console.ReadLine());` 
where *`XXXXXX`* is the type of variable that you are inputting.

> NOTE: in previous notes, i used `int.Parse()` and `double.Parse()`.  Either way is fine.



**Example**

```csharp
namespace MyClassDemo
{
    class MainClass
    {
        public static void Main(string[] args)
        {
            Double temperature;     // Double is a real number
          	Console.Write("What is the temperature? ")
          	// since temperature is a 'Double', we need to 
          	// convert to a double
            temperature = Convert.ToDouble(Console.ReadLine());
            Console.WriteLine("It is " + temperature + " degrees ");
            Console.ReadLine(); 
        }
    }
}

```

*Result*

```text
What is the temperature? 21
It is 21 degrees 
```



**Why do we need to convert?** 

**Answer**

> Anything that comes from Console.ReadLine() is treated incoming as a String.
>
> So if you want to input a number, say 21, then it is coming in as a `string` "21".
>
> To use it as a number (example `tempurature++`), we need to convert from a `string` to a `Double`.

Anything that comes in from ReadLine is a String - if you want to use/treat it as a number (ie. Doing math on it) you must Convert it 

# For Loop in C#

For loops are best used when you already know a finite number of times you want to do a loop. 

Example - print 10 aliens across the screen.  Print 3 rows - these are discrete known numbers. 

For loops are not really that useful in the heart of gaming because we "do something - until something else happens" - this is not a known fixed amount or quantity. 

### Syntax

`for (`*`initialize`*` ; `*`condition`*` ; `*`recurring`*) { `code` }

Where the 

* `initialize` is code that gets executed before the loop begins. 
  *  Must be a single statement (i.e. `i = 0;` ok!, `i=0;k=1;` NOT ok!, `i=k=0;` ok!)
* `condition` is used to check when to end the loop (ends if false)
* `recurring` is code that is executed at the end of every loop
  * Must be a single statement
* `code` is the code that gets executed for every loop
  * Is a code block, so as many statements as you want

![Flowchart of a `for loop`. On the printed figure, box 'a' is "i=0", box 'b' is "i<10", box 'c' is "i++", box 'd' is "code"](/Users/compsci/workspace/JAC/1P6/Images/17_for_loop_deconstructed.png)

#### Most common usage

* `initialize`: set a counter to zero, *e.g.* `int i = 0`
* `condition`: set max number of iterations, *e.g.* `i < 10`
* `recurring`: increment the counter, *e.g.* `i++`

**Example**

```csharp
// This is the most common style of a for loop

for (int i=0; i<10; i++) {
  // do some stuff
  Console.WriteLine("i = " + i);
}

// another common style
int j;
for (j = 0; j < 10; j++) {
  Console.WriteLine("j = " + j);
}
Console.WriteLine("Final j value is: " + j);
```

> **Note** that your controlling variable `i` is being controlled entirely by the for loop it is NOT RECOMMENDED that you go `i++` in your loop or alter the variable i. 
>
> You can USE the variable `i`, but do not alter it. Let the for loop do its magic for you.

>  **Note** by declaring `i` inside the for loop (`int i = 0`), the variable `i` is only available to code inside of the if loop, not outside (this refers to `scope` which we will talk about later.)



You can also use for loops in a decreasing manner - like this: 

```csharp
for (int apples = 10; apples > 6 ; apples --) 
{ 
		Console.WriteLine("hello"); 
} 
```

*Question*: How many times is 'hello' printed?

> **NOTE** Always make sure that your loop will end eventually. 
>
> * If you are `decrementing`, then usually your condition will be a `greater than`
> * If you are `incrementing`, then usually your condition will be a `less than`

### Bad examples

**works, but is simply a while loop**

Sometimes you get boneheads at work that leave out parts of the for loop to look cool. Do not do this, even though it would work: 

 ```csharp
int grape = 0; 
// in the for loop, we have no initializer, and no recurring code
// notice that we still need two semi-colons?
for ( ; grape < 3; ) 
{ 
		Console.WriteLine("hello"); 
  	grape ++; 
} 
 ```

The above is awful style. You're using your for loop as if it is a while loop. Do not do this!!! It is not healthy. But……it does work. 



**infinite loop**

Yes, sometimes you see this at work. 

 ```csharp
// there is no initialize, no condition, and no recurring code.
// this is an infinite loop.
// somewhere in the for loop you need to kick me out of this loop (e.g. via 'break')
for (;;) 
{ 
  // bla bla 
  // bla 
}
 ```

### Exercises

**Class Exercise**: Print 10 20 30 40 50 on the screen using a for loop. 

**Class Exercise**: Print the even numbers between 24 and 38 inclusive 

 No you don't have to hand it in. Yes you should be able to do it. Yes, the answers to these are on the next page. 

 Remember - there are many ways of doing this exercise. Your ways may be different than mine. Test your ways, make sure they do what is required. 

# Previous Exercises 

**do if you have time... do anyway! its good for you to practice!**

#### 4) Investment Earnings

The goal of this program is to calculate your investments earnings over a period of a number of years.

**Inputs**: 

* amount of money to invest
* the yearly interest rate 
* the number of years that you want to keep your investment

**Outputs**:

* The month, and the current investment total

**Need to know**:

* To calculate the interest earned for a given month:

$$
interest = current\_total \times \frac{yearly\_interest\_rate}{12\times100}
$$

`interest` = `current_total` * `yearly_interest_rate`/`12.0`/`100.0`

You need to do this calculation month by month (hint, while loop)

#### Optional Requirements

* Tidy up the output by limiting rounding the total money to the nearest penny
* Only output the total money for each year (instead of by each month)

#### 5) CREDIT CARD PAYMENTS

Assume you owe money to a credit card company.

* You can pay your bill all at once, or you can pay anything you want as long as it is equal to or greater than the minimum payment shown on your bill.
* How much does it end up costing you in interest if you only pay the minimum amount per month?
* How much does it end up costing you if you pay a minumum of `x` dollars?

Write a program that will answer these questions

**Inputs**

Assume that user enters valid numbers (i.e. you do not have to verify that the user typed a valid `float`, just assume that they did)

* How much money do you owe?
* What is the yearly interest rate? (NB: in Canada, it varies between 10-18%)
* What is the minimum amount that you can per month (Note that if this is less than what the credit card company calculates, you will have to pay what the credit card company says)

**Outputs**

Month by month:

* Current balance

* Interest

* Payment (the greater of the credit card minimum balance and the minimum balance that the user specified)

* New Balance

Summary:

* The number of years (approx) it takes to pay off your debt
* The total amount paid
* The total amount of interest paid

**Need to Know**

> You will need to find the minimum number between 4 numbers.  You can use `if` statements, are you can google how to find the minimum number in C# (`Math.Min`)

* To calculate interest

$$
interest = balance \times \frac{rate}{12\cdot100}
$$

`interest` = `balance` * `rate` / `12.0` / `100.0`

where 

* `interest` is the interest for this month
* `balance` is the current balance
* `rate` is the yearly interest rate

* To calculate the minimum payment that the credit card company requires:

$$
min\_pay = \min (\frac{fraction}{100} \times (balance + interest), $10, user\_min, balance)
$$

`min_pay` = `Min`(`fraction`/`100.0` * (`balance` + `interest`),  `$10`,  `user_min`,  `balance`)

where 

* `min_pay` is the minimum payment for this month
* `fraction` is the percentage of your balance that needs to be paid (typically 2%)
* `balance` is the current balance
* `interest` is the interest for this month
* `$10` is the minimum that the user must pay, regardless of the balance
* `user_min` is the minimum that the user is willing to pay per month



 