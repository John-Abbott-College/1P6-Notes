# In Class Work

Note for next year, this was so much harder for the students than I thought.

## 1) MAX_MIN

Given a list of numbers, find and output the minimum number and maximum numbers.
* The maximum number will never by larger than 1000, the minimum number will never be below -1000

**Inputs**

* -number of numbers that you want to enter

**Outputs**

* the maximum and minimum number

**Sample Output**
`Max is: 93 Min is: -11`

## 2) MAX_MIN - BETTER

Same as above, but write the code such that there is no known lower or upper limit.  In other words, your code will work with *any* data.

## 3) STATISTICS
> NOTE: The students don't know lists or arrays yet!!!!!!

Given a list of numbers, find and output the minimum number and maximum numbers.

* The maximum number will never by larger than 1000, the minimum number will never be below -1000

**Inputs**

* -number of numbers that you want to enter

**Outputs**

* the total and the average number

**Need to Know**

* Insert the following line of code into your own code
  `my_list = [5, -3, 21, 2, 93, -11, 67, 9]`

* The formula for the average of n numbers is:
$$
  \frac{\sum_{i=1}^n x_i}{n}
$$
For the non-math students... Take the total of all the numbers, and divide by the number of numbers.

**Sample Output**
`Total: 183, Average: 22.875`

## 4) Investment Earnings

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

`interest` = `current_total` * `yearly_interest_rate`/12.0/100.0

You need to do this calculation month by month (hint, while loop)

#### Optional Requirements

* Tidy up the output by limiting rounding the total money to the nearest penny
* Only output the total money for each year (instead of by each month)

## 5) CREDIT CARD PAYMENTS

Assume you owe money to a credit card company.

* You can pay your bill all at once, or you can pay anything you want as long as it is equal to or greater than the minimum payment shown on your bill.
* How much does it end up costing you in interest if you only pay the minimum amount per month?
* How much does it end up costing you if you pay a minumum of `x` dollars?

Write a program that will answer these questions

**Inputs**

Assume that user enters valid numbers (i.e. you do not have to verify that the user typed a valid `float`, just assume that they did)

* How much money do you owe?
* What is the yearly interest rate? (NB: in Canada, it varies between 10-18%)
* What is the minimum amount that you can per month (Note that if this is less than what the c redit card company calculates, you will have to pay what the credit card company says)

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

`interest` = `balance` * `rate` / 12.0 / 100.0

where 

* `interest` is the interest for this month
* `balance` is the current balance
* `rate` is the yearly interest rate

* To calculate the minimum payment that the credit card company requires:

$$
min\_pay = \min(\frac{fraction}{100} \times (balance + interest), $10, user\_min, balance)
$$

`min_pay` = min(`fraction`/100.0 * (`balance` + `interest`),  \$10,  `user_min`,  `balance`)

where 

* `min_pay` is the minimum payment for this month
* `fraction` is the percentage of your balance that needs to be paid (typically 2%)
* `balance` is the current balance
* `interest` is the interest for this month
* `$10` is the minimum that the user must pay, regardless of the balance
* `user_min` is the minimum that the user is willing to pay per month

