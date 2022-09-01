# Day 5 - Variables

## Definition

A variable is a temporary holding place for a value. Think of it as a box that can store a single item.

This value can be of different types, for example:

- a number, such as the user's hourly pay, or the number of students in a course;
- a word or sentence (aka. a "string"), such as the user's name;
- many other things that we'll visit later...

```csharp
// Number variables
int hourlyPay = 21;
int noStudents = 30;

// String variables
string userName = "Mauricio";
string greeting = "Hello there!";
```


### Variable Names

> 👉 Variable name should be **meaningful**!
>
> Anyone reading your code should be able to guess **what a variable represents** and **how it will be used** just based on the variable name.

Examples: 

* `highScore`
* `hourlyPay`
* `w`

What do is `highScore` referring to?
	- It depends on the context but if we are looking at the source code a game, we would have a good idea of what it holds and what's intended for.

What about `hourlyPay`?
	- Again, it's context dependent, but if we know we are looking at a budgeting app, we can guess it's meaning.

 `w`  is a terrible choice for a variable name.
	 - Only the original developer know what it means.

> 💣 Code submitted with poor variable names will have marks deducted.

There are rules for naming variables as well standards - refer to the web for this. 

#### Naming Rules

1. The variable name **cannot** start with a number
2. It may contain letters and numbers after the first character
3. It may contain an '\_' (underscore)
4. It **cannot** contain a ' ' (space), a '#' (hashtag), '!' (exclamation point), or '.' (period)
5. Variable names **cannot** be a *reserved* word. 
	- *Reserved* words are special words that the compiler expects to mean certain things internal to the language.
	- The list of reserved words is dependent on the computer language you are using. Example `print` is typically a reserved word for most languages.
	- For a list of reserved words in C#, see the official documentation [C# Keywords](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/).

#### Naming Standards

Naming standards are simply a recommended set of guidelines in naming your variables.  The advantage of following these guidelines is that other people who read your code will have an easier time of it.  And yes, someone *will* read your code, no matter where you end up working.

Naming standards [vary with programming language](https://en.wikipedia.org/wiki/Naming_convention_(programming)), so if you want information about another language, just check wikipedia.

##### Multi-word identifier formats

There are many different ways of using two or more words, flattened together into a single variable name. A few of them are shown below.

| Formatting | Name(s)                    |
| ---------- | -------------------------- |
| twowords   | flat case                  |
| TWOWORDS   | upper flat case            |
| twoWords   | camelCase                  |
| TwoWords   | PascalCase, UpperCamelCase |
| two_words  | snake case                 |

For .NET languages (C# is a .NET language) the Microsoft guidelines recommend the exclusive use of only `PascalCase` and `camelCase`.  `PascalCase` is used for class names (will be describing what a class is at a much later date). `camelCase` is used for variable names.

Although it is not in the MS guidelines, many people will use all CAPS if they are declaring a constant ( a constant is a variable whose data *never ever* changes.)

### Creating or Declaring Variables

When your program "declares" a variable - it 'creates' it. You have to declare a variable before you use it. I use the analogy of "birth" to give birth to or create a variable.  

Behind the scenes: 

> Your program has a line of code that says "reserve a spot for me to store data please". The operating system hears this request and reserves a location in memory specifically for that variable. This location is an address in RAM. 

## Creating Variables 

**A variable should (must in C#) be declared (or “born”) in most languages before you can use it.**  

 To declare a variable, we must specify what type of data we want to store.  We will cover different data types in another lecture, so for now, lets just introduce two different types of data.

**integers**: A whole number, signed or unsigned (`-10`, `+10`, `10`)  

**strings:** A list of characters (`sandy`, `bob is my brother`, `the number one (1) can often be confused as the letter ell (l)`)

To create an integer in C#, use the keyword `int`.

> The word int in C# is "reserved" - it is a keyword that is part of the language. You cannot create a variable named int !!!!! As innocent as it looks int is a "creator" 

To use a variable in C#:

* declare (*only ever declare once, you are not allowed to be born twice ... lol*)
* define (give your variable some data)
* use 

```csharp
int myscore;            // this is a declaration or birth 
myscore = 0;            // this is a define - meaning I give it a value 
myscore = myscore + 10; // I can use the variable  
```

Everytime you run your program, the operating system will reserve a place in memory for the variable. This place is irrelevant to you since you refer to the variable in a high level language and call it myscore. If you run your program tomorrow, the operating system will reserve a different place in RAM, but again, who cares since you refer to it as myscore. 

 ### How do Variables Work?

The variable name simply becomes an *alias* for a memory location.

#### Analogy

Imagine that the memory (RAM) is just a bunch of boxes, all lined up in a neat row.

When the programmer declares a variable with a name `sandyAge`, it is as if someone wrote the name of that variable (`sandyAge`) on a particular RAM box.

```csharp
int sandyAge;
```

There is nothing in the box (at least not yet).

---

I want to put the number `5` in the box?  How do I do that?  By using an *assignment statement*.

```csharp
sandyAge = 35; // not my real age :)
```

What does the above instruction mean?  

* Firstly: read from right to left (instead of the typical left to right). The number `35` is the data.  The equals sign (`=`) doesn't *really* mean equal, it means assign to.  

* Recap, take the number and assign it to... *what*?  
* To the `sandyAge` box in RAM.  How do we find that box?  We don't care, because the CPU and O/S will take care of finding the RAM box that has the name `sandyAge` written on it.

* Lastly, the number `35` is placed in the `sandyAge` RAM box.

---

My birthday has come and gone, and I want to change my age by one year.  How do I do that?

Continuing with the analogy...

* I need to get my current age out of the `sandyAge` box
* Whatever value it is, I need to add one to it
* Then I need to put this new number back into the `sandyAge` box.

```csharp
sandyAge = sandyAge + 1;   // this is not a MATH formula !!!
```

The above bit of code does exactly what we want.  

The code is parsed right to left.  So firstly, the program needs to 

* parse `sandyAge + 1`.  It recognizes that `sandyAge` is a variable, so it gets the number from the `sandyAge` RAM box, which currently happens to be the number `35`.
* Replacing `sandyAge` with `35`, the program now needs to parse `35 + 1`.  Because computers are good at math, it knows that the final number should be `36`.
* We now have `sandyAge = 36`.  Again, working from right to left, and knowing that the equals sign (`=`) actuall means *assign to*, the computer will place the number `36` into the `sandyAge` RAM box.

## Extra Info

### Variables in programming

In reality, a variable is a temporary holding location (memory address) for a value. This location has a name - which is the name of the variable.

The program (high-level language) refers to this address by the variable's name rather than the specific memory location.

FACT 

> Everytime you run your program, the operating system will allocate a different place in memory. You don’t really care because you reference that variable by its name in a high level language. The fact that it is created in a different place in RAM every run doesn’t affect you. Windows will handle this memory allocation. 

### An anology?

> An **accountant** is doing your taxes.  What is most important about identifying you is your **social insurance number** (SIN).  But it would not be nice to constantly call you by your number, and it would be hard for the accountant to remember what your number actually is.  Much better if the accountant simply calls you by your **first name** when communicating with you.  Only the **government** cares about your SIN.
>
>
>| Analogy                | Programming                     |
>| ---------------------- | ------------------------------- |
>| client's name          | variable name                   |
>| the client             | data                            |
>| government             | cpu                             |
>| accountant             | high level language             |
>| social inurance number | memory address for data storage |
>


### Rules

* In C#, almost (but not all) computer instructions end with a semi-colon (`;`)

* You must declare a variable before you give it a value

* Variable names must be unique (If two boxes in the RAM had the same name, how would the computer know what you meant if you said *go to box 'x' and get me the contents*)

* You must assign something to the variable before you can expect to get anything from it.

  ```csharp
  int sandyAge;
  int newAge;
  newAge = sandyAge + 1; // ERROR!!! ERROR!!!, sandyAge has not yet been defined!
  ```

* Parsing an assignment statement is from **right to left**. 

  * What is on the right of the equals sign is calculated first
  * The result of the above calculation is saved in the variable (RAM), overwriting anything that may have already been there.
  
* The left hand side (LHS) of an assignment statement must be a variable name. 

  * Remember that we are going to put the value from the right hand side (RHS) into the RAM box that has the variable name written on it.  Anything other than a variable name makes no sense.

* Programs execute statements **one at a time**.  You cannot go back or forward to see what else is going on around you.

#### Syntax Error

A syntax error occurs when the compiler cannot figure out what it is that you want it to do.  This can be because you misspelled an instruction, used a variable that has not yet been defined, lost a quote (`"`), missing a squiggly brace (`}`), or any number of confusing things.

When you try to compile your code, the compiler will notify you if you have any syntax errors.

#### Logic Error

This is when you want your algorithm to accomplish a task, but if you follow the directions of the algorithm, it doesn't do what you want it to do.

> *Mom*: Brush your teeth
>
> *Kid*: OK
>
> *Mom*: Why can't I smell toothpaste on your breath?
>
> *Kid*: You didn't tell me that I needed to use toothpaste.



## Examples

### What is the output?

```csharp
// Declare my variables first
int apples;
int grapes;
int oranges;

// Once my variables have been declared, give them values 
apples = 5;
grapes = 3;
oranges = 10;

// Do some math
apples = apples + grapes;
grapes = grapes + apples;
oranges = oranges + (apples * 2);

// print result onto the screen
Console.WriteLine(apples, oranges, grapes)
```

### What are the errors?

```csharp
highScore = highScore;
apples + 4 = oranges + 2;
apples + 5 = grapes;
oranges * 3 + 7;
grapes + 4 = apples * 4 - oranges + 7;
grapes;
14 = apples;
apples = 15;
```

Answers (*don't look at this before class*)

```csharp
// forgot to declare the variables
int highScore;
int apples, oranges, grapes; // this is allowed... it is not an error

```

```csharp
// forgot to give the variables values before you used them
highScore = 0;
apples = 0;
oranges = 0;
grapes = 0;
```

```csharp
// this code is valid, but it doesn't do much of anything
highScore = highScore
```

```csharp
// this code is invalid, because it does not have variable names on the 
// right-hand side of the equal sign
apples + 4 = oranges + 2;
apples + 5 = grapes;
oranges * 3 + 7;
grapes + 4 = apples * 4 - oranges + 7;
14 = apples;
```

```csharp
// This code is just confusing... You haven't told the computer what you 
// want to do with this variable.  Just shouting out a name is invalid :(
grapes;
```

```chsharp
// This is valid code.  The number 15 will be placed into memory which
// is associated with the apples variable name
apples = 15
```


## Lab Work

What is the output of the following bit of code?

```csharp
int a, b, c;
a = 4;
b = 3;
c = 2;
a = a + 4;
a = a + 4;
c = a + 5;
b = c - 2;
b = c - 2;
a = b + c + a;
a = b + c + 1;
c = c - 1;
b = b + 12;

Console.WriteLine("The values are ");
Console.WriteLine(a);
Console.WriteLine(b);
Console.WriteLine(c):
```


### Review

If you feel like you need a review, complete the following two tutorials from Microsoft:

- [Hello World - Introduction to C# interactive C# tutorial](https://docs.microsoft.com/en-us/dotnet/csharp/tour-of-csharp/tutorials/hello-world) 
- [Manipulate integral and floating point numbers in C#](# Manipulate integral and floating point numbers in C#)

