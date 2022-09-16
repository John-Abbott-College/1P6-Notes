# Boolean Algebra (cont)



## Three Logical Boolean Algebra

If you have three propositions in your logic (`P`, `Q` and `R`), you should follow the pattern shown below: 

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

> **definiton** ([wikipedia](https://en.wikipedia.org/wiki/Contradiction)) It is a proposition that is unconditionally false (i.e., a self-contradictory proposition).

How do we know if we have a contradiction?  Sometimes it is a matter of simply seeing the logical fallacy, but sometimes it can be challenging to discern.

Lets look at a simple **example**:

```csharp
// remember '&&' means 'and'
if (lives < 0 && lives > 10 ) {
  // do something
}
```

Assume for the moment that you cannot see the contradiction.  Next step create a truth table... mmm... but how?

* Look for a value of `lives` such that the first part of the condition `lives < 0` is true, and `lives > 10` is false, likewise for `true - false`, `false - true`, `true - true`

  | lives | `lives < 0` | `lives > 10` | `lives < 0` `and` `lives > 10` |
  | ----- | ----------- | ------------ | -------------------------- |
  | 5     | F           | F            | F   |
  | -5    | T           | F            | F   |
  | 15    | F           | T            | F   |
  | ???   | T           | T            | ... I cannot find a number where this is true |



Another **example**

```csharp
if (a > b && a < 10 && b > 11) {
  // do something
}
```
* Look for a values of `a`, `b`  such that the you look at all combinations of `true`,`false`, for each comparison (`a>b` etc)

	| a    | b    | `a>b` | `a<10` | `b>11` | `a>b && a<10` | `a>b && a<10 && b>11`                                        |
	| ---- | ---- | ----- | ------ | ------ | ------------- | ------------------------------------------------------------ |
	| 3    | 2    | T     | T      | F      | T             | F                                                            |
	| 14   | 13   | T     | F      | T      | F             | F                                                            |
	| 9    | 13   | F     | T      | T      | F             | F                                                            |
	| 11   | 10   | T     | F      | F      | F             | F                                                            |
	| 7    | 8    | F     | T      | F      | F             | F                                                            |
	| 15   | 17   | F     | F      | T      | F             | F                                                            |
  | 10   | 11   | F     | F      | F      | F             | F                                                            |
	| ??   | ??   | T     | T      | T      |               | I cannot find a combination of numbers<br>so that all conditions are true |



**_Never leave a contradiction `if` statement in your code !!!_**



## Tautology

> **definition** ([wikipedia]()) In mathematical logic, a **tautology** (from Greek (: ταυτολογία) is a formula or assertion that is true in every possible interpretation. An example is "x=y or x≠y"

How do we know if we have a tautology?  Sometimes it is a matter of simply seeing the logical fallacy, but sometimes it can be challenging to discern.

**Example**:

```csharp
// remember that "||" is "or"
if (score < 10 || score >= 10) {
	//do something
}
```

Lets make a truth table for this

| score | `score < 10` | `score >= 10` | `score < 10 or score >= 10`                          |
| ----- | ------------ | ------------- | ---------------------------------------------------- |
| 9     | T            | F             | T                                                    |
| 11    | F            | T             | T                                                    |
| 10    | F            | T             | T (always test 'edge' conditions)                    |
| ??    | T            | T             | Can't find a score that is true for both conditions  |
| ??    | F            | F             | Can't find a score that is false for both conditions |

**example** - is this a tautology?

```csharp
// remember that the && condition has to be evaluated first!
if (a > b || a < 10 && b > 11) {
  // do something
}
```

* Look for a values of `a`, `b`  such that the you look at all combinations of `true`, `false`, for each comparison (`a>b` etc)

  | a    | b    | `a>b` | `a<10` | `b>11` | `a<10 && b>11` | `a>b || (a<10 && b>11)` |
  | ---- | ---- | ----- | ------ | ------ | -------------- | ----------------------- |
  | 3    | 2    | T     | T      | F      | F              | T                       |
  | 14  | 13   | T     | F      | T      | F              | T                       |
  | 9    | 13   | F     | T      | T      | T              | T                       |
  | 11   | 10   | T     | F      | F      | F              | T                       |
  | 7    | 8    | F     | T      | F      | F              | F                       |
  | 15   | 17   | F     | F      | T      | F              | F                       |
  | 10   | 11   | F     | F      | F      | F             | F |
  | ??   | ??   | T     | T      | T      |                |                         |



**example** - is this tautology?

```csharp
if (a <= b || a => 10 || b <= 11) {
  // do something
}
```

* Look for a values of `a`, `b`  such that the you look at all combinations of `true`,`false`, for each comparison (`a>b` etc)

  | a    | b    | `a<=b` | `a>=10` | `b<=11` | `a<=b || a<=10` | `a<=b || a>=10 || b<=11` |
  | ---- | ---- | ------ | ------- | ------- | --------------- | ------------------------ |
  | 3    | 2    | F      | F       | T       | F               | T                        |
  | 14   | 13   | F      | T       | F       | T               | T                        |
  | 9    | 13   | T      | F       | F       | T               | T                        |
  | 11   | 10   | F      | T       | T       | T               | T                        |
  | 7    | 8    | T      | F       | T       | T               | T                        |
  | 15   | 17   | T      | T       | F       | T               | T                        |
  | 10   | 11   | T      | T       | T       | T               | T                        |
  | ??   | ??   | F      | F       | F       |                 |                          |



**_Never leave a tautology `if` statement in your code !!!_**

 

## Short Circuit (in programming logic)

Computers like to do the minimum amount of work as necessary to get the job done.

### `P or Q` Logic

If you have a logic statement with two conditions separated by an `or` (example: `a<0 || a<100`), 

```csharp
if (a<10 || a>30) {
  // execute this block of code if above evaluates to true
}
```

The computer will evaluate your logic in the following manner:
1. Establish that your statement includes an 'or'
2. Evaluate `a<10`
   1. If this is **`true`**, it doesn't matter what the other comparison evaluates to, because `true` `or` *anything* is **always** `true`... so jump to the `if block` of code.'
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
   1. If this is **`false`**, it doesn't matter what the other comparison evaluates to, because `false` `and` *anything* is **always** `false`... so jump to the end of the`if block` of code (do *not* execute the `if block`.'
   2. If this is `true`, then we need to carry on, because we don't know the final result of the `if` statement
3. Evaluate `a<30`
   1. if `true` execute block of code
   2. if `false` don't execute block of code.

### Programming efficient code

Good news - the compiler will probably compile this in a way that it does this efficiently. 

However, 

* when using an `or` construct, if possible, put the comparison that is mostly likely to be true as the first condition, so the second one does not have to be evaluated, and
* when using an `and` construct, if possible, put the comparison that is most likely to be false as the first condition, so the second one does not have to be evaluated.

## Material Implication

This is the "If this then that" concept, or "this implies that".

> The **material conditional** (also known as **material implication**) is an operation commonly used in logic. *...*  a formula $ P\rightarrow Q$ is true unless $P$ is true and $Q$ is false. ([wikipedia](https://en.wikipedia.org/wiki/Material_conditional))

We use the arrow to show `P implies Q` ( $P\rightarrow Q$ ).

Note that this logic does not necessarily translate well to natural languages, but we are going to try to give it a go...

> Due to the paradoxes of material implication and related problems, material implication is not generally considered a viable analysis of conditional sentences in natural language. ([wikipedia](https://en.wikipedia.org/wiki/Material_conditional))

Lets say 

* P - did you feed me?
* Q - I am fed?

Then

| P (you fed me) | Q (I have been fed) | comment                                                      | Result |
| -------------- | ------------------- | ------------------------------------------------------------ | ------ |
| yes            | yes                 | you fed me `implies` I have been fed?                        | True   |
| yes            | no                  | you fed me `implies` I have *not* been fed?                  | False  |
| no             | yes                 | **you haven't fed me `implies` I have been fed?<br>This is where English breaks down... I may have been fed by someone else, so the answer is true** | True   |
| no             | no                  | you haven't fed me `implies` I have *not* been fed?          | True   |

#### Implication Truth Table

| P    | Q    | P `implies` Q |
| ---- | ---- | ------------- |
| T    | T    | T             |
| T    | F    | F             |
| F    | T    | T             |
| F    | F    | T             |

Another quote from wikipedia justifies why translating this truth table into English is not really possible to do.

> Material implication does not closely match the usage of conditional sentences in natural language. For example, even though material conditionals with false antecedents are vacuously true, the natural language statement "If 8 is odd, then 3 is prime" is typically judged false. Similarly, any material conditional with a true consequent is itself true, but speakers typically reject sentences such as "If I have a penny in my pocket, then Paris is in France". These classic problems have been called the paradoxes of material implication. In addition to the paradoxes, a variety of other arguments have been given against a material implication analysis. For instance, counterfactual conditionals would all be vacuously true on such an account.

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

Show that $(P \rightarrow Q) \or (Q \rightarrow P)$ ( (P `implies` Q) `or` (Q `implies` P) ) is a **tautology**

To find the answer, create a truth table

| P    | Q    | P `implies` Q | Q `implies` P | P `implies` Q) `or` (Q `implies` P) |
| ---- | ---- | ------------- | ------------- | ----------------------------------- |
| T    | T    | T             | T             | T                                   |
| T    | F    | F             | T             | T                                   |
| F    | T    | T             | F             | T                                   |
| F    | F    | T             | T             | T                                   |

**Class exercise** (10 minutes)

Construct the truth table for $(P \rightarrow Q) \and (Q \rightarrow P): $  ( *(P `implies` Q) `and` (Q `implies` P)* )

Is it a *tautology* or *contradiction* or is it *valid* logical statement?

*Answer*: After we have done this in class, you can go to the next example.)

| P    | Q    | P `implies` Q | Q `implies` P | P `implies` Q) `and` (Q `implies` P) |
| ---- | ---- | ------------- | ------------- | ------------------------------------ |
| T    | T    | T             | T             | T                                    |
| T    | F    | F             | T             | F                                    |
| F    | T    | T             | F             | F                                    |
| F    | F    | T             | T             | T                                    |

**Class exercise**

Construct the truth table for $(P\rightarrow (Q\or R) ) \and R$ : ( *( P `implies` (Q `or` R) ) `and` R* )

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

Didn't get the above right? Or you only had four rows - don't panic. Re-read the notes, re do the above exercise and get it.  

Only when you get the above entirely 100% and understand it….. Then you can do the OPTIONAL 

**Optional Homework** (DeMorgan's Laws)

Note: test questions will look like this, so although you don't have to do the following, you *do not* have to hand this in.

1. Show that $P\rightarrow Q$ and $\neg P \or Q$ are logical equivalent ( (P `implies` Q) `is equivalent to`(`not`P `or`  Q) )
2. Show that $\neg (P \and Q) \leftrightarrow (\neg P \or \neg Q)$: ( `not`(P `and` Q) `is equivalent to` (`not` P `or` `not` Q) )
3. Show that $\neg(\neg P) \leftrightarrow P$: ( `not` ( `not` P) `is equivalent to` P ) 



## Three Logical Boolean Algebra

If you have three propositions in your logic (`P`, `Q` and `R`), you should follow the pattern shown below: 

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

> **definiton** ([wikipedia](https://en.wikipedia.org/wiki/Contradiction)) It is a proposition that is unconditionally false (i.e., a self-contradictory proposition).

How do we know if we have a contradiction?  Sometimes it is a matter of simply seeing the logical fallacy, but sometimes it can be challenging to discern.

Lets look at a simple **example**:

```csharp
// remember '&&' means 'and'
if (lives < 0 && lives > 10 ) {
  // do something
}
```

Assume for the moment that you cannot see the contradiction.  Next step create a truth table... mmm... but how?

* Look for a value of `lives` such that the first part of the condition `lives < 0` is true, and `lives > 10` is false, likewise for `true - false`, `false - true`, `true - true`

  | lives | `lives < 0` | `lives > 10` | `lives < 0` `and` `lives > 10` |
  | ----- | ----------- | ------------ | -------------------------- |
  | 5     | F           | F            | F   |
  | -5    | T           | F            | F   |
  | 15    | F           | T            | F   |
  | ???   | T           | T            | ... I cannot find a number where this is true |



Another **example**

```csharp
if (a > b && a < 10 && b > 11) {
  // do something
}
```
* Look for a values of `a`, `b`  such that the you look at all combinations of `true`,`false`, for each comparison (`a>b` etc)

	| a    | b    | `a>b` | `a<10` | `b>11` | `a>b && a<10` | `a>b && a<10 && b>11`                                        |
	| ---- | ---- | ----- | ------ | ------ | ------------- | ------------------------------------------------------------ |
	| 3    | 2    | T     | T      | F      | T             | F                                                            |
	| 14   | 13   | T     | F      | T      | F             | F                                                            |
	| 9    | 13   | F     | T      | T      | F             | F                                                            |
	| 11   | 10   | T     | F      | F      | F             | F                                                            |
	| 7    | 8    | F     | T      | F      | F             | F                                                            |
	| 15   | 17   | F     | F      | T      | F             | F                                                            |
  | 10   | 11   | F     | F      | F      | F             | F                                                            |
	| ??   | ??   | T     | T      | T      |               | I cannot find a combination of numbers<br>so that all conditions are true |



**_Never leave a contradiction `if` statement in your code !!!_**



## Tautology

> **definition** ([wikipedia]()) In mathematical logic, a **tautology** (from Greek (: ταυτολογία) is a formula or assertion that is true in every possible interpretation. An example is "x=y or x≠y"

How do we know if we have a tautology?  Sometimes it is a matter of simply seeing the logical fallacy, but sometimes it can be challenging to discern.

**Example**:

```csharp
// remember that "||" is "or"
if (score < 10 || score >= 10) {
	//do something
}
```

Lets make a truth table for this

| score | `score < 10` | `score >= 10` | `score < 10 or score >= 10`                          |
| ----- | ------------ | ------------- | ---------------------------------------------------- |
| 9     | T            | F             | T                                                    |
| 11    | F            | T             | T                                                    |
| 10    | F            | T             | T (always test 'edge' conditions)                    |
| ??    | T            | T             | Can't find a score that is true for both conditions  |
| ??    | F            | F             | Can't find a score that is false for both conditions |

**example** - is this a tautology?

```csharp
// remember that the && condition has to be evaluated first!
if (a > b || a < 10 && b > 11) {
  // do something
}
```

* Look for a values of `a`, `b`  such that the you look at all combinations of `true`, `false`, for each comparison (`a>b` etc)

  | a    | b    | `a>b` | `a<10` | `b>11` | `a<10 && b>11` | `a>b || (a<10 && b>11)` |
  | ---- | ---- | ----- | ------ | ------ | -------------- | ----------------------- |
  | 3    | 2    | T     | T      | F      | F              | T                       |
  | 14  | 13   | T     | F      | T      | F              | T                       |
  | 9    | 13   | F     | T      | T      | T              | T                       |
  | 11   | 10   | T     | F      | F      | F              | T                       |
  | 7    | 8    | F     | T      | F      | F              | F                       |
  | 15   | 17   | F     | F      | T      | F              | F                       |
  | 10   | 11   | F     | F      | F      | F             | F |
  | ??   | ??   | T     | T      | T      |                |                         |



**example** - is this tautology?

```csharp
if (a <= b || a => 10 || b <= 11) {
  // do something
}
```

* Look for a values of `a`, `b`  such that the you look at all combinations of `true`,`false`, for each comparison (`a>b` etc)

  | a    | b    | `a<=b` | `a>=10` | `b<=11` | `a<=b || a<=10` | `a<=b || a>=10 || b<=11` |
  | ---- | ---- | ------ | ------- | ------- | --------------- | ------------------------ |
  | 3    | 2    | F      | F       | T       | F               | T                        |
  | 14   | 13   | F      | T       | F       | T               | T                        |
  | 9    | 13   | T      | F       | F       | T               | T                        |
  | 11   | 10   | F      | T       | T       | T               | T                        |
  | 7    | 8    | T      | F       | T       | T               | T                        |
  | 15   | 17   | T      | T       | F       | T               | T                        |
  | 10   | 11   | T      | T       | T       | T               | T                        |
  | ??   | ??   | F      | F       | F       |                 |                          |



**_Never leave a tautology `if` statement in your code !!!_**

 

## Short Circuit (in programming logic)

Computers like to do the minimum amount of work as necessary to get the job done.

### `P or Q` Logic

If you have a logic statement with two conditions separated by an `or` (example: `a<0 || a<100`), 

```csharp
if (a<10 || a>30) {
  // execute this block of code if above evaluates to true
}
```

The computer will evaluate your logic in the following manner:
1. Establish that your statement includes an 'or'
2. Evaluate `a<10`
   1. If this is **`true`**, it doesn't matter what the other comparison evaluates to, because `true` `or` *anything* is **always** `true`... so jump to the `if block` of code.'
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
   1. If this is **`false`**, it doesn't matter what the other comparison evaluates to, because `false` `and` *anything* is **always** `false`... so jump to the end of the`if block` of code (do *not* execute the `if block`.'
   2. If this is `true`, then we need to carry on, because we don't know the final result of the `if` statement
3. Evaluate `a<30`
   1. if `true` execute block of code
   2. if `false` don't execute block of code.

### Programming efficient code

Good news - the compiler will probably compile this in a way that it does this efficiently. 

However, 

* when using an `or` construct, if possible, put the comparison that is mostly likely to be true as the first condition, so the second one does not have to be evaluated, and
* when using an `and` construct, if possible, put the comparison that is most likely to be false as the first condition, so the second one does not have to be evaluated.

## Material Implication

This is the "If this then that" concept, or "this implies that".

> The **material conditional** (also known as **material implication**) is an operation commonly used in logic. *...*  a formula $ P\rightarrow Q$ is true unless $P$ is true and $Q$ is false. ([wikipedia](https://en.wikipedia.org/wiki/Material_conditional))

We use the arrow to show `P implies Q` ( $P\rightarrow Q$ ).

Note that this logic does not necessarily translate well to natural languages, but we are going to try to give it a go...

> Due to the paradoxes of material implication and related problems, material implication is not generally considered a viable analysis of conditional sentences in natural language. ([wikipedia](https://en.wikipedia.org/wiki/Material_conditional))

Lets say 

* P - did you feed me?
* Q - I am fed?

Then

| P (you fed me) | Q (I have been fed) | comment                                                      | Result |
| -------------- | ------------------- | ------------------------------------------------------------ | ------ |
| yes            | yes                 | you fed me `implies` I have been fed?                        | True   |
| yes            | no                  | you fed me `implies` I have *not* been fed?                  | False  |
| no             | yes                 | **you haven't fed me `implies` I have been fed?<br>This is where English breaks down... I may have been fed by someone else, so the answer is true** | True   |
| no             | no                  | you haven't fed me `implies` I have *not* been fed?          | True   |

#### Implication Truth Table

| P    | Q    | P `implies` Q |
| ---- | ---- | ------------- |
| T    | T    | T             |
| T    | F    | F             |
| F    | T    | T             |
| F    | F    | T             |

Another quote from wikipedia justifies why translating this truth table into English is not really possible to do.

> Material implication does not closely match the usage of conditional sentences in natural language. For example, even though material conditionals with false antecedents are vacuously true, the natural language statement "If 8 is odd, then 3 is prime" is typically judged false. Similarly, any material conditional with a true consequent is itself true, but speakers typically reject sentences such as "If I have a penny in my pocket, then Paris is in France". These classic problems have been called the paradoxes of material implication. In addition to the paradoxes, a variety of other arguments have been given against a material implication analysis. For instance, counterfactual conditionals would all be vacuously true on such an account.

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

Show that $(P \rightarrow Q) \or (Q \rightarrow P)$ ( (P `implies` Q) `or` (Q `implies` P) ) is a **tautology**

To find the answer, create a truth table

| P    | Q    | P `implies` Q | Q `implies` P | P `implies` Q) `or` (Q `implies` P) |
| ---- | ---- | ------------- | ------------- | ----------------------------------- |
| T    | T    | T             | T             | T                                   |
| T    | F    | F             | T             | T                                   |
| F    | T    | T             | F             | T                                   |
| F    | F    | T             | T             | T                                   |

**Class exercise** (10 minutes)

Construct the truth table for $(P \rightarrow Q) \and (Q \rightarrow P): $  ( *(P `implies` Q) `and` (Q `implies` P)* )

Is it a *tautology* or *contradiction* or is it *valid* logical statement?

*Answer*: After we have done this in class, you can go to the next example.)

| P    | Q    | P `implies` Q | Q `implies` P | P `implies` Q) `and` (Q `implies` P) |
| ---- | ---- | ------------- | ------------- | ------------------------------------ |
| T    | T    | T             | T             | T                                    |
| T    | F    | F             | T             | F                                    |
| F    | T    | T             | F             | F                                    |
| F    | F    | T             | T             | T                                    |

**Class exercise**

Construct the truth table for $(P\rightarrow (Q\or R) ) \and R$ : ( *( P `implies` (Q `or` R) ) `and` R* )

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

Didn't get the above right? Or you only had four rows - don't panic. Re-read the notes, re do the above exercise and get it.  

Only when you get the above entirely 100% and understand it….. Then you can do the OPTIONAL 

**Optional Homework** (DeMorgan's Laws)

Note: test questions will look like this, so although you don't have to do the following, you *do not* have to hand this in.

1. Show that $P\rightarrow Q$ and $\neg P \or Q$ are logical equivalent ( (P `implies` Q) `is equivalent to`(`not`P `or`  Q) )
2. Show that $\neg (P \and Q) \leftrightarrow (\neg P \or \neg Q)$: ( `not`(P `and` Q) `is equivalent to` (`not` P `or` `not` Q) )
3. Show that $\neg(\neg P) \leftrightarrow P$: ( `not` ( `not` P) `is equivalent to` P ) 


