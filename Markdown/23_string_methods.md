
# String Input and Compare

```csharp
   string myStr; 
   myStr="Jane";  // you can, but the ReadLine, even if blank will over ride this value 
   
	Console.WriteLine("Who are you?"); 
   myStr = Console.ReadLine(); 

   if (myStr == "Ted")  // Case must match exactly 
   { 
	     Console.WriteLine ("Yahoo it is TED!!!!"); // if it is ted you say yahoo! 
   } 

   Console.WriteLine("Hello there "+myStr); 

```

 Consider the above - the person types in their name and we want to see if it is Ted. 

### Question

* Did the user type upper case, or lower case?

* Will it work if I typed Ted? or tEd? or some crazy combination? 
* Your job - test this to tell me if casing is an issue. 

 How do I tell, how do I know? Answer: You can surf, or rip it apart with the debugger! 

So, lets use the debugger:

#### Use the VS Debugger to answer the question

![screenshot of VS Debugger](../Images/22_Debug_compare_strings.png)

Open the `immediate window` via Debug->Windows. The immediate window allows you to inspect variables, and expressions

* To see the value of a variable, you simply type the variable name, or expression

Type the following

```code
myStr
myStr == "Ted"
myStr = "Ted"
myStr == "ted"
myStr.ToUpper()
myStr.ToLower()
```

*Expected results shown in `Immediate Window`*

```dos
myStr
"ted"
myStr == "Ted"
false
myStr = "Ted"
"Ted"
myStr == "Ted"
true
myStr.ToUpper()
"TED"
myStr.ToLower()
```

 I proved that 

*`ted` is not the same as `Ted`*

#### Use the command line debugger to answer the question

The command line debugger does *not* allow you to test code like the `intermediate` window in VS Debugger, but you can 

* See the value of the variables, `print `*` variable_name`*
* Set variables to specific values

* Set the next line to be executed `setip = `*` line number`*

Since line 19 corresponds to the statement: ` if (myStr == "Ted")`, we can keeping testing the `if` condition over and over again. If the code enters the `if block` then the condition is true, otherwise it is false


## How to properly compare strings

I can convert the user input to lower case and compare it to `ted` OR I can convert the user input to upper case and compare it to `TED`. Your choice. 

I can convert the user input to lower case and compare it to `ted` OR I can convert the user input to upper case and compare it to `TED`. Your choice. 

Aha! Now I can redo line 19 to look like this: 

```csharp
if (myStr.ToUpper() == "TED") // Now it works with any case!
```

Now I am bullet proof! 

I could also do this:

```csharp
if (myStr.ToLower() == "ted")
```

 

Note that:

```csharp
if (myStr.ToLower == "tEd")
```

is an error - because the above will never ever be true - I'm converting the user input to lower case and I'm comparing it to something with an upper case "E" in it. This can never be true. 

