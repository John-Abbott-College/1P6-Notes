
# Change Looping Behaviour 

## `break` and `continue` 

`break` is a reserved word - it means get out of your CURRENT LOOP - exit it immediately, do not test any conditions, get out NOW - but only of your current loop. 

> If you are on a ferris wheel, and it breaks, there is no going down to the bottom of the ride and exiting normally.  You are going to have to jump off the wheel.  It is up to the designer of this wheel (loop) to ensure that there will be no unwanted consequences for not completing the loop.  
>
> You do NOT go back onto the ride!

`continue` means - jump immediately to the end of your CURRENT LOOP and test whether you iterate again or not. In other words - stop what you're doing, and jump immediately to the border guard who will verify and see if you can go back and start the loop again. 

> If you are on a ferris wheel and it stops for some reason, and you are inpatient, you can always jump off, and get back on again once you are on the ground.  You *continue* to enjoy your ride.

`break` and `continue` are two commands that are used in loops.  They must be ‘protected’ by an if statement within the loop otherwise they serve no purpose.  Some programmers frown upon their usage and see these as techniques for “patch code” 

*summary*

`break`: this will unconditionally break you out of your **current loop only** - not all your loops. 

`continue`: this will cause you to jump to the **“}” end of your current loop**, and possibly iterate the loop once more or not. 

> Note that the `break` is also used in the switch statement. 

**example**: 

 ```csharp
 int x = 0;
 while (x < 10)
 {
   x++;
   if (x == 5)
   {
     // I hate five, so I want abort the entire darn thing...
     break;
   }
   Console.Write(x + ' ')
 }
 ```

*Output*

```
1 2 3 4
```

**BE CAREFUL** - it throws you out of the loop - not out of the "if" statement. The end of the `if` statement and the end of the `while loop` are both `}`.  It can be confusing.

Some people add comments after a closing `}` indicating what block of text it is referring to.

*Example* 

```csharp
   } // if x == 5
     Console.Write(x + ' ')
} // while x<10
```

 **example**

```csharp
 int x = 0;
 while (x < 10)
 {
   x++;
   if (x == 5)
   {
     // I dislike five, so I want to skip over it
     continue;
   } // if x == 5
   Console.Write(x + ' ')
 } // while x < 10
```

*Output*

```
1 2 3 4 6 7 8 9 10
```

**Example**

```csharp
for (int w=0; w<100; w++) 
{
  // do some code
  break;							// this line will always execute, exiting the loop
  score = score + 20; // this code will never execute
  lives--;						// this code will never execute
}
```

This is why the `break` (or `continue`) should be 'protected' inside the loop with an if statement. 

For example: 

```csharp
while (lives > 0) 
{
  // code here
  // code here
  if (bullets <= 0) {
    break;	// this is ok, because the break is protected by the 'if' statement
  }
  difficulty++;
  score++;
}
```

### Common uses for `break`

Stop looping once you get the information that you want

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

Bailing out when the data you are getting makes no sense

```csharp
for (int i=0; i<10000; i++) {
  x = read_data_from_some_file();
  if (! check_data_makes_sense(x)) {
    Console.WriteLine("ERROR: Cannot parse your file");
    break;
  }
  // more code
}
```
After a simple test, you know your data does not need further processing.

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

### Common uses for `continue`

Getting rid of bad input, but still continuing with your processing

```csharp
for (int i=0; i<10000; i++) {
  x = read_data_from_some_file();
  if (! check_data_makes_sense(x)) {
    Console.WriteLine("ERROR: invalid data point");
    continue;
  }
  // more code
  // ... continue processing the file
}
```
Keep looping until you get the information that you want

```csharp
while (true) {
  Console.Write("Guess my name: ");
  guess = Console.Readline();
  if (guess != SECRET_NAME) {
    ConsoleWriteLine("Nope, still haven't guessed it")
    continue
  }
  // you are so smart :)
  // more code
}
```

