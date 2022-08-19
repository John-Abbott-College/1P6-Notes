# Boolean Algebra 

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

### `bool` data type (C#)

In C# there is a data type that we have not yet looked at.  The data type allows us to represent the logic values `true` and `false`.

We use **variables** of type `bool` to represent elements of our situation or procedure. Variables may take one of only two values. Traditionally this would be `true` or `false` **- nothing else**. So for instance we may have a variable **`is_raining`** and state that this represents if it is raining outside or not. The value of **`is_raining`** would be : 

- **`true`** if it is raining outside. 
- **`false`** if it is not raining outside. 

**Example**: 

- **`is_raining`** represents if it is raining outside or not. 
- **`work_completed`** represents if I have completed my work or not. 
- **`should_run`** represents if I go for a run or not. 

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
| ⋀      | `&&`| AND       |
| ⋁      | `||` |OR        |
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

