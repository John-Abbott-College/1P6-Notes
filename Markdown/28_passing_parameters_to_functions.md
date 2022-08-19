# Passing Parameters to Functions

## Default Parameters

Some functions may seem to be called with a varying amount of arguments. 

```csharp
a = myfunc(10,20); 		// function has 2 arguments
b = myfunc(4, 8, 9); 	// what's going on ? 3 arguments ??
```

 No problem. This means the function has a default value so the function might look like this: 

 ```csharp
 static int myfunc(int param1, int param2, int param3=56) 
 { 
 	// bla bla bla 
 	return somenumint32; 
 }
 ```

**So what is the ``param3=56`` do? **

If parameter 3 is *not* filled in (i.e. the calling program does not pass argument 3), then `param3` will default to the value `56`.  The program will *not* crash claiming that `param3` is undefined

 ### Respecting the order

The following is **very important**

* You MUST still pass the parameters in order when you call the function
* You MUST still pass all non-default parameters when you call the function
* Any *default parameters* must always follow the *non-default parameters*

Allowed:

```csharp
static int myFunc(int a, int b, int c = 35)
```

**Not** allowed:

```csharp
static int myFunc(int a, int b = 35, int c )
```

## Named Parameters

You will not be expected to know this for any work in this class, but if you are curious, google it.

# Examples

## generic function for inputting integers

```csharp
// =============================================================================
// Program entry point
// =============================================================================
static void Main(string[] args)
{
  // I want to ask the user for age, hourly wage, hours worked, etc
  // ... and I want to validate every single input ....
  // ugh... that's going to be ugly, ... TryParse, loop => messy!
  // let's redesign
  int age, wage, hours, months, score;
  
  // so in function GoGetNumber I can then dance around with tryparse ... etc ...
  score = GoGetNumber("How do you think you did on the test?");
  age = GoGetNumber("What is your age");
  wage = GoGetNumber("what is your hourly wage");
  hours = GoGetNumber("Combien d'heures tu travail");
  months = GoGetNumber("How many months did you work");
}

// =============================================================================
// Generic function to get integers from users!
// =============================================================================
static int GoGetNumber (string message) 
{
  int num;
  bool success = false;
  while (true)
  {
    Console.Write(message+" "); // aha! the passed argument is displayed!
    success = int.TryParse(Console.ReadLine(), out num);
    if (success) { break; }
    Console.WriteLine("Hey! You entered a bad integer! Try again!");
  } 
  return num;
}
```

Notice how `GoGetNumber` can be used, and that it can be in different languages



# Exercises

NOTE: Some of these were taken from day 27, because we didn't have time last class

## Write your own Functions

Write the function and a driver program to implement. Each one is separate 

- `a = multiply(n1, n2);` 

- `biggernum = findbiggest(n1,n2);` 

- `exp = pow(4,2);` 


## Modifying GoGetNumber

- rewrite `GoGetNumber` to enable user to add the error message.  Test your work

  - Example of calls:

  `hours = GoGetNumber("Combien d'heures tu travail","Tu as typé une mauvaise character")`

  `age = GoGetNumber("Cuantos años tienes", "¿Eres un idiota? ¿Por qué estás escribiendo letras cuando deberías escribir un número?"); `)

* What about if you wanted a lower limit and a high limit - a range??? How would you do this? 

  Well the call would look like this: 

  `Lotteryguess = GoGetNumber("Enter a number between 6 and 49", "hey stop typing characters", "You typed in something good, but not in range!", 6,49); `

  The function would need to accept 5 arguments: 

  1 - the prompt message (string)

  2 - the error message because they typed in an invalid character (string)

  3 - the error message where they typed in a good number, but the number was out of range (string)

  4 - lowerlimit (int)

  5 - upperlimit (int)

  *This function would be my universal get a number type of function.*

* Now what if parameter 4 and 5 - the limits were sometimes used, sometimes not….. for example: 

  ``` csharp 
  age = GoGetNumber("quelle age as tu", "Hey! Mauvais charactere!", "age impossible", 2, 120);
  
  guess = GoGetNumber("pick a number between 1 and 100", "Bad character", "out of range", 1, 100); 
  
  // what???? only 4 are being passed???? 
  tickets = GoGetNumber("how many tickets", "invalid typing", "you can't have negative", 0);  
  
  // whaat?? now only 2 are being used 
  pick = GoGetNumber("type in a number", "lay off the characters");  
  
  ```

   

  Is this possible?? Answer - yes - with optional parameters.. 

  We simply re-write the first line of the function with a default value for arguments that may not be passed!!!!  

  This is your magic line of code 

  ```csharp
  static int GoGetNumber(String askmessage, String errmessage, String rangemessage="", int lowlimit = Int32.MinValue, int hilimit = Int32.MaxValue) 
  ```

  Note: You cannot leap-frog an argument. For example, you cannot do this: 

  ```csharp
  pick = GoGetNumber("what is the number", 10, 100); 
  ```

  **Position is important, your arguments must match the parameters** 

  So to do the above you would have to do this:

  ```csharp
  pick = GoGetNumber("What is the number", "", "", 10, 100)
  ```

  

   
