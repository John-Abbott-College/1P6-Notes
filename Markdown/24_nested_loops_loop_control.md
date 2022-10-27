# Nested Loops

The idea here is to have a loop within a loop - indentation is more important than ever!  

When creating nested loops make sure you clearly understand how many iterations you require and how that variable is increasing or decreasing. Make sure you loop eventually ends! 

Consider printing this out: (`X` is an alien!)

```text
X X X X
X X X X
```

So we have 2 row of aliens, and 4 columns. It is a "2 by 4" matrix or grid. 

 Few things to remember: 

- You love RC Cola ! 
- You remember Greek/Roman architecture with those huge columns 
- you like sitting in row boats 

![A pic of an RC cola can](../Images/24_RC_Cola.png)

What is this insanity? 

 Well RC - means row, then column. R then C. So a 8 by 14 grid is 8R by 14C 

 Thinking of architecture? 

![Roman coleseum](../Images/24_roman_cols.png) 

Look at those beautiful columns, they go *up*/*down*

![Rowboat being rowed, viewed from the top](../Images/24_rowboat.png)

Look at the rowboat, the oars are horizontal... they go from *left*/*right*

**Summary**: 

Rows then columns, columns go up and down, rows go side to side. 

Do not screw this up!

**Pseudo code**

 So to print the above aliens here is what we do (pseudo code): 

```text
for row = 1 to 2 
{ 
	for col = 1 to 4 
	{ 
		print alien;  // do not skip a line 
	} 
	print a new line character; // print only after the columns are printed
} 
```

**Not to do**

Also very important - do not declare the same variable in a loop!!!! this is dangerous - remember you can't give birth to the same named child in a given house: 

```csharp 
for (int i=0; i<10; i++) 
{ 
  int grapes; // BE VERY CAREFULL ABOUT DECLARING INSIDE A LOOP!
  grapes++; 
} 
```

The above is bad for 2 reasons: 

- in this example, you are declaring `grapes` 10 different times! 
- secondly - you're doing `grapes++` on an undefined variable - you're relying on C# to initialize this as zero - unhealthy. 

**Another example**

Below is a sample of what you will do later in ANOTHER COURSE 

- no you don't have to know it for test 2, nor test 3 in this course 
- Warning may contain nuts. 

Later on in programming 2, 3, 4 you may declare variables in a loop! But this is more advanced object oriented programming

**pseudo-code**: 

```csharp
 declare myarray[10] 
 for (int i = 0; i<10; i++) 
 { 
   // the object pointer is stored in an array called myarray
   // instatiates an object of alien class
   // `new` forces the creation of new Alien (sort of like a declaration, but not quite)
 	myarray[i] = new Alien(); 
 } 
```

## Class Exercise

### Exercise 1

Create a chess/checker board. 

 This is a board with 8 rows and 8 columns. Starting with a white square and alternating.  Use `X` for black square, and `O` for white square.

<img src="./Images/24_checkerboard.png" alt="checkerboard" style="zoom: 50%;" />

Typically programmers use variable names such as: 

- `row` and `col` 
- `r` and `c` 
- `i` and `j`  (effectively from Sec V math) 

 If (col+row) % 2 == 0  then print white square  else print black square 

**pseudo code**: 

We are using modulo to add the row and column and if it is even we go white square 

```text
for row = 1 to 8   // eight is a magic number - it should be a constant!! 
   for col = 1 to 8 
    If (col+row) % 2 == 0  then print white square  else print black square
  next col 
      print blank line, moving to next row 
next row 
```

 You can implement this into C# using O and X where O is white and X is black 

```text
OXOXOXOX 
XOXOXOXO 
OXOXOXOX 
XOXOXOXO 
OXOXOXOX 
XOXOXOXO 
OXOXOXOX 
XOXOXOXO 
```

(8 by 8 board above) 

### Exercise 2

Want to take this a step further: 

Another exercise to try: Prompt the user to input a size of the board, print it out. 

The pattern will always be square. 

#### Validation

**Want to do some Q/A Testing? Quality Assurance?** 

- Test your program above with 
  - a negative number - does it crash? 
  - zero - does it crash? 
  - one - does it crash? 
  - 10 - it should work 
  - 100000000 what happens when it goes off screen? Crash? is there a max size? did you code for this? 
  - what happens if they enter "Bob" for size? Crash? 
  - What happens if they enter 4.3 for size, does the `real number` crash it? 
- Remember - your program should **NEVER crash** - you should display error message. 

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

