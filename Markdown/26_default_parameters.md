# Function Design & Default Parameters

## Default Parameters

It is possible to use the same function with a different number of arguments.

```csharp
a = MyFunc(10, 20);		// function with 2 arguments
b = MyFunc(4, 8, 9); 	// 3 arguments?! How?!
```

This is only possible if the function uses **default values**. The function declaration might look like this:

```csharp
static int MyFunc(int param1, int param2, int param3 =5)  // notice the =5
{ 
	// function logic here
 	return localInt; 
}
```

The third parameter, `param3 = 5`, works as follow:

1. If parameter 3 **is NOT passed** to the function, then `param3` will default to the value `5`. Therefore, the program will *not* crash claiming that `param3` is undefined.
2. If a parameter 3 **is passed** to the function, `param3` will be equal to the value passed.


### Defaults Go Last

When using default parameters, in a function declaration, they must be the last parameters declared in your function signature.

*Allowed:*

```csharp
static int myFunc(int a, int b, int c = 35)
```

***Error:***

```csharp
static int myFunc(int a, int b = 35, int c )  // default in the middle:
```


### Summary

> **Important Rules:**
>  
> - Parameters order must always be respected.
> - All non-default parameters must be passed when calling the function.
> - Any *default parameters* must **follow the *non-default parameters***.


## Named Parameters


> You are not be expected to know named parameters!
> Not on the test. For your knowledge only.

It is also possible to use named parameters to change the order of arguments being passed to a function.

*Function declaration:*
```csharp
static string GetJacEmail(string firstName, string lastName)
{
	string localString = firstName.ToLower() + "." +
					    lastName.ToLower() + "@johnabbott.qc.ca";
	return localString;
}
```

*Function call:*
```csharp
string email;
// Function call with normal ordered arguments
email = GetJacEmail("Mauricio", "Buschinelli");

// email = mauricio.buschinelli@johnabbott.qc.ca

// Function call with named parameters but in the right order
email = GetJacEmail(firstName: "Mauricio", lastName: "Buschinelli");

// Function call with named parameters but in the WRONG order
email = GetJacEmail(lastName: "Buschinelli", firstName: "Mauricio");
```


## Function Design

The course has covered enough concepts in order design **modular and reusable functions**.

Remember, the **design principles** for creating good functions are:

- **Avoid repetitive code**.
- **Create reusable code.**
- **Help keep code modular and organized**.

These principles are inline with **how to learn computational thinking** (covered in week 1, lesson #2):

**Being incremental and iterative**:
	- Design should start with small pieces that can be verified to work. Slowly add complexity and regularly check that it is still functional.

**Testing and debugging**:
	- Develop strategies for anticipating and dealing with problems efficiently. Most of the development time is spent debugging.

**Reusing and remixing**:
	- Don't reinvent the wheel but understand what you are bringing into your design so that you can adapt it to your needs and fix it when it breaks. Provide proper attribution.
	
**Abstracting and modularizing**:
	- Build something large by putting together collections of smaller parts. Make reusable and adaptable parts.

(*Adapted from Brennan & Resnick, AERA 2012, New frameworks for studying and assessing the  
development of computational thinking*)


### Design Example: GetIntInput( )

Let's create a function named `GetIntInput( )` that will:

> Ask the user for a piece of information and returns the inputted integer. If an invalid input is provided, an error is shown and the user can try again.

- The function must be reusable, so make it as generic as possible.
- Assume that this function will be used to collect different types of information.

#### Phase 1: Prototype

The first step is to create something as simple as possible that will accomplish the main features of our function.

##### Phase 1.a - Brainstorm Pseudo Code:

Using a new function:

1. Display the request for information.
2. Collect input.
3. Parse the integer.
4. Output an error message for invalid inputs.
5. Repeat steps 2 to 4 until parsing worked.
6. Return parsed integer.

##### Phase 1.b - Inputs and Outputs

> If an element of your requirements or final design is not clear:
> 
> - Start with a reasonable assumption that will simplify your prototype.
> - Go back and revise/improve it later.

**Outputs**
- The parsed integer.
**Inputs**
- Do we have any? Start with no inputs. Revisit it later.

How about the message that will ask the user to enter some information?
- Don't worry about it for now. Hard code it!

##### Phase 1.c - Code Prototype

> *The example code is purposely not show. Will be included after in-class exercise*


#### Phase 2 - Make it reusable

Refactor your code to make the function reusable for any 

## Resources

- [Named and Optional Arguments](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/named-and-optional-arguments) (C# Programming Guide) by Microsoft.


## Exercises

### 1. Modifying GetIntInput

- rewrite `GetIntInput` to enable user to add the error message.  Test your work

  Example of calls:

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

   
Is this possible? Yes - with optional parameters.

We simply re-write the first line of the function with a default value for arguments that may not be passed.

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

