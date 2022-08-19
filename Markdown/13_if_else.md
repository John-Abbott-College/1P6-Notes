# Proper symbol names

[source](https://finallylearn.com/what-are-the-keyboard-symbol-names/)

Note: French names are according to goole translate, and classroom feedback   :)
| Symbol | English | French |
| ---- | ------------------------------- |---|
| [ ]  | brackets, square brackets       |crochets  |
| [    | open bracket                    |parenthèse ouverte |
| ]    | close bracket                   | fermer la parenthèse |
| { }  | braces, curly brackets          |accolades |
| {    | open brace                      |accolade ouverte |
| }    | close brace                     |accolade rapprochée |
| \    | backslash, backward slash       |barre oblique inverse |
| \|   | vertical pipe, pipe             | baree vertical |
| ;    | semicolon                       |point-virgule |
| :    | colon                           |deux points |
| ‘    | apostrophe, prime, single quote |apostrophe, premier, guillemet simple |
| “    | quotation mark, double quotes   |guillemets, guillemets doubles |
| .    | period, decimal, dot            |point, décimal, point |
| /    | slash, forward slash            |barre oblique, barre oblique |
| <>   | angle brackets                  |équerres |
| <    | less than                       |moins de |
| >    | greater than                    |supérieur à |
| `    | back tick, back quote  |tique arrière, citation arrière |
| ~    | tilde                                |tilde |
| !    | exclamation mark, exclamation point  |point d'exclamation |
| @    | at, at sign, at symbol               |Aromas,  à commerciale |
| #    | pound, hash, number                  |Diése |
| ^    | carat                                |carats |
| &    | ampersand                       |esperluette, et commerciale |
| *    | asterisk                             |astérisque |
| (    | open parenthesis, left parenthesis   |parenthèse ouverte, parenthèse gauche |
| )    | close parenthesis, right parenthesis |parenthèse fermante, parenthèse droite |
| ( )  | parentheses, round brackets          |parenthèses |


# Conditionals

## The `if` Statement 

The `if` statement appears in every language. It is extremely important. We use it to alter flow of our program. It is very important to understand that the if statement has a condition - and the answer to this condition is either `TRUE` or `FALSE`. 

The format of and `if statement`  in C# is: 
* **`if (`_`boolean conditional`_` )` _`code block`_**

where: 

* *`boolean conditional`* is anything that evaluates to `true` or `false` 
  * the `boolean conditional` *must* be surrounded by parenthesis `(...)`
* `code block` can either be
  * a single line of code, ending in a semi-colon, *or*
  * multiple lines of code, enclosed in squiggly braces `{ ... }`

Consider the syntax in the following C# code snippet shown below

 ```csharp
 if (score < 100)
 {
 		Console.WriteLine("Keep on trying");
 		Console.WriteLine("You will get it soon");
 }
 Console.WriteLine("Enjoy the game");
 
 ```

So above we assume the variable score is declared and defined. And if score < 100 then we do the two lines of code in the if statement. If it is false, we do NOT do the two lines of code in the if statement. 

Notice that the `Console.WriteLine("Enjoy the Game");` will ALWAYS be run because it is not contingent (or dependent) on the condition of (score <100). 

 **Things to note:**

* `if` is NOT capitalized!

* Remember - your condition must yield a true or false answer. Nothing else. 

  there is no semi-colon after the close squiggly brace (`}`)

* The `true` `code block` is the block of code that *immediately* follows the `if` statement

* Notice that lines `3` and `4` are indented?  This is not required by the compiler, but it *is* required by humans.  Without this clue (via indentation), human readers (programmers, debuggers, etc), will not necessarily realize that there is an code block.

* Visual studio will format your code as you type (indentation), but sometimes if you cut'n'paste code, it can easily get messed up.  In Visual Studio, according to the documentation, the shortcut key is `ALT`+`SHIFT`+`F`

* You should always open and close your if statements with squiggly braces

* Keep bracess aligned - make sure one opens and one closes 

* Indentation is optional but strongly recommended. Keep it pretty!!!! 

  - Braces aligned, code inside the brace brackets indented 

* if your "True” section (`if block`) contains only one line of code, you do not need the opening and closing brace bracket. This rule applies only when there is one line of code. If you add a second line of code, braces are mandatory 

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



## The `else` Statement

The `else` cannot live alone. It must be part of an `if statement`. The `else` part of an `if statement` is **OPTIONAL**. 

The format of and `if-else statement`  in C# is: 
`if (`_`boolean conditional`_` )` _`code block`_  **`else` _`code block`_**


- The `else` is part of an `if statement`. It is OPTIONAL 
- An `if statement` can have only one `else` part 
- The `else` is performed if the `condition` is FALSE 
- The `else` cannot ‘be alone’ - it must be part of an `if` with a `TRUE block of code`. Note the `if` *always* has a TRUE part of the code 
- The `else` bracketing rules are the same as mentioned above for the `if block` in the previous section. 
- Note that *either* the first block of code in an `if` is performed when the condition is true OR the second block of code in an if is performed if the condition is false. **NEVER BOTH** 
- Do not put a semicolon after the word `else` 
- don’t put a semicolon after a squiggly brace 
- If you have a line of code that is the same (common) in the TRUE part and FALSE part of an `if`, consider pulling it out of the `if` statement and put it before or after the entire `if statement` 

 **Example**

```csharp
// many lines of code above
if (lives <= 0)
{
  	Console.WriteLine("you died");
  	Console.WriteLine("better luck next time");
}
else
{
  	Console.WriteLine("you made it");
  	Console.WriteLine("you are are still alive");
}
Console.WriteLine("Thank you for playing");
```

> Lines 4 and 5 are executed if the `if` statement is true.  The true block ALWAYS comes first
>
> Lines 9 and 10 are excuted if the `if` statment is false.  The false block ALWAYS comes second
>
> Line 12 will be executed no matter what, because it is outside of both the `if` and `else` code blocks

Notice for the code above which is clear, well written example of an `if statement``:

* the condition `lives <=0` is in ROUND (no-brace) parantheses and has no semicolon
* see how nicely the TRUE and FALSE part are indented the same amount, aligned
* note that "Thank your for playing" will ALWAYS be shown, whether the lives <=0 or not.



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

 
