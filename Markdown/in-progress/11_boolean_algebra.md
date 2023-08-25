# Boolean Algebra 

## Intro to Boolean Algebra

There are instances where we need to test for a multiple boolean conditions at the same time. For example:

1. Both birth-day **AND** birth-month must match the current day to declare a birthday.
2. The oil in the car should be changed every 6 months **OR** every 5,000 km.
3. To return a new sweater you must have the receipt **AND NOT** remove the price tag.

The combination of **AND**, **OR**, and **NOT** conditions with the boolean values `true` and `false` is called boolean algebra (or boolean logic).

Reading and writing proper boolean algebra is **important to design accurate and efficient code with proper logic** (ex. good `if` statements).


## Boolean logic & Computer Science

Consider the following piece of pseudo code for giving a player extra lives:

> If the game score is less than 100 points and more than 275 points then:
>
> - add 1 to the number of lives.


A programmer can implement this code *never* get a syntax error, however, this code will not work. *What is wrong with this logic?* 

- No matter what you do, the number of lives never increases. The two boolean conditions are contradictory and will never happen simultaneously.

By studying Boolean Algebra, developers can begin to "look for" and analyze these types of logical errors. This is particularly important when making decisions in code via `if/else` statements, and when manipulating and querying data in databases (3rd semester course).


## Basic Operations

The basic logic operations are AND, OR, and NOT.
Each has a special notation in math and in C#.

| MATH | C#     | Operation | Description                             |
| ---- | ------ | --------- | --------------------------------------- |
| ⋀    | `&&`   | AND       | True when all elements are true.        |
| ⋁    | `\|\|` | OR        | True when at least one element is true. |
| ¬    | `!`    | NOT       | The inverse of an element.              | 

![Three separate Venn diagrams. The first (x and y) shows two circles labeled x and y respectively, the two circles overlap, and where the two circles overlap, the diagram is coloured in red. The second (x or y) shows tow circles labeled x and y respectively, the two circles overlap. All of the x circle and all of the y circle is coloured in red. The third diagram shows only one circle, labeled x, surrounded by a square.  Everything outside of the circle, but still inside the square, is coloured red.](../Images/09_and_or_not.png)

**Figure 1** : Diagram displaying the Venn diagram of `AND`, `OR`, and `NOT`.  

### `AND` Operation

We use the upside down 'v' (`⋀`) symbol for `AND`

`x AND y` is written as `x ⋀ y` 

**Example**

For a meal to be considered a "special", a client must by a pizza and a drink.

| English|Math|C#|
|:----:|:----:|:---:|
|Special is a pizza *AND* drink | special = pizza $\land$ drink | `special = pizza && drink;` |

**Do we have a special?**

Let's construct a table for all of the possible options

| bought pizza? | bought drink? | is it a Special? |
|:-------------:|:-------------:|:----------------:|
|      yes      |      yes      |       yes        |
|      yes      |      no       |        no        |
|      no       |      yes      |        no        |
|      no       |      no       |        no        |


#### `AND` Truth Table

To generalize the `AND` operation, we will construct a **truth table** for x AND y (is it a special?), where x and y are either `true` (T) or `false` (F).

> x is "Bought Pizza"
>
> y is "Bought Drink" 
>
> So the only circumstance where we get this to happen when both x and y are true.

|   x   |   y   | x $\land$ y |
|:-----:|:-----:|:-----:|
| **T** | **T** | **T** |
|   T   |   F   |   F   |
|   F   |   T   |   F   |
|   F   |   F   |   F   |

Legend: T = True, F = False

### `OR` Operator

`x OR y` is written as `x ⋁ y` 

**Example**

|           English           |          Math           |              C#               |
|:---------------------------:|:-----------------------:|:-----------------------------:|
| Drink is Rootbeer *OR* Coke | drink = rootbeer ⋁ coke | `drink = rootbeer \|\| coke;` |

So, we send our friend out to get pizza and drinks.  They come back with pizza and a drink.

**Do we have a drink?**

Let's construct a table for all of the possible options

| bought rootbeer? | bought coke? | is it a drink? |
| ---------------- | ------------ | ------------------------------ |
| yes              | yes          | yes                            |
| yes              | no           | yes                            |
| no               | yes          | yes                            |
| no               | no           | no                             |

#### `OR` Truth Table

To generalize the `OR` operation, we will construct a **truth table** for x OR y, where x and y are either `true` (T) or `false` (F).

> Remember the Rootbeer or Coke example - you only need either one.
>
> x is "Bought Rootbeer"
>
> y is "Bought Coke" 


|  $x$  |  $y$  | x ⋁ y |
|:-----:|:-----:|:-----:|
| **T** | **T** | **T** |
| **T** |   F   | **T** |
|   F   | **T** | **T** |
|   F   |   F   |   F   |

### `NOT` Operator

`NOT x` is written as ¬ x

This operator transforms the variable into **its opposite**. It's also know as **negation**.

**Example**

Juices are more expensive and are not considered a drink. Therefore, to qualify for a "special", **you must not get juice** with your meal.

| English              | Math                   | C#                 |
| -------------------- | ---------------------- | ------------------ |
| Drink is *NOT* juice | drink = ¬ juice | `drink = ! juice;` |

If we send a friend out to get pizza and drinks, **do we qualify for a special**?

Let's construct a table for all of the possible options

| bought juice? | is it a drink? |
|:-------------:|:--------------:|
|      yes      |       no       |
|      no       |      yes       |

#### `NOT` Truth Table

To generalize the `NOT` operation, we will construct a truth table for ¬ x, where x is either `true` (T) or `false` (F).

> Remember the not juice example.
>
> $x$ is "Bought drink"
>

|   x   |  ¬ x  |
|:-----:|:-----:|
| **T** |   F   |
|   F   | **T** |



## Example 2: ShouldRun

The program `ShouldRun` below helps a user decide if they should go for a run or not.

- **`isRaining`** represents if it's raining outside or not. 
- **`workCompleted`** represents if user has completed their work or not. 
- **`shouldRun`** represents if user should go for a run or not.

User should go for a run if the work is completed and it's not raining.

The above "questions" are asked during the program execution and stored in the appropriate variables.

The final answer will be a combination of trues and falses based on the user's input. 

```csharp
// declare variables
bool isRaining;
bool workCompleted;
bool shouldRun;
string answer;

// get inputs
Console.WriteLine("It is raining [Y/N] ");
answer = Console.ReadLine();
isRaining = answer == "Y";

Console.WriteLine("It your work completed? [Y/N] ");
answer = Console.ReadLine();
workCompleted = answer == "Y";

// User should run if work is completed AND it's NOT raining
shouldRun = workCompleted && !isRaining;

if(shouldRun)
{
	Console.WriteLine("You should run!");
}
else
{
	Console.WriteLine("You can't go running");
}
```

Note the boolean expression `shouldRun = workCompleted && !isRaining`
 

### Example 3: BirthdayChecker

The program *BirthdayChecker* prompts the user for their birth-month and birth-day. The program reads the current date from the system and informs the user if it's their birthday.

*Inputs & Outputs*
> **Inputs**:
> - User's birth-day and birth-month.
> - Current day and month from system's calendar.
> **Outputs**:
> - Confirmation message with yes or no for birthday.

*Pseudo Code*
> Ask user for their birth-day and their birth-month.<br>
> Get current month and day from system's calendar.<br>
> **Check that:**
>	- Current month is the same as user's birth-month?
>	- AND
>	- Current day is the same as user's birth-day?
> **If yes:**
>	- Display "Happy birthday" message.
> **If no:**
>	- Display "Sorry, your birthday" message

But how do we get the system's current day? 🤔

## System's DateTime

We can ask the operating system for the current date using C#.
The current date is available as a `DateTime` object that must be declared before it can be used:

```csharp
// Get system time at the moment the object variable is declared.
DateTime systemTime = DateTime.Now;

// System time includes:
// day, day of week, month, year, hour, minutes, and more...

Console.WriteLine($@"
	Day: {systemTime.Day}
	Day of week: {systemTime.DayOfWeek}
	Month: {systemTime.Month}
	Year: {systemTime.Year}
	Hour: {systemTime.Hour}
	Minutes: {systemTime.Minute}
");
```

| DateTime variable    | Data type | Value range                   |
| -------------------- | --------- | ----------------------------- |
| systemTime.Day       | `Int32`   | 1 to 31                       |
| systemTime.DayOfWeek | `string`  | "Monday", "Tuesday", ... ,  "Friday" |
| systemTime.Month     | `Int32`   | 1 to 12                       |
| systemTime.Year      | `Int32`   | 2023 (current year)           |
| systemTime.Hour      | `Int32`   | 0 to 24                       |
| systemTime.Minute    | `Int32`   | 0 to 59                       |

As illustrated in the table above, with the exception of `DayOfWeek`, all of the date values show above are of type `Int32`. 

Note that `DayOfWeek` can be easily converted to `string` with:

```csharp
DateTime localTime = DateTime.Now;

string weekDayString = Convert.ToString( localTime.DayOfWeek );
Console.WriteLine(weekDayString);
```

### Example 3: BirthdayChecker (Con't)

Now that we know how to get the systems' time, we can implement *BirthdayChecker*.

*Code*
```csharp
// Declaring multiple variables of the same type in one line
int dayInput, monthInput, systemDay, systemMonth;
string messageOutput;

Console.Write("Please enter your birth-day: ");
dayInput = int.Parse( Console.ReadLine() );
Console.Write("Please enter your birth-month: ");
monthInput = int.Parse( Console.ReadLine() );

// Get system time
DateTime systemTime = DateTime.Now;
systemDay = systemTime.Day;
systemMonth = systemTime.Month;
// Output system time to verify that values make sense
Console.WriteLine($"Today's day: {systemDay}, and month: {systemMonth}");

// Check if user's birth day and month match system's date
if( (dayInput == systemDay) && (monthInput == systemMonth) )
{
    messageOutput = "Congrats! It's your birthday!";
}
else
{
    messageOutput = "Not your birthday yet";
}
Console.WriteLine(messageOutput);
```


## Order of Operations

Similarly to traditional algebra, we can mix the `AND`, `OR` and `NOT` operations. When doing so, we must know the order in which they will be evaluated.

The order of operations for Boolean algebra, **from highest to lowest priority** is:
1. NOT
2. AND
3. OR

Expressions **inside brackets** are always **evaluated first**.

### Order Examples

Use the following values for the examples below:

$x=true, y=false, z=false$.

<br>

**Example 1:**  x `or` y `and` z versus (x `or` y) `and` z

*Evaluating x `or` y `and` z*

|                   | Order of operating                                 |
| --------------------------- | --------------------------------------- |
| true `or` false `and` false | evaluate the `and` false `and` false)   |
| *true* `or` *false*         | evaluate the `or` (*true* `or` *false*) |
| *true*                      | final result                            |

<br>

*Evaluating (x `or` y) `and` z*

|                                     | Order of operating                                                   |
| ----------------------------------- | --------------------------------------------------------- |
| (*true* `or` *false*) `and` *false* | evaluate inside brackets (*true* `or` *false*)) |
| (*true*) `and` *false*                 | evaluate the `and` (*true* `and` *false*)             |
| *false*                             | final result                                              |

<br>

**Example 2:**  `not` $x$ `and` $y$ `or` $z$ versus `not` ($x$ `and` $y$ `or` $z$)

*Evaluating `not` $x$ `and` $y$ `or` $z$*

|                                   | Order of operating                                      |
| --------------------------------- | -------------------------------------------- |
| `not` true `and` false `or` false | evaluate the `NOT` ($\neg true$)             |
| false `and` false `or` false      | evaluate the `and` (false `and` false)       |
| false `or` false                  | evaluate the `or` (false `or` false) |
| $false$                           | final result                                 |

<br>

Evaluating `not` ($x$ `and` $y$ `or` $z$)

|                                     | Order of operating                       |
| ----------------------------------- | ---------------------------------------- |
| `not` (true `and` false `or` false) | bracket first                            |
| `not` (true `and` false `or` false) | evaluate the `and` (true `and` false)    |
| `not` (false `or` false)            | evaluate the `or` (false `or` false)     |
| `not` (false)                       | evaluate the `NOT` ($\neg false$) |
| $true$                              | final result                             |

## Negating `AND` and `OR`s

A common situation in computer science happens when we have a logical statement that we want to use in an `if construct` that is opposite of what we want.

**Example**

We want to print `yay!` only if x is not 10 and y is not 5.

```csharp
// BAD code: doing nothing if a boolean condition is met
if (x==10 && y==5)
{
	// do nothing on purpose
}
else
{
  Console.WriteLine("yay!");
}
```
```csharp
// It works, but is kinda hard to read!
if (! (x==10 && y==5) )
{
	Console.WriteLine("yay!");
}
```

```csharp
// An attempt to fix above code, 
// but the logic is WRONG!
if (x != 10 && y != 5) {
  Console.WriteLine("yay!");
}
```

Why is the above logic wrong?

Lets compare the truth tables for `NOT`( $x$ `AND` $y$) and compare to `NOT`$x$ `OR`  `NOT`$y$

**Truth Table for `NOT`( $x$ `AND` $y$)**

| $x$ | $y$ | $x \land y$ | $\neg(x \land y)$ |     | 
| --- |:---:|:-----------:|:-----------------:|:---:|
| T   |  T  |      T      |         F         |     |
| T   |  F  |      F      |         T         |     |
| F   |  T  |      F      |         T         |     |
| F   |  F  |      F      |         T         |     |

**Truth Table for `NOT` $x$ `OR` `NOT`$y$**

| $x$ | $y$  | $\neg x$ | $\neg y$ | $\neg x \lor \neg y$ |
| ---- | :----: | :----:    | :--------: | :--------------------: |
| T    | T    | F       | F        | F                  |
| T    | F    | F       | T        | T                  |
| F    | T    | T       | F        | T                  |
| F    | F    | T       | T        | T                  |

<br>

**Both truth tables have the same results!**

Conclusion:

> **English**<br>
>  &emsp;
>  `not` (x `and` y) is the same as `not` x `or` `not` y
>  
> **Math**<br>
> &emsp;
> $\neg (x \land y) = \neg x \lor \neg y$
>   
> **C#**<br>
> &emsp;
> `!(x && y) == !x || ! y`
>  



Therefore, the equivalent logic of: 

```csharp
if (!(x==10 && y==5 ))
```

is:
```csharp
if (x != 10 || y != 5)
```

## Exercise

Prove, using truth tables, that

> $\neg (x \lor y) = \neg x \land \neg y$

