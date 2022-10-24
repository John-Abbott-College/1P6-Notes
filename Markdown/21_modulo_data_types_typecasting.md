## Keyboard Tips: Auto format (indent)
Make sure to **constantly** use automatic code formatting:

**Default hotkeys** for Visual Studio (Windows):

- Ctrl+E, Ctrl+D to format the entire document.
- Ctrl+E, Ctrl+F to format the selection (whatever is highlighted).

**Some versions** of Visual Studio (Windows):

- Ctrl + K + D  to format entire document.
- Ctrl + K + F to format the selection (whatever is highlighted).

**To find out which key bindings apply in _your_ copy of Visual Studio**:
In menu _Edit_ → _Advanced menu_ - the keys are displayed to the right of the menu items, so it's easy to discover what they are on your system.

**Customize the keyboard shortcuts** in menu _Tools_ → _Options_ → _Environment_ → _Keyboard_ (either by selecting a different "keyboard mapping scheme", or binding individual keys to the commands "Edit.FormatDocument" and "Edit.FormatSelection").


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


## Typecast and Mixed Types

Sometimes you need to temporarily convert a number into another type so that is matches. 

**example**: 

 ```csharp
  int apples = 25; 
  double grapes = 3.35; 
 
  grapes = grapes * apples; // will this work??? I'm mixing types….. uh oh….not sure. 
 
  // what about: 
  apples = apples * grapes; // not sure either 
 ```



 Now what is you want to multiply these? An integer and a Double??? Will you get into trouble here? 

Some languages are "loosely typed" and some are very "strictly typed". C# is finnicky with its types, so we need to typecast 

## Explicit Casting

> **General Rule** - to avoid relying on the system to "maybe" do something for you - you should "typecast" your variables to the type on the left hand side of the equals. 

 **Rules**

* You want everything on the right hand side of the equals sign to match the type of the variable on the left hand side of the equals sign.
* to change type, enclose the type name in parenthesis before your variable. 
  * *Example*: ` (int) var1 `
    * this means, convert `var` to an `int` for this calculation only!

**Example**: 

 ```csharp
 int abc = 2; 
 double def = 6.8; 
 
 abc = abc * (int) def; 
 
 // similarly 
 def = def * (double) abc; 
 ```


Remember - typecast is only temporary for that equation or line of code. Typecast does not change they type of the variable which was assigned at birth.  

FYI - if you typecast a `double` to an `int`, it will be TRUNCATED !

> **Truncated**: the decimal portion of the real number will be chopped off.  
>
> This has the affect that the real number will always be rounded towards zero to the nearest integral value.
>
> *Positive numbers*: `(int) 45.9 = 45`,  `(int) 45.0 = 45`, `(int) 45.1 = 45`
>
> *Negative numbers*: `(int) -45.9 = -45`,  `(int) -45.0 = -45`, `(int) -45.1 = -45`

## Type Conversion Methods

[reference](https://www.w3schools.com/cs/cs_type_casting.php)

It is also possible to convert data types explicitly by using built-in methods, such as `Convert.ToBoolean`, `Convert.ToDouble`, `Convert.ToString`, `Convert.ToInt32` (`int`) and `Convert.ToInt64` (`long`):

```csharp
int myInt = 10;
double myDouble = 5.25;
bool myBool = true;

Console.WriteLine(Convert.ToString(myInt));    // convert int to string
Console.WriteLine(Convert.ToDouble(myInt));    // convert int to double
Console.WriteLine(Convert.ToInt32(myDouble));  // convert double to int
Console.WriteLine(Convert.ToString(myBool));   // convert bool to string

```

### What is the difference between explicit type casting and converting?

Converting a real number to integer uses *rounding* instead of *truncation*.  See example below:

```csharp
double a = 45.7;
int b = (int)a;
int c = Convert.ToInt32(a);

Console.WriteLine("original number: " + a);
Console.WriteLine("integer cast: " + b);
Console.WriteLine("convert to Int32: " + c);

```
