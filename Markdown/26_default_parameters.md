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

Refactor your code to make the function reusable for **any prompt message** you might have.

Examples of message:



The message should be passed to the function as an argument.

Examples of function calls:

```csharp
int birthDay, studentNumber, age;

string birthDayQuestion = "What is your birth day?";
string studentNumberQuestion = "Please enter your JAC student number";
string ageQuestion = "Quel âge as-tu ?";

birthDay = GetIntInput(birthDayQuestion);
studentNumber =GetIntInput(studentNumberQuestion);
age =GetIntInput(ageQuestion);
```


## Resources

- [Named and Optional Arguments](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/named-and-optional-arguments) (C# Programming Guide) by Microsoft.


## Exercises

### 1. GetIntInput: Max and Min Limits

Refactor (aka. modify) the `GetIntInput( )` done in class in order to:

- Pass the maximum and minimum allowed integers to the function.
- Have the function will assure the user input is within this range.
- If a minimum range is not passed, have it default to `1`.

Example of function calls:

```csharp
birthYear = GetIntInput(birthYearQuestion, 2022, 1900);
birthDay =GetIntInput(birthDayQuestion, 31, 1);
birthDay =GetIntInput(birthDayQuestion, 31);  // only 2 arguments passed
```


### 2. GetIntInput: Custom Limit Error Message

Refactor the previous  `GetIntInput( )` in order to:
- Pass a custom error message to the function if user enters an integer outside of the valid range.

Example of function calls:

```csharp
string birthDayQuestion = "What is your birth day?";
birthDay =GetIntInput(birthDayQuestion, 1, 31, "Invalid. Day range is between 1 to 31");
```

### 3. GetIntInput: Custom Parse Fail Message

Refactor the previous `GetIntInput( )` in order to:
- Pass a custom parse error message in case the user does not types in an integer
- If a custom message is not provided, use a default error message.
Example of function calls:

```csharp
string birthDayQuestion = "What is your birth day?";
string rangeErrorMessage = "Invalid. Day range is between 1 to 31";

// Function call with custom parse error message
birthDay = 
GetIntInput(birthDayQuestion, 1, 31, rangeErrorMessage, "Birth day must be an integer");

// Function call without error message (dafault parameter is used)
birthDay = 
GetIntInput(birthDayQuestion, 1, 31, rangeErrorMessage);
```
