# Do While Loop

This is another type of loop in C#. It is similar to the while loop - but - the condition is checked at the end of the loop (not at the beginning). This means that your loop will guaranteed iterate at least once - even if the condition is false 

 Pseudo code: 

```text
x = 0; 									// Clearly, x is NOT greater than 10
do 
{ 
	/// bl bla bla bla 		// but this code will be executed at least ONCE
	// bla bla bla 				// before the condition is checked!
} while (x > 10); 			// restarts the loop if true

```

 **Formal syntax in Csharp** 

```csharp 
int yourchoice; 
// yourchoice is undefined, it better be defined before you hit the 
// checking of the condition 

do 
{ 
	// your code block 
	// It is your job to ensure that  
	// yourchoice has a value (it is defined) 
	// Perhaps ask the user for input, and put that into yourchoice 
} while (yourchoice !=5); 

```

Compare and contrast of `while` versus `do while`: 

```csharp
while (x<10) { 						// NO SEMICOLON !!!
  // bla bla bla bl 
  // more code here 
}
```



```csharp
do { 
  // bla lba bla 
  // code here 
) while (x<10); 					// USE SEMICOLON !!!
```

## Creating Menus

This type of loop is excellent for menu choices and creating menus. 

Consider the pseudo code below: 

```text
int menuChoice
do
{
	clear screen
	print "Main Menu"
	print "1. option one"
	print "2. option two"
	... etc ...
	print "9. Quit Menu"
	
	print "please enter choice"
	input menuChoice
	if (menuChoice == 1) {
		do option one code
	}
	else if (menuChoice == 2) {
		do option two code
	}
	... etc
}
// QUIT
while (menuChoice !=9);
```

Notice how this menu system will keep looping offering the user choices and doing the choices until the user chooses 9, when the menu system stops. 

## Validating User Input

Sometimes we ask the user for input within a certain range - and we want the user to enter such a number. If they don't we want to keep asking them to do so until they type the proper number. 

**Remember:** *A `do-while loop` checks the `condition` AFTER the code block has been executed!*

**Example**

```csharp
int yourNumber;

// =======================================================================
// get valid user number using a do-while
// =======================================================================
// get the number
do
{
  Console.Write("Please enter a number between 9 and 49 inclusive: ");
  // NEVER DEFINE A VARIABLE INSIDE A LOOP
  // (the reason will be explained at a later date)
  // int yourNumber  !!! Don't do it!!
  yourNumber = int.Parse(Console.ReadLine()); 
}

// validation that number is good
while (yourNumber < 9 || yourNumber > 49);

// =====================================================================
// now that we have a valid user number... do stuff
// =====================================================================
Console.WriteLine("Yes, you have typed in a valid number: "+yourNumber);

// =====================================================================
// keep the console window open until the user hits "return" key
// =====================================================================
Console.ReadLine();
```



Consider displaying nice error messages for the user 

```csharp
int yourNumber;
int MIN_NUM = 9;
int MAX_NUM = 49

// =======================================================================
// get valid user number using a do-while
// =======================================================================
// get the number
do
{
  Console.Write("Enter a number between "+MIN_NUM+" and "+MAX_NUM+" inclusive: ");
  yourNumber = int.Parse(Console.ReadLine()); 
  
  // error message
  if (yourNumber < MIN_NUM || yourNumber > MAX_NUM) {
    Console.WriteLine("Please read instructions carefully!!!")
  }
}

// validation that number is good
while (yourNumber < MIN_NUM || yourNumber > MAX_NUM);

// =====================================================================
// now that we have a valid user number... do stuff
// =====================================================================
Console.WriteLine("Yes, you have typed in a valid number: "+yourNumber);

// =====================================================================
// keep the console window open until the user hits "return" key
// =====================================================================
Console.ReadLine();
```
