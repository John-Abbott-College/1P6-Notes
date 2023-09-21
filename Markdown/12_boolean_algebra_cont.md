# Boolean Algebra - Part 2

## Three Logical Boolean Algebra

If there are three propositions in your logic (`P`, `Q` and `R`), to evaluate all possible combinations, it is recommended that you follow the pattern shown below:

| P    | Q    | R    |
| ---- | ---- | ---- |
| F    | F    | F    |
| F    | F    | T    |
| F    | T    | F    |
| F    | T    | T    |
| T    | F    | F    |
| T    | F    | T    |
| T    | T    | F    |
| T    | T    | T    |

If you replace all the `F` with `0` and the `T` with `1` you will see a binary count from (top) `000` all the way to the bottom `111`. Which is the range of 0 to 7.  

`0` - `000`<br>`1` - `001`<br>`2` -`010`<br>`3` - `011`<br>`4` - `100`<br>`5` - `101`<br>`6` - `110`<br>`7` - `111`

Note this is 8 possible outcomes. Strongly recommended you follow the pattern above 

## Contradictions

> **A contradiction** is a proposition that is unconditionally false.
> In other words, a self-contradictory proposition. - ([wikipedia](https://en.wikipedia.org/wiki/Contradiction))

How do we know if we have a contradiction?

Sometimes it's easy to see the logical fallacy, however, for complex expressions it can be hard and we might need to breakdown the expression using **truth tables**.

### Example 1

```csharp
// remember '&&' means 'and'
if (lives < 0 && lives > 10 )
{
  // do something
}
```

Assume for the moment that you cannot see the contradiction.  Next step create a truth table:

* Look for a value of `lives` such that the first part of the condition `lives < 0` is true, and `lives > 10` is false, likewise for `true - false`, `false - true`, `true - true`

  | lives | `lives < 0` | `lives > 10` | `lives < 0` `and` `lives > 10` |
  | ----- | ----------- | ------------ | -------------------------- |
  | 5     | F           | F            | F   |
  | -5    | T           | F            | F   |
  | 15    | F           | T            | F   |
  | ???   | T           | T            | ... cannot find a number where this is true |

Conclusion: it is a contradiction.

### Example 2

Evaluate if the expression below is a contradiction.

```csharp
if (a > b && a < 10 && b > 11)
{
  // do something
}
```

* Look for values of `a` and  `b`  in order to cover all possible combinations of the expressions:
	* `a > b`
	* `a < 10`
	* `b > 11`

;<br>

| a    | b    | `a>b` | `a<10` | `b>11` | `a>b && a<10` | `a>b && a<10 && b>11`                                        |
| ---- | ---- | ----- | ------ | ------ | ------------- | ------------------------------------------------------------ |
| 3    | 2    | T     | T      | F      | T             | F                                                            |
| 14   | 13   | T     | F      | T      | F             | F                                                            |
| 9    | 13   | F     | T      | T      | F             | F                                                            |
| 11   | 10   | T     | F      | F      | F             | F                                                            |
| 7    | 8    | F     | T      | F      | F             | F                                                            |
| 15   | 17   | F     | F      | T      | F             | F                                                            |
| 10   | 11   | F     | F      | F      | F             | F                                                            |
| ??   | ??   | T     | T      | T      |               | Cannot find a combination of numbers so that all conditions are true |


> **Never leave a contradiction `if` statement in your code !_**



## Tautology

> **Tautology** is a formula or assertion that is true in every possible interpretation.<br>
> In other words, the expression is redundant and unnecessary because it is always true.
> Such as the expression (x=y or x≠y).


### Example 3

Evaluate if the expression below is a tautology.

```csharp
// remember that "||" is "or"
if (score < 10 || score >= 10)
{
	//do something
}
```

With the truth table below:

| score | `score < 10` | `score >= 10` | `score < 10 or score >= 10`                          |
| ----- | ------------ | ------------- | ---------------------------------------------------- |
| 9     | T            | F             | T                                                    |
| 11    | F            | T             | T                                                    |
| 10    | F            | T             | T (always test 'edge' conditions)                    |
| ??    | T            | T             | Can't find a score that is true for both conditions (not a possibility)  |
| ??    | F            | F             | Can't find a score that is false for both conditions (not a possibility) |

Conclusion: It is a tautology. For all possible values of score, the expression is always true.

### Example 4

Evaluate if the expression below is a tautology.

```csharp
// remember that the && condition has to be evaluated first!
if (a > b || a < 10 && b > 11)
{
  // do something
}
```

* Look for a values of `a`, `b`  such that the you look at all combinations of `true`, `false`, for each comparison (`a>b` etc)

| a   | b   | `a>b` | `a<10` | `b>11` | `a<10 && b>11` | `a>b \|\| (a<10 && b>11)` |
| --- | --- | ----- | ------ | ------ | -------------- | ----------------------- |
| 3   | 2   | T     | T      | F      | F              | T                       |
| 14  | 13  | T     | F      | T      | F              | T                       |
| 9   | 13  | F     | T      | T      | T              | T                       |
| 11  | 10  | T     | F      | F      | F              | T                       |
| 7   | 8   | F     | T      | F      | F              | F                       |
| 15  | 17  | F     | F      | T      | F              | F                       |
| 10  | 11  | F     | F      | F      | F              | F                       |
| ??  | ??  | T     | T      | T      |                |                         |

Conclusion: it is not a tautology. There are possible values for a and b that make the expression `false`.


> **_Never leave a tautology `if` statement in your code !_**

 

## Short Circuit (in programming logic)

Computers like to do the minimum amount of work as necessary to get the job done.

### `P or Q` Logic

If you have a logic statement with two conditions separated by an `or` (example: `a<0 || a<100`), 

```csharp
if (a<10 || a>30)
{
  // execute this block of code if above evaluates to true
}
```

The computer will evaluate your logic in the following manner:

1. Establish that your statement includes an 'or'
2. Evaluate `a<10`
   1. If this is **`true`**, it doesn't matter what the other comparison evaluates to, because `true` `or` *anything* is **always** `true`... so jump to the `if code block` (short circuit).
   2. If this is `false`, then we need to carry on, because we don't know the final result of the `if` statement
3. Evaluate `a<30`
   1. if `true` execute block of code
   2. if `false` don't execute block of code.

### `P and Q` Logic

If you have a logic statement with two conditions separated by an `and` (example: `a>100 && a<10`), 

```csharp
if (a>10 && a<30) {
  // execute this block of code if above evaluates to true
}
```

The computer will evaluate your logic in the following manner:

1. Establish that your statement includes an 'and'
2. Evaluate `a>10`
   1. If this is **`false`**, it doesn't matter what the other comparison evaluates to, because `false` `and` *anything* is **always** `false`... so jump to the end of the`if block` of code and do *not* execute the `if block` (short circuit).
   2. If this is `true`, then we need to carry on, because we don't know the final result of the `if` statement
3. Evaluate `a<30`
   1. if `true` execute block of code
   2. if `false` don't execute block of code.

### Programming efficient code

* When using an `or` construct, whenever possible, put the comparison that is mostly likely to be true as the first condition, so the second one does not have to be evaluated.
* When using an `and` construct, if possible, put the comparison that is most likely to be false as the first condition, so the second one does not have to be evaluated.

## Material Implication

 **Material conditional** (also known as **material implication**) uses the arrow notation to show that `P implies Q` ( $P\rightarrow Q$ ).

> $P\rightarrow Q$ is true unless $P$ is true and $Q$ is false.


Note that this logic does not necessarily translate well to natural languages such as English.

> Due to the paradoxes of material implication and related problems, material implication is not generally considered a viable analysis of conditional sentences in natural language. ([wikipedia](https://en.wikipedia.org/wiki/Material_conditional))

#### Implication Truth Table

| P    | Q    | P `implies` Q |
| ---- | ---- | ------------- |
| T    | T    | T             |
| T    | F    | F             |
| F    | T    | T             |
| F    | F    | T             |


## Equivalence

$P \leftrightarrow Q$ means that P and Q are equivalent.  So the double implication is `True` if P and Q are both `True` or if P and Q are both `false`; otherwise, the double impliction is false.

Truth table:

| P    | Q    | P `is equivalent to` Q |
| ---- | ---- | ---------------------- |
| T    | T    | T                      |
| T    | F    | F                      |
| F    | T    | F                      |
| F    | F    | T                      |

It is controversial whether or not the relationship $P \leftrightarrow Q$ can be properly rendered by the English '*if and only if* ' .

## Exercises

**Exercise 1**

Show that $(P \rightarrow Q) \lor (Q \rightarrow P)$ 

*Equivalent in English:* ( (P `implies` Q) `or` (Q `implies` P) ) is a **tautology**

To find the answer, create a truth table

| P    | Q    | P `implies` Q | Q `implies` P | P `implies` Q) `or` (Q `implies` P) |
| ---- | ---- | ------------- | ------------- | ----------------------------------- |
| T    | T    | T             | T             | T                                   |
| T    | F    | F             | T             | T                                   |
| F    | T    | T             | F             | T                                   |
| F    | F    | T             | T             | T                                   |

Therefore it is a tautology.


**Exercise 2**

Construct the truth table for: $(P \rightarrow Q) \and (Q \rightarrow P)$

*Equivalent in English:* (P `implies` Q) `and` (Q `implies` P)

Is it a *tautology* or *contradiction* or is it *valid* logical statement?

*Answer*: It is not a tautology (some `false` results), and not a contradiction (some `true` results). Therefore it is a valid statement.

| P    | Q    | P `implies` Q | Q `implies` P | (P `implies` Q) `and` (Q `implies` P) |
| ---- | ---- | ------------- | ------------- | ------------------------------------ |
| T    | T    | T             | T             | T                                    |
| T    | F    | F             | T             | F                                    |
| F    | T    | T             | F             | F                                    |
| F    | F    | T             | T             | T                                    |


**Exercise 3**

Construct the truth table for $(P\rightarrow (Q\lor R) ) \land R$
*English*:  *( P `implies` (Q `or` R) ) `and` R* 

Answer: 

| P    | Q    | R|Q `or` R | P `implies` (Q `or` R) | (P `implies` (Q `or` R) ) `and` R |
| ---- | ---- | -------- | ---------------------- | --------------------------------- |--|
| T | T | T | T | T |T|
| T | T | F | T | T |F|
| T | F | T | T | T |T|
| T | F | F | F | F |F|
| F | T | T | T | T |T|
| F | T | F | T | T |F|
| F | F | T | T | T |T|
| F | F | F | F | T |F|


**Optional Homework** (DeMorgan's Laws)

Note: test questions will look like this, so although you don't have to do the following, you *do not* have to hand this in.

1. Show that $P\rightarrow Q$ and $\neg P \lor Q$ are logical equivalent ( (P `implies` Q) `is equivalent to`(`not`P `or`  Q) )
2. Show that $\neg (P \land Q) \leftrightarrow (\neg P \lor \neg Q)$: ( `not`(P `and` Q) `is equivalent to` (`not` P `or` `not` Q) )
3. Show that $\neg(\neg P) \leftrightarrow P$: ( `not` ( `not` P) `is equivalent to` P )


