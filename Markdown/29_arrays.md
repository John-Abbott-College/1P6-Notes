# Arrays

## Why do we need arrays?

Imagine the following:

I am a *very* small security firm.  My job is to scan all email messages looking for bad things ("liver and onions").

I only have a maximum of 5 messages per day.

My code could look like:

```csharp
if (message2.contains("liver_and_onions")) {
  Console.WriteLine("MSG 1, OMG: They are feeding their kids poison! Call the cops!")
}
if (message2.contains("liver_and_onions")) {
  Console.WriteLine("MSG 2, OMG: They are feeding their kids poison! Call the cops!")
}
if (message3.contains("liver_and_onions")) {
  Console.WriteLine("MSG 3, OMG: They are feeding their kids poison! Call the cops!")
}
if (message4.contains("liver_and_onions")) {
  Console.WriteLine("MSG 4, OMG: They are feeding their kids poison! Call the cops!")
}
if (message5.contains("liver_and_onions")) {
  Console.WriteLine("MSG 5, OMG: They are feeding their kids poison! Call the cops!")
}
```

But, my code is so good, and my protection of children against 'liver and onions' is so popular, I suddenly find myself with 5000 customers. With an expectation that this could increase over time?

What do I do? Use an array!

## What is an array?

There are many analogies that can describe an array, I am going to list a few of them here:

* An array is kind of like a Motel.  
  * There is only ONE motel, and it has a unique name
  * The motel has different rooms (elements) with people inside
  * The rooms are all beside each other, attached one after another
  * To access information about a specific room (element), you use the *room number* (index) to know where to go.
  * You cannot add on a new room, or delete an existing room, without rebuilding the Motel (array)
* An array is kind of like a community mailbox
  * This community mailbox is unique, and you can give it a name to refer to it ('On the corner of Grand and Cote St Luc')
  * The community mailbox has different slots (elements) for leaving mail
  * The individual slots (elements) are all in the same mailbox
  * To get the mail for a specific person, you use the slot number (index) to know which one to open
  * You cannot add a new slot (element), or delete an existing slot (element), without rebuilding the mailbox (array)
* An array is kind of like a Box containing smaller boxes.
  * We are going to work with this in class.

### Terminology

**Array** : an contiguous area of memory where a set of elements (integer, double, boolean) are stored

* the size of the array must be specified when the array is created 
* arrays are of fixed size.  you cannot make them grow larger by adding new stuff

**Element**: a value stored within the array, that can accessed using an index

**Index**: An integer used to say which element you want.  The first element is **zero**, and the last element would be **size_of_array - 1**.

### Arrays versus Lists

For those who already know how to program, and have used lists before (python uses lists predominately), here is a description of the differences

| Arrays                                                  | Lists                                               |
| ------------------------------------------------------- | --------------------------------------------------- |
| Elements are stored in contiguous memory                | Elements are stored all over the place              |
| Accessing elements is very fast                         | Accessing elements is very slow                     |
| Must define the size of the array at the beginning      | Size of the list does not need to be defined        |
| Cannot add or delete elements once the array is defined | Can append, insert, and delete elements as required |
| Access elements by using square brackets `a[i]`         | Access elements by using square brackets `a[i]`     |

## Why do we need arrays? (Cont)

Remember my company (talked about previously) that protects children from liver and onions?

Without going into the why of the C# syntax, my new code could look like:

```csharp
for (int i=0; i<messages.Length; i++) {
	if (messages[i].contains("liver_and_onions")) {
  	Console.WriteLine($"MSG {i}, OMG: Feeding their kids poison! Call the cops!")
	}
}
```





# In class exercise with the boxes

With your group, do the following with your 'arrays'

Note: 

Green = a[0]

Red = a[1]

Blue = a[2]

Purple = a[3]

Take out the cardboard squares and place them on the table.

Sort your array, ie. the boxes are in the order Green, Red, Blue, Purple.

*Execute* the following code manually.

Keep a table of the array, and write down the contents of each element of the array, for each line of code.

```text
a[0] = 2
a[1] = 1
1[2] = 0
a[3] = 4

a[2] = a[1]
a[3] = a[3] - a[0]
a[1] = 2*a[1]
a[2] = a[0] - a[1]
a[3] a[0] * a[1]
a[3] = a[0] + a[1] - 1
a[0] = 3
a[3] = (a[3] + a[1] + 1) / 3
```



# C# Array Syntax

### Declaring an array

*`type_of_array`*`[] `*`variable_name`*

Examples:

```csharp
int[] intArray;
double[] doubleArray;
string[] stringArray;
```

### Creating an array

>  **NOTE: Declaring an array is not the same thing as creating an array**

*`variable_name`*` = `**`new`**_`type_of_array`_`[`*`size_of_array`*`]`

Examples:

```csharp
intArray = new int[10];	// create an array of integers of size 10
doubleArray = new double[20];
stringArray = new string[5];
```

or you can do the declaration and the creation on the same line

```csharp
int[] intArray = new int[10];	// create an array of integers of size 10
double[] doubleArray = new double[20];
string[] stringArray = new string[5];
```

### Assigning Values to an Array

*Copied from*:  [tutorials point C# arrays](https://www.tutorialspoint.com/csharp/csharp_arrays.htm)

You can assign values to individual array elements, by using the index number, like −

```csharp
double[] balance = new double[10];
balance[0] = 4500.0;
```

You can assign values to the array at the time of declaration, as shown −

```csharp
double[] balance = { 2340.0, 4523.69, 3421.0};
```

You can also create and initialize an array, as shown −

```csharp
int [] marks = new int[5]  { 99,  98, 92, 97, 95};
```

You may also omit the size of the array, as shown −

```csharp
int [] marks = new int[]  { 99,  98, 92, 97, 95};
```

You can copy an array variable into another target array variable. In such case, both the target and source point to the same memory location −

```csharp
int [] marks = new int[]  { 99,  98, 92, 97, 95};
int[] score = marks;
```

When you create an array, C# compiler implicitly initializes each array element to a default value depending on the array type. For example, for an int array all elements are initialized to 0.

### Reading/writing to individual array elements

To access a particular element in array, use an index.  

**IMPORTANT NOTE**: if the array is of size 4, then the indices are 0, 1, 2, 3

*`array_name`*`[`*` index `*`]`

Examples:

```csharp
int[] intArray = new int[10];	// create an array of integers of size 10
intArray[3] = 21;
Console.WriteLine(intArray[0]);
intArray[2] = 2 * intArray[3];
```



# Data Storage of Local Variables and Arrays

When a program is executing, it needs to manage the memory.

> NOTE: Maybe a better explanation in lecture 31?

## Local Variables

Local variables are only accessible when they are executing the code block they are defined in.  Which means that the memory address (the actual location of in RAM) is assigned to this variable only during the duration of that code block.  Confused?

```csharp
static void foo() { // Code block 1
  int Sandy = 35;
  int Bob = 29;
  
  // ... some code ...
 
  for (int i = 1; i<10; i++) { // Code block 2
    int Sally = 902;
    int Bill = 98;
    // ... some code...
  }
}
```

Currently the executing code block is the `for` loop.  It needs access to `Sandy`, `Bob`, `Sally`, `Bill`, and `i`. The executing code saves the data for these variables in RAM (and keeps track of where each one is)

Imagine the following table is a section of RAM.  

| Address | Variable Name    | Value |
| ------- | ---------------- | ----- |
| 351     | Sandy            | 35    |
| 352     |                  | 67    |
| 353     | Bob              | 29    |
| 354     | Sally            | 902   |
| 355     | i                | 1     |
| 356     | Bill             | 98    |
| 377     | *- unassigned -* | 101   |

When the `while` loop finishes, the variables `Sally`, `Bill`, and `i` are no longer required, and are no longer associated with these addresses.  These addresses can. now be used for other things.

| Address | Variable Name    | Value |
| ------- | ---------------- | ----- |
| 351     | Sandy            | 35    |
| 352     |                  | 67    |
| 353     | Bob              | 29    |
| 354     | *- unassigned -* | 902   |
| 355     | *- unassigned -* | 10    |
| 356     | *- unassigned -* | 98    |
| 377     | *- unassigned -* | 101   |



### Stack

When the program starts, it reserves memory for local variables (plus a few other things) in a special area in memory called the `stack`.

It is called the stack, because it is similar to a stack of plates,... i.e.

* when a new local variable is required it is added to the existing stack 
  * put a plate on top of a stack of plates
* when the local variables are no longer required, it is removed from the stack (leaving the memory available for something else) 
  * remove a plate or plates from the top of the stack of plates

Typically, the number of local variables is limited in size, so the amount of memory reserved for the stack is also limited.  If you need too much memory, you have a **stack overflow** and your program crashes.

### Heap

When the program starts, it also reserves memory for things that could be quite large.  The amount of memory reserved for the `heap` is quite large, and is able to grow in size as required.

What is stored on the heap?

* Objects, arrays, lists, dictionaries, etc. (this will be explained a little bit later)

## Storing Array Data

Arrays can be quite large, although they can be small.  However, the compiler (which organizes the code and memory) will treat all arrays the same way, regardless of size.

So, given that arrays can be large, they may not fit into the *stack*.  

Therefore, 

* The required amount of memory will be reserved in the *heap* to store the array's data

* a variable will be created that holds the starting address to the memory that is reserved in the *heap* (a pointer)

# Consequences of Arrays Being Stored in the Heap

Consider the following code:

```csharp
int [] a = new int[5] {1,2,3,4,5};
int [] b;

Console.WriteLine(a[0]+" "+a[1]+" "+a[2]+" "+a[3]+" "+a[4]);
b = a;
b[2] = b[2] + 200;
Console.WriteLine(a[0]+" "+a[1]+" "+a[2]+" "+a[3]+" "+a[4]);
```

*Result*

```text
1 2 3 4 5
1 2 203 4 5
```

*Analysis*

* (Line 1) declare *and* create a new array
  * Memory in the heap is reserved for the array (assume that it starts at the address 103)
  * the address of the heap data is stored in a local variable (`a`). (So `a` is a *pointer* with a value of `103`)
* (Line 2) declare but do NOT create a new array
  * `b` is a pointer to an array, but is currently undefined
* (Line 4) print out the content of `a`
  * Note: `a[2]` means... take the address of `a` (which is hypothetically `103`), and add `2` to it to get `105`. Now access the data that is stored in the heap at address `105`.  This would be the value of `a[2]` which is  `3`

* (Line 5)   `b` (a pointer) is given the contents of `a`, also a pointer, which means now that `b` is equal to `103`
* (Line 6)  `b[2]` means... take the address of `a` (which is hypothetically `103`), and add `2` to it to get `105`. Now access the data that is stored in the heap at address `105`.  
  * The data at address `105` is currently `3`.
  * Add `200` to get`203` and save it at the same address (`b[2]`) of `105`
  * NOTE!!! we just changed data in the heap.  This is the same data that `a` is referring to when it wants info about the array!!!
* (Line 7) print out the content of `a`
  * Note: `a[2]` means... take the address of `a` (which is hypothetically `103`), and add `2` to it to get `105`. Now access the data that is stored in the heap at address `105`.  This would be the value of `a[2]` which is now  `203`

*Trace*

| Line# | `ptr val of a` | `ptr val of b` | `addr:103` | `addr:104` | `addr:105` | `addr:106` | `addr:107` |
| ----- | -------------- | -------------- | ---------- | ---------- | ---------- | ---------- | ---------- |
| 1     | 103            |                | 1          | 2          | 3          | 4          | 5          |
| 2     |                | `Null`         |            |            |            |            |            |
| 5     |                | 103            |            |            |            |            |            |
| 6     |                |                |            |            | 203        |            |            |


## Exercises

1. Follow the tutorial [Perform operations on arrays using helper methods in C#](https://learn.microsoft.com/en-us/training/modules/csharp-arrays-operations/)
	- Make sure to complete the final challenge.


