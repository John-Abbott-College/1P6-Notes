# For Loop

For loops are best used when you already know a finite number of times you want to do a loop. 

Example - print 10 aliens across the screen.  Print 3 rows - these are discrete known numbers. 

For loops are not really that useful in the heart of gaming because we "do something - until something else happens" - this is not a known fixed amount or quantity. 

### Syntax

`for (`*`initialize`*` ; `*`condition`*` ; `*`recurring`*) { `code` }

Where the 

* `initialize` is code that gets executed before the loop begins. 
  *  Must be a single statement (i.e. `i = 0;` ok!, `i=0;k=1;` NOT ok!, `i=k=0;` ok!)
* `condition` is used to check when to end the loop (ends if false)
* `recurring` is code that is executed at the end of every loop
  * Must be a single statement
* `code` is the code that gets executed for every loop
  * Is a code block, so as many statements as you want

![Flowchart of a `for loop`. On the printed figure, box 'a' is "i=0", box 'b' is "i<10", box 'c' is "i++", box 'd' is "code"](/Users/compsci/workspace/JAC/1P6/Images/17_for_loop_deconstructed.png)

#### Most common usage

* `initialize`: set a counter to zero, *e.g.* `int i = 0`
* `condition`: set max number of iterations, *e.g.* `i < 10`
* `recurring`: increment the counter, *e.g.* `i++`

**Example**

```csharp
// This is the most common style of a for loop

for (int i=0; i<10; i++) {
  // do some stuff
  Console.WriteLine("i = " + i);
}

// another common style
int j;
for (j = 0; j < 10; j++) {
  Console.WriteLine("j = " + j);
}
Console.WriteLine("Final j value is: " + j);
```

> **Note** that your controlling variable `i` is being controlled entirely by the for loop it is NOT RECOMMENDED that you go `i++` in your loop or alter the variable i. 
>
> You can USE the variable `i`, but do not alter it. Let the for loop do its magic for you.

>  **Note** by declaring `i` inside the for loop (`int i = 0`), the variable `i` is only available to code inside of the if loop, not outside (this refers to `scope` which we will talk about later.)



You can also use for loops in a decreasing manner - like this: 

```csharp
for (int apples = 10; apples > 6 ; apples --) 
{ 
		Console.WriteLine("hello"); 
} 
```

*Question*: How many times is 'hello' printed?

> **NOTE** Always make sure that your loop will end eventually. 
>
> * If you are `decrementing`, then usually your condition will be a `greater than`
> * If you are `incrementing`, then usually your condition will be a `less than`

### Bad examples

**works, but is simply a while loop**

Sometimes you get boneheads at work that leave out parts of the for loop to look cool. Do not do this, even though it would work: 

 ```csharp
int grape = 0; 
// in the for loop, we have no initializer, and no recurring code
// notice that we still need two semi-colons?
for ( ; grape < 3; ) 
{ 
		Console.WriteLine("hello"); 
  	grape ++; 
} 
 ```

The above is awful style. You're using your for loop as if it is a while loop. Do not do this!!! It is not healthy. But……it does work. 



**infinite loop**

Yes, sometimes you see this at work. 

 ```csharp
// there is no initialize, no condition, and no recurring code.
// this is an infinite loop.
// somewhere in the for loop you need to kick me out of this loop (e.g. via 'break')
for (;;) 
{ 
  // bla bla 
  // bla 
}
 ```

### Exercises

**Class Exercise**: Print 10 20 30 40 50 on the screen using a for loop. 

**Class Exercise**: Print the even numbers between 24 and 38 inclusive 

 No you don't have to hand it in. Yes you should be able to do it. Yes, the answers to these are on the next page. 

 Remember - there are many ways of doing this exercise. Your ways may be different than mine. Test your ways, make sure they do what is required. 

# Previous Exercises 

**do if you have time... do anyway! its good for you to practice!**

#### 4) Investment Earnings

The goal of this program is to calculate your investments earnings over a period of a number of years.

**Inputs**: 

* amount of money to invest
* the yearly interest rate 
* the number of years that you want to keep your investment

**Outputs**:

* The month, and the current investment total

**Need to know**:

* To calculate the interest earned for a given month:

$$
interest = current\_total \times \frac{yearly\_interest\_rate}{12\times100}
$$

`interest` = `current_total` * `yearly_interest_rate`/`12.0`/`100.0`

You need to do this calculation month by month (hint, while loop)

#### Optional Requirements

* Tidy up the output by limiting rounding the total money to the nearest penny
* Only output the total money for each year (instead of by each month)

#### 5) CREDIT CARD PAYMENTS

Assume you owe money to a credit card company.

* You can pay your bill all at once, or you can pay anything you want as long as it is equal to or greater than the minimum payment shown on your bill.
* How much does it end up costing you in interest if you only pay the minimum amount per month?
* How much does it end up costing you if you pay a minumum of `x` dollars?

Write a program that will answer these questions

**Inputs**

Assume that user enters valid numbers (i.e. you do not have to verify that the user typed a valid `float`, just assume that they did)

* How much money do you owe?
* What is the yearly interest rate? (NB: in Canada, it varies between 10-18%)
* What is the minimum amount that you can per month (Note that if this is less than what the credit card company calculates, you will have to pay what the credit card company says)

**Outputs**

Month by month:

* Current balance

* Interest

* Payment (the greater of the credit card minimum balance and the minimum balance that the user specified)

* New Balance

Summary:

* The number of years (approx) it takes to pay off your debt
* The total amount paid
* The total amount of interest paid

**Need to Know**

> You will need to find the minimum number between 4 numbers.  You can use `if` statements, are you can google how to find the minimum number in C# (`Math.Min`)

* To calculate interest

$$
interest = balance \times \frac{rate}{12\cdot100}
$$

`interest` = `balance` * `rate` / `12.0` / `100.0`

where 

* `interest` is the interest for this month
* `balance` is the current balance
* `rate` is the yearly interest rate

* To calculate the minimum payment that the credit card company requires:

$$
min\_pay = \min (\frac{fraction}{100} \times (balance + interest), $10, user\_min, balance)
$$

`min_pay` = `Min`(`fraction`/`100.0` * (`balance` + `interest`),  `$10`,  `user_min`,  `balance`)

where 

* `min_pay` is the minimum payment for this month
* `fraction` is the percentage of your balance that needs to be paid (typically 2%)
* `balance` is the current balance
* `interest` is the interest for this month
* `$10` is the minimum that the user must pay, regardless of the balance
* `user_min` is the minimum that the user is willing to pay per month



 