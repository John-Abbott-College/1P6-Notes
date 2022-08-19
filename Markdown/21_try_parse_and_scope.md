# Try Parse

Up until now, we have assumed when we ask the user for an integer, that the user types an integer.

However, you must always assume that your user is *dumb as a rock* and will not necessarily do what you ask of them.

Consider the following example code, 

```csharp
using System;

namespace ahha
{
    class MainClass
    {
        public static void Main(string[] args)
        {
            int yourNumber;
            Console.Write("Please enter a number: ");
            yourNumber = int.Parse(Console.ReadLine());
            Console.WriteLine("Thank you :)");
         }

    }
}

```

*running the code*

```text
Please enter a number: boo
```

Once the user hits return, a pop-up window comes along, and says

​		**System Format Exception has been thrown**

> **NOTE**: the above is the output from a MAC, running Visual Studio.  It may be different than what a Windows machine will display.

At this point your program stops.  In other words, the user has crashed your program!

### Never EVER let the user crash your program!!!!

So, what do we do?  We use **try parse**. Try Parse will NEVER cause your program to crash.

## Converting a string to an integer

### Syntax

`bool `*`didWork`*` = int.TryParse(`*`string`*`, out  `*`myInteger`*`)`

where

* *`didWork`* is a boolean variable
  * it will be set to true if the computer was able to convert the string to an integer
  * else it will be set to false
* `string` is the string to be converted (it can be a variable containing a string)
* `myInteger` is an integer variable
  * if the computer is able to conver the string to an integer, then `myInteger` will be set to that value
  * else, myInteger will be set to zero!

### Converting, but not testing

We can, if we want, just convert the string into an integer, and not care if it is set to zero if the user types something silly.

**Example**

```csharp
using System;

namespace ahha
{
    class MainClass
    {
        public static void Main(string[] args)
        {
            int yourNumber;
            Console.Write("Please enter a number: ");
            int.TryParse(Console.ReadLine(), out yourNumber);
            Console.WriteLine("Your number is: "+yourNumber);
         }

    }
}
```

```text
Please enter a number: 35
Your number is: 35
```

```text
Please enter a number: boo
Your number is: 0
```

**Example**: Enter a number between 1 and 10

```csharp
int yourNumber = 0;
do
{
   Console.Write("Please enter a number between 1 and 10: ");

   // if this fails, it sets yourNumber to zero, which is
   // outside of the range I wanted, so all is good
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

### Converting, and testing

If the string does not convert to an integer, it will be set to zero.  But sometimes zero is a valid number, and we need to differentiate between someone entering a valid zero, and someone trying to break our program by entering "boo" instead of a number.

Remember that `int.TryParse(...)` return a boolean, `true` if the string can be converted to an integer, and `false` otherwise.

NOTICE that the while loop is checking for `not true`!

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
    Console.WriteLine("\"" + answer + "\" is not a valid integer!");
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



A more concise example, but does not give user feedback.  It may seem like a better solution, but check the output below.  The user may not know what is going on!

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

#### More examples

```csharp
bool isnum;
int b;
Console.Write("Enter an integer ");
// isnum is the success of the operation
// the variable after the reserved work 'out', `b` in this case,
// is where the number will go if it is valid

do 
{
  // isnum will be set to true or false
  isnum = int.TryParse(Console.ReadLine(), out b);

  // if isnum is true, then the computer was able to 
  // parse the input correctly
  if (isnum)
  {
    b = b * 2;
    Console.WriteLine("Twice the number is " + b);
  }
  
  // otherwise, the computer could not parse the input
  else 
  {
    Console.WriteLine("You did not enter a valid integer");
    // program does not crash!
    Console.WriteLine("please try again");
  }
} while ( ! isnum ); // Loops again if `isnum` is false

```

Below is an example that protects against user typing in strings, and it also validates a range 

The program keeps asking the user for their age - protecting against bad input and also validating that their age is between zero and 25. 

So this program will loop forever until you enter an age between zero and 25 

```csharp
using System; 

namespace delme 
{ 
    class Program 
    { 
        static void Main(string[] args) 
        { 
            // Goal - to get the user's age and display it on the screen. 
            // we need 2 variables to do this: 
            // goodnum - which is a boolean - that will tell me if the 
            // user typed in a string  
            // instead of a number. 
            // yourage - which is where the user's input will go. 
            Boolean goodnum; 
            int yourage; 
            do 
            { 
                // the user's input will end up in variable yourage 
                // the TryParse will return a TRUE or a FALSE to goodnum. 
                Console.WriteLine("Enter an age between 0 and 25?"); 
                goodnum = int.TryParse(Console.ReadLine(), out yourage); 

                if (goodnum)     // same as saying ...... if (goodnum == true) 
                { 
                    // the status is true - so the convert to int is good, 
                    // so the user tyed in a number 
                    Console.WriteLine("You are " + yourage + " years old"); 

                    // if you need it between 0 and 25 years old 
                    if ((yourage < 0) || (yourage > 25)) 
                    { 
                        Console.WriteLine("out of range, try again"); 
												// this will force the loop to iterate again! 
                        goodnum = false;   
                    } 
                } 
                else 
                { 
                    Console.WriteLine("Hey! You typed in a string (or a double)! "); 
                } 

            } while (!goodnum);   // same as   while (goodnum == false); 
            Console.ReadLine();   // to prevent window closure 
        } 
    } 
} 
```

## Convert a string to a double

Same rules as converting a string to an integer

### Syntax

`bool `*`didWork`*` = double.TryParse(`*`string`*`, out  `*`myDouble`*`)`

where

* *`didWork`* is a boolean variable
  * it will be set to true if the computer was able to convert the string to an integer
  * else it will be set to false
* `string` is the string to be converted (it can be a variable containing a string)
* `myDouble` is an double variable
  * if the computer is able to conver the string to an double, then `myDouble` will be set to that value
  * else, myDouble will be set to zero!

### 