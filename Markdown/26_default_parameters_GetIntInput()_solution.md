# Missing Example

This example was left out of the previous notes on purpose:


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
  
  // so in function GetIntInput I can then dance around with tryparse ... etc ...
  score = GetIntInput("What score do you think you got on the test?");
  wage = GetIntInput("What is your hourly wage");
  months = GetIntInput("How many months did you work");
  age = GetIntInput("Quel âge as-tu ?");
}

// =============================================================================
// Generic function to get integers from users!
// =============================================================================
static int GetIntInput (string message) 
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

Notice how `GetIntInput` can be used, and that it can be in different languages


## Resources

- [Named and Optional Arguments](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/named-and-optional-arguments) (C# Programming Guide) by Microsoft.


## Exercises

### 1. Modifying GetIntInput

- rewrite `GetIntInput` to enable user to add the error message.  Test your work

  - Example of calls:

  `hours = GetIntInput("Combien d'heures tu travail","Tu as typé une mauvaise character")`

  `age = GetIntInput("Cuantos años tienes", "¿Eres un idiota? ¿Por qué estás escribiendo letras cuando deberías escribir un número?"); `)

* What about if you wanted a lower limit and a high limit - a range??? How would you do this? 

  Well the call would look like this: 

  `Lotteryguess = GetIntInput("Enter a number between 6 and 49", "hey stop typing characters", "You typed in something good, but not in range!", 6,49); `

  The function would need to accept 5 arguments: 

  1 - the prompt message (string)

  2 - the error message because they typed in an invalid character (string)

  3 - the error message where they typed in a good number, but the number was out of range (string)

  4 - lowerlimit (int)

  5 - upperlimit (int)

  *This function would be my universal get a number type of function.*

* Now what if parameter 4 and 5 - the limits were sometimes used, sometimes not….. for example: 

``` csharp 
age = GoGetNumber("Quelle âge as-tu?", "Hey! Mauvais charactere!", "Âge invalide", 2, 120);
  
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

  

   
