# Unary Operators

**Unary operators** are the short-form notation for operations done to one variable.

There are `PREFIX` operators and `POSTFIX` operators. They are both `UNARY` operators. 


| symbol | explanation                 | Example                                |
| ------ | --------------------------- | -------------------------------------- |
| `++`   | increment by one            | `a++` is same as `a = a + 1`           |
| `--`   | decrement (subtract) by one | `a--` is same as `a = a - 1`           |
| `+= x` | increment by `x`            | `a += 3` is equivalent to: `a = a + 3` |
| `-= x` | decrement (subtract) by `x` | `a -= 3` is equivalent to `a = a - 3`  |
| `/= x` | divide by x                 | `a /= 5` is equivalent to `a = a/5`    |
| `*= x` | multiply by x               | `a *= 4` is equivalent to `a = a*5` |

**Example 1**

```csharp
int a = 1;
int b = 2;

a = a + b;   
// you could re-write the line above using unary operators: 
a += b; 

// Final result: a = 3
```

>  *Note*: You can certainly get away with never using this syntax but it is quite common out there in the real world. 


**Example 2**

 ```csharp
int apples = 5; 
 
apples++;    // It means apples = apples + 1;
			  // apples is now 6 
 ```


### Prefix vs Postfix Operators

In all of the example above, the unary increment operators were used in their **postfix** form.

**Postfix** means the operator was placed **after** (post) the variable.

```csharp
int apples = 5; 
apples++;    // apples = apples + 1;
```

**Prefix** means the operator was placed **before** (pre) the variable.

```csharp
int apples = 5; 
++apples;    // apples = apples + 1;
```


> There is a big difference in **when** the value of the variable is calculated for postfix vs prefix operators.

**Rules:**

- **prefix** operators are calculated **before** variable assignment.
- **postfix** operators are calculated **after** variable assignment.

 **Example 3**

```csharp
int a = 5; 
int b = 4; 

b = ++a + b;

Console.WriteLine("Value of b is: " + b);
Console.WriteLine("Value of a is: " + a);
// Result?
```

In the example above, `++` is in the **prefix** position, so `a = a + 1` happens **before** the value of `b` is calculated.

If we were to break down the operations:

```csharp
int a = 5; 
int b = 4; 

// Breaking down b = ++a + b;

// 1. Calculate the unary ++a (prefix is done before assignment).
a = a + 1   // a = 6

// 1. Calculate b
b = a + b   // b = 6 + 4
```

*Output*
```text
Value of b is: 10
Value of a is: 6
```

**Example 4**

```csharp
int a = 5; 
int b = 4; 

b = a++ + b;

Console.WriteLine("Value of b is: " + b);
Console.WriteLine("Value of a is: " + a);
// Result?
```

*Output*
```text
Value of b is: 9   // Can you see why?
Value of a is: 6
```

### Overdoing Unary Operators

In general, don't make expressions with unary operators too complicated!

Keep it simple so that other humans can easily read things without getting confused. 

Consider what happens if things get too messy: 

```csharp
int a = 1;
a = a++; // Do not do this. 
Console.WriteLine(a ); 
```

We think the output should be `2` but things get screwy and you only get `1`  


### Exercises

**Exercise 1**

What is the output of the code below?

```csharp
int a = 2; 
int b = 3; 
int c = 4; 

a = ++b - c--; // this is the major line 
Console.WriteLine (a+ " " + b + "  " + c); 
```


**Exercise 2**

```csharp
int a, b, c; // the variables are born 
a = 5; 
b=3; 
c = ++ b - a; 
a = a + c--; 
c -=a; 
a = ++b + ++c; 

Console.WriteLine(a + “ ” + b+ “ ” +c); 
```

