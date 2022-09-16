# Boolean Algebra 

## Intro to Boolean Algebra

There are instances where we need to test for a mix conditions. For example:

1. Both birth-day **AND** birth-month must match the current day to declare a birthday.
2. The oil in the car should be changed every 6 months **OR** every 5,000 km.
3. To return a new sweater you must have the receipt **AND NOT** remove the price tag.

The combination of **AND**, **OR**, and **NOT** conditions is called boolean algebra or boolean logic.

### Example 1

The program *BirthdayCalculator* prompts the user for their birth-month and birth-day. The program reads the current date from the system and informs the user if it's their birthday.

*Pseudo Code*



- boolean OR and AND
	- Examples:
		- Give birthday example
`if (birthMonth == currentMonth) && (birthDay == currentday)`

Show them how to get system time.
```csharp
// Get local system Time.
DateTime localTime = DateTime.Now;

// System time includes:
// day, day of week, month, year, hour, minutes, and more...

Console.WriteLine($@"
	Day: {localTime.Day}
	Day of week: {localTime.DayOfWeek}
	Month: {localTime.Month}
	Year: {localTime.Year}
	Hour: {localTime.Hour}
	Minutes: {localTime.Minute}
");
```



With the exception of `DayOfWeek`, all of the date values show above are of type `Int32`. Do note that `DayOfWeek` can be easily converted to `string` with:

```csharp
DateTime localTime = DateTime.Now;

string weekDayString = Convert.ToString( localTime.DayOfWeek );
Console.WriteLine(weekDayString);
```

- Writing a bot that brings the recycling bin outside:
	- It's Wed and the bin is not empty;
	- `if (weekDay == "Wednesday") && (binNotEmpty)`





What is boolean algebra?

**Short Answer**: Arithmetic operations and/or rules based on `true`/`false` logic.

**Long Answer** (from [wikipedia](https://en.wikipedia.org/wiki/Boolean_algebra))

> In [mathematics](https://en.wikipedia.org/wiki/Mathematics) and [mathematical logic](https://en.wikipedia.org/wiki/Mathematical_logic), **Boolean algebra** is the branch of [algebra](https://en.wikipedia.org/wiki/Algebra) in which the values of the [variables](https://en.wikipedia.org/wiki/Variable_(mathematics)) are the [truth values](https://en.wikipedia.org/wiki/Truth_value) *true* and *false*, usually denoted 1 and 0, respectively.[[1\]](https://en.wikipedia.org/wiki/Boolean_algebra#cite_note-:0-1) Instead of [elementary algebra](https://en.wikipedia.org/wiki/Elementary_algebra), where the values of the variables are numbers and the prime operations are addition and multiplication, the main operations of Boolean algebra are the [conjunction](https://en.wikipedia.org/wiki/Logical_conjunction) (*and*) denoted as ∧, the [disjunction](https://en.wikipedia.org/wiki/Logical_disjunction) (*or*) denoted as ∨, and the [negation](https://en.wikipedia.org/wiki/Negation) (*not*) denoted as ¬. It is thus a formalism for describing [logical operations](https://en.wikipedia.org/wiki/Logical_operation), in the same way that elementary algebra describes numerical operations.

## Boolean Logic in CompSci

Why study boolean logic at all?

Once we dive into logic programming, we will see a lot of math statements using `P` and `Q` and `X` and `Y` and `AND` and `OR` statements.  But why are we doing this? What's going on? What does this have to do with programming???? 

Answer: a lot. 

Consider the following piece of pseudo code 

> if the game score is less than 100 and more than 275 then
>
> ​	add 1 to the number of lives 
>
> end if

You can code this. You will *never* get a syntax error, nor will you get any other type of error. 

*What is wrong with this logic?* 

​	No matter what you do, the number of lives never increases.

*Do you understand why?*

By studying Boolean Algebra, we can begin to "look for" and analyze these types of logical errors. This is very important to understand when making decisions in our code via `if/else` statements, but also in datababase courses (3rd semester?) when you are searching for specific data in a database.

## Example 1: ShouldRun?

The program helps a user decide if they should go for a run or not.

- **`is_raining`** represents if it is raining outside or not. 
- **`work_completed`** represents if I have completed my work or not. 
- **`should_run`** represents if user should go for a run or not. 

The above "questions" you can ask the user during the run of the program and store their answers in their appropriate variables. These answers will be some combination of trues and falses based on the user's choice and input. 

```csharp
// declare our variables
bool is_raining;
bool work_completed;
bool should_run;
string answer;

// get input
Console.Write("It is raining [Y/N] ");
answer = Console.ReadLine();
is_raining = answer == "Y";

Console.Write("It your work completed? [Y/N] ");
answer = Console.ReadLine();
work_completed = answer == "Y";

// should we run now, true or false
// our work is completed and it is not raining
should_run = work_completed && !is_raining;

// ... rest of code ... 

```

 

## Basic Operations

| MATH   |C#| operation |
| ------ |--| --------- |
| ⋀      | `&&`| AND      |
| ⋁     | `||`| OR      |
| $\neg$ | `!`| NOT       |

![Three separate Venn diagrams. The first (x and y) shows two circles labeled x and y respectively, the two circles overlap, and where the two circles overlap, the diagram is coloured in red. The second (x or y) shows tow circles labeled x and y respectively, the two circles overlap. All of the x circle and all of the y circle is coloured in red. The third diagram shows only one circle, labeled x, surrounded by a square.  Everything outside of the circle, but still inside the square, is coloured red.](../Images/09_and_or_not.png)

**Figure 1** : Diagram displaying the Venn diagram of `AND`, `OR`, and `NOT`.  

### `AND` Operation

We use the upside down 'v' (`⋀`) symbol to mean `AND` so 

`x AND y` is written as `x ⋀ y` 

**Example**

| English|Math|C#|
|----|----|---|
|Supper is *pizza* and *coke* | $ supper = pizza \and coke $ | `supper = pizza && coke;` |

So, we send our friend out to get supper, and they come back with two items. 

**Do we have supper?**

Let's construct a table for all of the possible options

| bought pizza? | bought coke? | is it the supper that I wanted? |
| ------------- | ------------ | ------------------------------- |
| yes           | yes          | yes                             |
| yes           | no           | no                              |
| no            | yes          | no                              |
| no            | no           | no                              |

#### `AND` Truth Table

To generalize the `AND` operation, we will construct a `truth table` for $x \and y$, where $x$ and $y$ are either `true` (T) or `false` (F).

> Remember the Coke and Pizza example - you need both for me to be happy!
>
> $x$ is "Bought Pizza"
>
> $y$ is "Bought Coke" 
>
> * the only way to shut me up is to get me both! 
>
> So the only circumstance where we get this to happen when both x and y are true - you got pizza, and you got Coke, so this is the ONLY situation where I am happy. 

| $x$   | $y$   | $x\and y$ |
| ----- | ----- | --------- |
| **T** | **T** | **T**     |
| T     | F     | F         |
| F     | T     | F         |
| F     | F     | F         |



### `OR` Operator

`x OR y` is written as `x ⋁ y` 

**Example**

| English                   | Math                          | C#                          |
| ------------------------- | ----------------------------- | --------------------------- |
| Drink is Rootbeer or Coke | $ drink = rootbear \or coke $ | `drink = rootbeer || coke;` |

So, we send our friend out to get pizza and drinks.  They come back with pizza and a drink.

**Do we have have what we want?**

Let's construct a table for all of the possible options

| bought rootbeer? | bought coke? | is it the drink that I wanted? |
| ---------------- | ------------ | ------------------------------ |
| yes              | yes          | yes                            |
| yes              | no           | yes                            |
| no               | yes          | yes                            |
| no               | no           | no                             |

#### `OR` Truth Table

To generalize the `OR` operation, we will construct a `truth table` for $x \or y$, where $x$ and $y$ are either `true` (T) or `false` (F).

> Remember the Rootbeer or Coke example - you only need either one for me to be happy!
>
> $x$ is "Bought Rootbeer"
>
> $y$ is "Bought Coke" 
>
> So the circumstances where I am happy is when either x or y are true.

| $x$   | $y$   | $x\and y$ |
| ----- | ----- | --------- |
| **T** | **T** | **T**     |
| **T** | F     | **T**     |
| F     | **T** | **T**     |
| F     | F     | F         |

### `NOT` Operator

`NOT x` is written as $\neg x$ 

**Example**

| English              | Math                   | C#                 |
| -------------------- | ---------------------- | ------------------ |
| Drink is *not* Pepsi | $ drink = \neg pepsi $ | `drink = ! pepsi;` |

So, we send our friend out to get pizza and drinks.  They come back with pizza and a drink.

**Do we have have what we want?**

Let's construct a table for all of the possible options

| bought pepsi? |  is it the drink that I wanted? |
| ------------- | ------------------------------ |
| yes           |  no                            |
| no            | yes                             |

#### `NOT` Truth Table

To generalize the `NOT` operation, we will construct a `truth table` for $\neg x$, where $x$  is either `true` (T) or `false` (F).

> Remember the not Pepsi example - As long as you didn't buy Pepsi, I am happy!
>
> $x$ is "Bought Pepsi"
>

| $x$   | $\neg x$ |
| ----- |  --------- |
| **T** |  F     |
| F     | **T**     |



## Order of Operations

Of course, you can mix `AND`, `OR` and `NOT` operations, so it is important to know the order in which they will be evaluated.

The order of operations for Boolean algebra, from highest to lowest priority is NOT, then AND, then OR. Expressions inside brackets are always evaluated first.

**Examples**:

$x=true, y=false, z=false$. 

**Example:**  $x$ `or` $y$ `and` $z$ versus ($x$ `or` $y$) `and` $z$

|  | comment                   |
| ----------------------------- | ------------------------- |
| $true \or false \and false$ | to do: evaluate the `AND` ($false \and false$) |
| $true \or false$              | to do: evaluate the `OR` ($true\or false$) |
| $true$                        | final result |



|  | comment                   |
| ----------------------------- | ------------------------- |
| $(true \or false) \and false$ | to do: evaluate inside brackets (`OR` ($true \or false$)) |
| $(true) \and false$              | to do: evaluate the `AND` ($true \and false$) |
| $false$                        | final result |

**Example:**  `not` $x$ `and` $y$ `or` $z$ versus `not` ($x$ `and` $y$ `or` $z$)

|                                  | comment                                        |
| -------------------------------- | ---------------------------------------------- |
| $\neg true \and false \or false$ | to do: evaluate the `NOT` ($\neg true$)        |
| $false \and false \or false$     | to do: evaluate the `AND` ($false \and false$) |
| $false \or false$                | to do: evaluate the `OR` ($false \or false$)   |
| $false$                          | final result                                   |



|                                  | comment                            |
| -------------------------------- | ---------------------------------- |
| $\neg (true \and false \or false)$ | to do: bracket first   |
| $\neg (true \and false \or false)$     | to do: evaluate the `AND` ($true \and false$) |
| $\neg (false \or false)$                | to do: evaluate the `OR` ($false \or false$) |
| $\neg (false)$                          | to do: evaluate the `NOT` ($\neg false$) |
| $true$ | final result |

## Negating `AND` and `OR`s

A common situation in computer science happens when we have a logical statement that we want to use in an `if construct` that is opposite of what we want.

**Example**

```csharp
// Example of BAD CODING!
if (x==10 && y==5) {
}
else {
  Console.WriteLine("yay!");
}
```
```csharp
// It works, but is kinda hard to read!
if (! (x==10 && y==5) ) {
}
else {
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

Lets compare the truth tables for `NOT`( $x$ `AND` $y$) and  `NOT`$x$ `OR`  `NOT`$y$)

**Truth Table for `NOT`( $x$ `AND` $y$)**

| $x$  | $y$  | $x \and y$ | $\neg(x \and y)$ |
| ---- | ---- | ---------- | ---------------- |
| T    | T    | T          | F                |
| T    | F    | F          | T                |
| F    | T    | F          | T                |
| F    | F    | F          | T                |

**Truth Table for `NOT` $x$ `OR` `NOT`$y$**

| $x$  | $y$  | $\neg x$| $\neg y$ |$\neg x \or \neg y$ |
| ---- | ---- | ----    | -------- |--------------------|
| T    | T    | F       | F        | F                  |
| T    | F    | F       | T        | T                  |
| F    | T    | T       | F        | T                  |
| F    | F    | T       | T        | T                  |



**BOTH TRUTH TABLES HAVE THE SAME RESULTS !!! **

>  $\neg (x \and y) = \neg x \or \neg y$



So, what is the equivalent logic of 

```csharp
if (!(x==10 && y==5 ))
```
Answer:
```csharp
if (x != 10 || y != 5)
```

## Student Exercise

Prove, using truth tables, that

> $\neg (x \or y) = \neg x \and \neg y$

