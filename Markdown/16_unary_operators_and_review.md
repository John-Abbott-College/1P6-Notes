# Review for test

### Trace Table Walthrough

Write a trace table for:

```csharp
int a = 10;
int b = 2;
int c = 0;
c = a + b;
d = c + b;
a = b / a;
```

### Truth Tables

Create truth table for: ` ( p imples q ) and (p or q)`

### if statements

... practice the code examples that I gave in lab class last week.

### while loops

... practice the code examples that I gave in lab class last week.

# Unary Operators

These are operations that are done on one variable. These can (and do) occur on the right hand side of the equals. Or they can occur all alone. 

There are `PREFIX` operators and `POSTFIX` operators. They are both `UNARY` operators. 

**Example**

 ```csharp
   int apples; 
 
   apples = 5;    // you could have done int apples = 5; 
 // you'd be declaring and defining on the same line. 
 
   ++ apples;    // this is a unary operator. It means apples = apples + 1; 
 // This changes the value of apples. It "increments" it by one. 
 
   apples ++;  // same thing it increases apples by one. 
 
   int orange = 10;   // declare and define on one line… 
 
   orange ++ ;    // this is also a unary operator it means oranges = orange + 1; 
 ```



Things get a little funky when we introduce an "=" into the equation - then it makes a **big** difference whether the `++` is on the left hand side or right hand side of the variable. 

When using `UNARY` operators in an equation notice that the variable on the left hand side of the equals changes, `AND` the variables with the UNARY operator (on the right hand side) changes as well!! 

 **Example**

```csharp
int a = 5; 

int b = 4; 

b = ++a + b; // there is no syntax error here - there is a unary operation going on. 

// what is the output of a?  Of b? 
```



**Rules**: 

- Do all the `prefix` operators (these appear on the left hand side of the variable 
- Do the `=` and alter the variable on the left hand side of equals 
- Do the `postfix` operators (these appear on the right hand side of the variable 



**Exercise**

Try this exercise now: 

```csharp
int a = 2; 
int b = 3; 
int c = 4; 

a = ++b - c--; // this is the major line 
Console.WriteLine (a+ " " + b + "  " + c); 

```

 What is the output of the above?  

Never do this: `a = -- c -- - ++ b --; `, it is just way too confusing!!!

**Exercise**

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



In general don't make things this complicated!!! Keep it simple. You may see this in the workplace. 

FYI `--` means reduce by one or `DECREMENT` the variable (opposite of `INCREMENT`) 

**Example**

Consider what happens if things get too messy: 

```csharp
using System; 
class MainClass { 
public static void Main (string[] args) { 
	int a, b, c; // the variables are born 
	a = 1; 
  a = a++; // getting snafu'ed on itself! Do not do this. 
	Console.WriteLine(a ); 
	Console.WriteLine ("Hello World"); 
} 
}
```
 We think the output should be `2` but things get screwy and you only get `1`  

Moral of the story - don’t get too twisted doing things like 
`c  = -- c ++ ;` 

 

