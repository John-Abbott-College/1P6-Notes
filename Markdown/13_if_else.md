
# If Statements Pt.2

* if your "True” section (`if block`) contains only one line of code, you do not need the opening and closing brace bracket. This rule applies only when there is one line of code. If you add a second line of code, braces are mandatory 

## Bad Examples


**Example of _BAD_ coding style**

```csharp
if (a < b ) 
  	Console.WriteLine( "yes" );
  	Console.WriteLine( "hello world" );
Console.WriteLine("All done!")
```

*Why?*

* Because of the way we have indented the code, it appears as if the `if block`  are lines `2` and `3`.  BUT... because there are no squiggly braces, the actual `if block`  is just line 2.

If the code was properly formatted, it should look like:
```csharp
if (a < b ) 
  	Console.WriteLine( "yes" );
Console.WriteLine( "hello world" );
Console.WriteLine("All done!")
```

But this is still not good?

*Why?*

* Although this is still syntatically correct, it is not unusual to add statements to the `if block`.  The programmer may not notice that there are no squiggly braces, and inadvertently create a bug

* after the programmer adds a new line, thinking that it will work as expected, but in fact will not.

```csharp
if (a < b ) 
  	Console.WriteLine( "yes" );
  	Console.WriteLine( "eh is less than bee" );   // #### NOT part of "if block"
Console.WriteLine( "hello world" );
Console.WriteLine("All done!")
```

**Example of good coding style**

Even if there is only *one* line of code in your `true` block, **_always_** use braces!!!

```csharp
if (a < b ) 
{
  	Console.WriteLine( "yes" );
}
Console.WriteLine( "hello world" );
Console.WriteLine("All done!")
```

Now, when the programmer adds something to the `if` block, it will be correct.

```csharp 
if (a < b ) 
{
  	Console.WriteLine( "yes" );
  	Console.WriteLine( "eh is less than bee" );   // #### IS part of "if block"
}
Console.WriteLine( "hello world" );
Console.WriteLine("All done!")
```



**A different coding style **

Some people (me) like to keep the openning squiggly on the same line as the `if` statement.  However, Visual Studio keeps undoing my format.  Oh well.

```csharp
if (a < b ) {   // Open brace on same line as if statement
  	Console.WriteLine( "yes" );
  	Console.WriteLine( "eh is less than bee" );
}
Console.WriteLine( "hello world" );
Console.WriteLine("All done!")
```



### Common Syntax Errors

```csharp
if (a < b ) 
		x = 3;  				// **** Now the if block is this line
{   
  	Console.WriteLine( "yes" );										// Not the if block!
  	Console.WriteLine( "eh is less than bee" );   // Not the if block!
}
Console.WriteLine( "hello world" );
Console.WriteLine("All done!")
```



```csharp
// This one is a VERY common error
if (a < b ) ;	// Added a semi-colon after the "if"
{
  	Console.WriteLine( "yes" );
  	Console.WriteLine( "eh is less than bee" );   
}
Console.WriteLine( "hello world" );
Console.WriteLine("All done!")
```

So why is the above code an error?  

* The extra semicolon indicates the end of a line of code
* Even though there is no code, it still indicates that there was a line of code
* if there is a line of code immediately following an `if` condition, then it becomes the `if block`.
* So finally, we have an empty line of code that is part of the `if` block.  So even if the `if condition` is true, the empty line of code will be executed (in other words, nothing will happen)

```csharp
// This one is a VERY common error, but at least it will not compile :)
if (a = b ) 	// NOT comparing a to b, but setting a equal to b,
              // and then testing if a is true
{
  	Console.WriteLine( "yes" );
  	Console.WriteLine( "eh is less than bee" );   
}
Console.WriteLine( "hello world" );
Console.WriteLine("All done!")
```



So if lives is less than 0 I will see: *you died, better luck next time*, and  *Thank you for playing* 

If lives is greater than zero I will see *you made it*, *you are still alive*, and  *Thank you for playing*. 

 

We could also rephrase the question from `lives <=0` to `lives > 0`.

```csharp

if (lives >0) 
{ 
		Console.WriteLine("you made it"); 
		Console.WriteLine("you are still alive"); 
} 
else 
{ 
		Console.WriteLine("you died"); 
		Console.WriteLine("better luck next time"); 
} 

// The line of code below is independent of the if statement and will 
// ALWAYS be run 
Console.WriteLine ("Thank you for playing"); 
```

What if there was not an `else part`.  What would I see? 

```csharp
if (lives >0) 
{ 
	Console.WriteLine("good going!"); 
	Console.WriteLine("keep it up"); 
} 

// The line of code below is independent of the if statement and will 
// ALWAYS be run 
Console.WriteLine ("Thank you for playing"); 
```


What if lives was zero - what would you see? Well, the condition is FALSE so I would NOT do the true part. I would look for an else. Uh oh there is not else, so I just do nothing and simply do NOT do the true part. So I would see: "Thank you for playing" 

> Remember : after your condition the FIRST part is ALWAYS the TRUE part - It is MANDATORY. The second optional else part is FALSE - if it exists. 

 

### Common Syntax Error

```csharp
if (lives >0) 
{ 
		Console.WriteLine("you made it"); 
		Console.WriteLine("you are still alive"); 
} 
else 
		Console.WriteLine("you died"); 			// This is the "else" block
{ 
		Console.WriteLine("better luck next time"); // this is NOT the "else" block
} 

// The line of code below is independent of the if statement and will 
// ALWAYS be run 
Console.WriteLine ("Thank you for playing"); 
```



## Nesting if statements

Within a `code block`, any `code block`, we can add another `if` or `if - else` statement.

It is not too difficult to see what is going on, as long as align your code correctly!

```csharp
if ( a<b )
{
  	// line of code
  	// line of code
  	if ( lives < 0 )
  	{
    		// line of code
    		// line of code
    		// etc...
  	}
  	// maybe another line of code still part of the TRUE block
  	// maybe more
}
else
{
  	// code here
  	// code here
  	if (score < 10)
  	{
    		// line of code
  	}
  	// maybe line of code here in the false block
}
Console.WriteLine("You will always see this!!!")
```



# In Class Exercise (Food Menu)

Create a flowchart and/or pseudo code to model this: 

Make a restaurant ordering system. 

* Ask the user if they want a hot dog.
*  If they answer yes (they can only buy one), 
  * hot dogs are \$2 each. 
* Next ask them if they want a hamburger. 
* If they answer yes (they can only buy one), 
  * hamburgers are \$3 each. 
* Next ask them if they want a Coke ( you can only buy one Coke), 
  * Coke is $1.50. 
* After they are done ordering I want to see TWO things: 
  * The total amount of their bill (hint hint cough cough…..accumulator?) 
  * The number of products they order (hint hint cough cough…I want you to COUNT the number of items…gee…mmm) 

So your program asks 3 questions: 

Do you want a hot dog? (input yes no) 

Do you want a hamburger (input yes no) 

Do you want a Coke (yes no). 

Now print out answer. 

>  Example of output - the user chose a hamburger and Coke 
>
> Thank you for your order. You ordered two items and your total cost is $4.50 

**Hints and clues** : 

use a counter and accumulator to do this! 

You need three if statements in series - not nested. Print out your totals. 

Consider the following Flowgorithm - 

*Notes*: 

- A string is a group of character together. A string variable holds "words" not numbers. 
  - So if YourAnswer is a string you can do this: 
    - YourAnswer = "anything you type" 
- In the "if" statement - you must use TWO equals signs together to test for equality. Using one will cause a logical error. Using a single equals is an assign. It's a verb! It takes right hand side and puts it into left hand side. A double equals is a TEST only, it does not move/change anything. 
- For now test "yes" lower case. We will learn more combinations of "Y" "Yes" "yES", etc… later…. 

 
