# Looping Over Arrays

## for loop

```csharp
int [] a = new int[100];
for (int i = 0 ; i < a.Length; i++) 
{
  a[i] = i*8;
}
```

Notice that we can get the length (size) of an array by using a *property* called `Length`.

> Properties and Methods will be taught in Programming II

## foreach loop

*Syntax*:

`foreach (`*`tmp_variable`*` in `*`array`*) { ... }

*Notes*

When you use a `foreach` loop, you cannot assign any value to the temporary variable

*Examples*:

```csharp
int[] a = new int[100];
for (int j = 0; j<a.Length; j++)
{
   a[j] = j * j;
}

foreach (int x in a)
{
  // x = 35; // NOT ALLOWED!!
  Console.WriteLine("i="+i+"  x = " + x);
}

```

What is the equivalent of a `foreach` loop?

``` csharp
											// int i = 0
foreach (int x in a)  // while i < a.Length {
{											//     i = i + 1
  										//     int x = a[i] // but you are not allowed to modify x
  // ... more code		// ... more code
}
```

# Arrays, Pointers  - revisited

How arrays are created, and what is *really* stored in the declared array variable.
![Cartoon - story follows in text](../Images/31_creating_array.png)
Imagine the following:

* Off you go to the hardware store to pick up supplies. 
* As you peruse the shelves, you pick up things that you need and put them in your shopping cart, which we will call the *stack*. 
* The shopping cart holds your *local variable data*.
* You come across a stack of bags of soil that you need.  They do not fit in your shpping cart.
* You yell "HEY! Memory Manager, I need you to reserve 20 bags of dirt for me"
* The memory manager the goes to the back of store in an area where there are numbered stalls which can be used to store stuff.  This is called the *heap*.  
	* the memory manager finds a slot that is big enough to hold your valuables.  In this cartoon, the available memory slots are from 103-112 
	* if the data (bags of soil) exist, the memory manager saves this in the appropritately addressed slot.
* The memory manager now brings you back a slip of paper, saying that the stuff in the appropriate slot belongs to you!
* You take this information, and save it in a special kind of variable (a pointer, or more accurately, a reference).  This information contains the number of the slot where your valuables are, and what kind of valuables are stored there.
* Now, you give this piece of paper a name (the variable name), and stuff it into your shopping cart.  
* You are already to carry on.

## c# example

```csharp
soil[] bags_of_soil = new soil [20];
```



# Passing Arrays to functions
![cartoon - story follows](../Images/31_passing_array_to_function.png)
Continuing our story...

* You, whose sole function is to get supplies (shall we call you `get_supplies` ?) need to give the bags of soil to the landscaper whose sole function is to fix your lawn (called `fix_lawn`?)
* You cannot give the bags of soil to the landscaper, because you don't have them!
* ... but... you do have a slip of paper (called my_array in the comic) that has the information of where the bags of soil are
* You instruct the landscaper to make a copy of this paper, so that they now have the information required.
* Your job is done.
* The landscaper on the other hand, needs to get the soil out of the bags.  Being ornery, they decide to ask specifically for bag #3.
* The landscaper yells out to the memory manager, "Hey, get bag # 3.  Here is the information as to where it is stored"
* So, the poor overworked memory manager does just that.

The end, sleep tight

## C# example

```csharp
static void get_supplies() {
  soil[] bags_of_soil = new soil[20] {"dirt", "dirt", "dirt", // ... etc}
  int green_box = 3;
    
  fix_lawn(bags_of_soil);  
}

// Notice that we have to specify that 'dirt' is a `soil array'?
static void fix_lawn( soil[] dirt ) 
{
  soil three = dirt[3];
  // and more code
}
```

## VERY IMPORTANT

Because `get_supplies` and `fix_lawn` are only copying the location of the bags of dirt, when either actually manipulates this dirt (array), they are *both* accessing the same pile of bags of soil.

