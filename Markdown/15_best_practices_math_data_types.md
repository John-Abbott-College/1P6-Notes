**Reminder** : your test will be at 11:30 - 14:30 am Thursday Sept 30. The test is closed book, closed notes. Bring pen, pencil, eraser.

# Thoughts about assignment 2

1. Please, *please*, do not have ridiculously long lines of code.  

   1. In C#, the line of code doesn't end until there is the semi-colon, so just hit 'return' once in a while
   2. Long comments can be split over multiplie lines, just remember to start each line with `//`

2. For the same reason as above, *please* do **not** use end-of-line comments.  The code line becomes too long.  Not everyone one has 60" monitors!

   1. Unless defining a variable, put the comment on a separate line *above* the line(s) of code that it is referring to.

3. All code should have, at minimum, a comment describing what the program is supposed to do

4. Use proper variable names.  If they are long, use either `camelCase` or `snake_case`. Do *not* runallthewordstogetherwithoutanyspaces. 

5. To save the extra use of variables that you won't need later on, use the following:

   ```csharp
   int number = int.Parse( Console.ReadLine() );
   double real_number = double.Parse( Console.ReadLine() );
   ```

6. **USE CONSTANTS**. Seeing a formula like the one below would be hard to modify if the requirements for the program changed suddenly

   ```csharp
   // if you don't know what it is supposed to be doing, then it would
   // be hard to figure out
   total = 9 * 99 + 10 * 99 * 0.8 + (number - 19) * price * 0.7;
   ```

   ```csharp
   // Better way
   total = NUM_FULL_PRICE * price +
           NUM_FIRST_DISCOUNT * price * FIRST_DISCOUNT_PERCENTAGE/100.0 +
           (number_purchased - NUM_FULL_PRICE - NUM_FIRST_DISCOUNT) * price 
           * SECOND_DISCOUNT_PERCENTAGE/100.0;
   
   ```

   

# Comparison Operators

| Symbol | Description                                                  |
| ------ | ------------------------------------------------------------ |
| `<`    | less than                                                    |
| `>`    | greater than                                                 |
| `<=`   | less than or equal (Note... no space between the `<` and `=`) |
| `>=`   | greater than or equal (... no space between the `>` and the `=`) |
| `==`   | equality (be very careful not to use a single `=` in a `conditional`) |
| `!=`   | not equal to                                                 |

We use comparison operators in `if` statements and in `while` loops whenever we test a condition. 

Notice how whenever/however I test something it always yields a true or false answer. 

### Common Mistake

**Version 1**

```csharp
int age = 15;
if (age == 16) 
{ 
	Console.WriteLine("Happy Sweet 16"); 
} 
// Nothing is displayed
```

**Version 2**

```csharp
int age = 15;
if (age = 16) // Lucky for you, the compiler see this error, and will not run your code! 
{ 
	Console.WriteLine("Happy Sweet 16"); 
} 
```

# Mathematical Operations

**Mathematical Operations** 

| symbol | explanation                                                  |
| ------ | ------------------------------------------------------------ |
| `*`    | asterisk means multiply (when it is in in a formula) (it could be part of a comment, for example `/* hi there */`) |
| `/`    | divide                                                       |
| `%`    | modulo (the remainder after the integer division)            |
| `++`   | increment by one (unary operator)  `a++` is same as `a = a + 1` |
| `--`   | decrement by one (unary operator) `a--` is same as `a = a - 1` |
| `+=`   | `a += 3` is equivalent to: `a = a + 3`                       |
| `-=`   | `a -= 3` is equivalent to `a = a - 3`                        |
| `/=`   | `a /= 5` is equivalent to `a = a/5`                          |
| `*=`   | `a *= 4` is equivalent to `a = a*5`                          |

**Example**

```csharp
// code excerpts 
a = a + b;   

// you could re-write the above using a different syntax doing this: 
a += b; 
```

>  *NOTE*: You can certainly get away with never using this syntax but it is quite common out there in the real world. 

### Modulo

**Example**

```text
Declare a, b, c as integer 

a = 10; 
b = 3; 
c = a % b;  // c will be 1 
```

Modulo is the remainder after division.

`10/3` is `3 remainder 1` , `10` `modulo` `3` is `1`

**Exercise**

Evaluate the following math expressions:  

```text
 5 % 2 
14 % 5 
20 % 6 
 4 % 8 
14 % 8 
25 % 17 
 2 % 9 
 9 % 2  
```

**Example**: Modulo is very commonly used to determine if something is even or odd. 

```csharp
// variables declared and defined above

if ( (number % 2) == 0 ) 
{ 
		Console.WriteLine(" number is even!") 
} 
else 
{ 
		Console.WriteLine("number is odd!") 
} 
```

So if the number divides by two perfectly, the remainder will be zero and so it is even. Otherwise it is odd.  

# C# Data Types

`.NET` has many types that are "supersets" of native C types. This means they are the same as the true C type but they have other goodies associated to it (which you will learn in programming 2). 

| Reserved Word | .NET Type | Type                                                         | Size (bits) | Range (values)                                          |
| ------------- | --------- | ------------------------------------------------------------ | ----------- | ------------------------------------------------------- |
| byte          | Byte      | Unsigned integer                                             | 8           | 0 to 255                                                |
| sbyte         | SByte     | Signed integer                                               | 8           | -128 to 127                                             |
| short         | Int16     | Signed integer                                               | 16          | -32,768 to 32,767                                       |
| ushort        | UInt16    | Unsigned integer                                             | 16          | 0 to 65,535                                             |
| int           | Int32     | Signed integer                                               | 32          | -2,147,483,648 to 2,147,483,647                         |
| uint          | UInt32    | Unsigned integer                                             | 32          | 0 to 4294967295                                         |
| long          | Int64     | Signed integer                                               | 64          | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| ulong         | UInt64    | Unsigned integer                                             | 64          | 0 to 18,446,744,073,709,551,615                         |
| float         | Single    | Single-precision floating point type                         | 32          | -3.402823e38 to 3.402823e38                             |
| double        | Double    | Double-precision floating point type                         | 64          | -1.79769313486232e308 to 1.79769313486232e308           |
| decimal       | Decimal   | Precise fractional or integral type that can represent decimal numbers with 29 significant digits | 128         | (+ or -)1.0 x 10e-28 to 7.9 x 10e28                     |
| char          | Char      | A single Unicode character                                   | 16          | Unicode symbols used in text                            |
| bool          | Boolean   | Logical Boolean type                                         | 8           | True or False                                           |
| object        | Object    | Base type of all other types                                 |             |                                                         |
| string        | String    | A sequence of characters                                     |             |                                                         |
| DateTime      | DateTime  | Represents date and time                                     |             | 0:00:00am 1/1/01 to 11:59:59pm 12/31/9999               |

 

**The most common types are**: 

Int32  - this is used to declare an integer 

Single - this is used to declare a floating point real number 

String - used to declare a string (or group of characters - a word) 

Boolean - to declare Boolean types 

You will notice .NET types begin with capital letters. 

>  For now: only use `string` or `String`, `double` or `Double`, `int` or `Int32`, `bool` or `Boolean`.  Everything else should be avoided unless you have a special reason not to.