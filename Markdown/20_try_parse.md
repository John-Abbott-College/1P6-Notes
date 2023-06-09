> **Announcements**
> - Using `TryParse` is not a requirement of assignment 3, however, an extra 1% will be awarded for **properly using it to validate invalid user input** in the assignment.
> 	- If the criteria for valid input is not explicitly defined for a function in the game, you must decide what is considered as valid and **explain your reasoning using code comments**.
> 	- The final assignment grade cannot exceed 8.5%

# Try Parse

Up until now, we've assumed that when asked, the user provides a valid number.

> However, you must always assume that the user will not necessarily provide a valid input.

Consider the following example:

```csharp
int yourNumber;
Console.Write("Please enter a number: ");

yourNumber = int.Parse(Console.ReadLine());
Console.WriteLine("Thank you :)");
```

*Running the code*
```text
Please enter a number: boo
```

Once the user hits return:

**💥 System.FormatException: Input string was not in a correct format. 💥**

At this point the program crashes and stops. 

> You should **never** allow the user crash your program!

The `TryParse` flow allows us to parse user input but not crash our program.

## String to int with TryParse

**Syntax**

```csharp
string myString = Console.ReadLine();
int myInteger;
bool didWork = int.TryParse(myString, out myInteger);
```

Where:

- `out` is a keyword and must be present (will be covered later in the course, it defines a parameter passed as reference rather by value).
* *`didWork`* is a boolean variable
  * It's **true if** `myString` was successfully parsed to an integer.
  * **otherwise it's false** (aka. parsing failed).
* `myString` is the string to be converted (it can be a variable containing a string)
* `myInteger` is an integer variable
  * if the computer is able to convert the string to an integer, then `myInteger` will be set to that value
  * **otherwise, `myInteger` will be set to zero**.

## Examples

### Ex 1 - Converting, but not testing

It's possible to just convert the string into an integer and not test if `int.TryParse` was successful.
Note that in this case, it's possible that `yourNumber` was set to zero (the default behaviour of `TryParse`)

```csharp
int yourNumber;
Console.Write("Please enter a number: ");

int.TryParse(Console.ReadLine(), out yourNumber);
Console.WriteLine("Your number is: "+yourNumber);
```

```text
Please enter a number: 35
Your number is: 35
```

```text
Please enter a number: boo
Your number is: 0
```

### Ex 2 - Number in a range

Program prompts the user for an number between 1 and 10.

In this example, if parsing fails, `yourNumber` is set to zero, which is outside the desired range and **will be caught by the do-while boolean condition**.

```csharp
int yourNumber = 0;
do
{
   Console.Write("Please enter a number between 1 and 10: ");

   
   int.TryParse(Console.ReadLine(), out yourNumber);
}
while (yourNumber < 1 || yourNumber > 10);

Console.WriteLine("Your number is: " + yourNumber);

```

```text
Please enter a number between 1 and 10: 99
Please enter a number between 1 and 10: -5
Please enter a number between 1 and 10: 5.2
Please enter a number between 1 and 10: boo hoo !
Please enter a number between 1 and 10: 5
Your number is: 5
```

### Ex 3 - Converting, and testing

Remember: **if the string does not convert to an integer, it will be set to zero**.  However, depending on the program, zero might be a valid number.

Therefore, we need to differentiate between the **user entering a valid zero or invalid input**.

`int.TryParse( )` returns a boolean:
- `true` if the string can be converted to an integer, and
- `false` otherwise.

We can write a while loop that checks for `int.TryParse( )` returning `not true`:

```csharp
int yourNumber;
bool itWorked;
do
{
	Console.Write("Please enter a number: ");
	string answer = Console.ReadLine();
	itWorked = int.TryParse(answer, out yourNumber);
	  
	if (!itWorked)
	{
		Console.WriteLine(answer + " is not a valid integer!");
	}
}
while (!itWorked);

Console.WriteLine("Your number is: " + yourNumber);
```

```text
Please enter a number: boo hoo!
"boo hoo!" is not a valid integer!

Please enter a number: 15.0
"15.0" is not a valid integer!

Please enter a number: 15.
"15." is not a valid integer!

Please enter a number: 15
Your number is: 15
```

### Ex 4 - No user feedback (Bad!)

Below is a more concise example, **however, it does not give user feedback**.
It may seem like a better solution, but check the output below.  The user may not know what is going on.

> Always provide helpful feedback if the user should change their input.

```csharp
int yourNumber;
do
{
	Console.Write("Please enter a number: ");
}
while (! int.TryParse(Console.ReadLine(), out yourNumber));

Console.WriteLine("Your number is: " + yourNumber);
```

```text
Please enter a number: boo hoo !
Please enter a number: 15.5
Please enter a number: 15.0
Please enter a number: 15.
Please enter a number: 15
Your number is: 15
```

### Ex 5 - Checking strings & number range

Below is an example that protects against user typing in strings, and it also validates a range 

The program continuously prompts the age - protecting against bad input and also validating that their age is between zero and 25.

```csharp
using System; 
namespace example
{ 
    class Program 
    { 
        static void Main(string[] args) 
        {
            Boolean goodParse; // whether parsing worked or not
            int userAge; 
            do 
            {
                Console.WriteLine("Enter an age between 0 and 25?"); 
                goodParse = int.TryParse(Console.ReadLine(), out userAge); 

                if (goodParse)     // same as if (goodParse == true)
                {                    
                    // validating: between 0 and 25 years old
                    if ((userAge < 0) || (userAge > 25)) 
                    {
                        Console.WriteLine("out of range, try again"); 
                        // Force the loop to iterate again
                        goodParse = false;
                    }
                    else  // validation is ok
                    {
	                    Console.WriteLine("You are " + userAge + " years old");
                    }
                } 
                else   // goodParse is false
                { 
                    Console.WriteLine("Hey! You typed in a string (or a double)! "); 
                } 

            } while (!goodParse);   // same as  while (goodParse == false); 
        } 
    } 
}
```

## Convert a string to a double

Same rules as converting a string to an integer

**Syntax**

`bool `*`didWork`*` = double.TryParse(`*`myString`*`, out  `*`myDouble`*`)`

where:$

* *`didWork`* is a boolean variable
  * it will be set to true if the computer was able to convert the string to an integer
  * else it will be set to false
* `myString` is the string to be converted (it can be a variable containing a string)
* `myDouble` is an double variable
  * if the computer is able to convert the string to an double, then `myDouble` will be set to that value
  * else, `myDouble` will be set to zero!
