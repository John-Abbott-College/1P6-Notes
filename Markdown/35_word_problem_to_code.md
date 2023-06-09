# Converting a word problem to code

When developing a program.

1. Make sure you understand the entire problem to be converted to code
2. Read the requirements carefully
3. What steps do you need to take to accomplish this goal
4. Could this `step` be its own function?
   1. What are its inputs and outputs
   2. Make this function generic, so that it can be reused elsewhere.
   3. Should do one thing, and one thing only
 
   1. create a loop,
   2. or create a function
   3. or both
6. How are these functions going to interact?

NOTE:  If you are using global variables, you probably are doing something wrong, except under very special circumstances!



## Example:

> Design a procedure that **lets the user enter the total rainfall for each month** of a year into an array. You should use additional functions to **calculate and display the total rainfall** for the year (do this entirely in the function), another function to **compute and return the average monthly rainfall** (display the average in your main), and another function to **display the months with the highest and lowest amounts of rain**.

### Parse the above:

* lets the user enter the total rainfall for each month 
* calculate and display the total rainfall
* compute and return the average monthly rainfall
* display the months with the highest and lowest amounts of rain

### Data

* an array of rainfall 
  * each index (an integer between 0 and 11 inclusive) refers to a month
  * each element is the amount of rainfall (either double, or integer)

### Now, lets break it down even further:

* lets the user enter the total rainfall for each month (*create a function*)
  * user must enter data
    * this data must be a `double` or an `int`, and it cannot be less than zero (*create a function*)
  * Must enter 12 separate rainfall amounts
    * *use a loop*
    * But must also specify which month the rainfall is for
      * Convert loop counter to month (*create a function*)
  * must keep information about the total rainfall
    * *create an array* for storing all the rainfall amounts
  * other steps require this data, so:
    * *return rainfall amounts*
* calculate and display the total rainfall (*create a function*)
  * what info do we need? The amount of rainfall for each month
    * *input: rainfall array*
  * display the total
    * *need to use an accumulator*
  * Print the output in this function, or in the calling function?
    * if displaying the total in the calling function, then...
      * *must return total rainfall*
* compute and return the average monthly rainfall (*create a function*)
  * what info do we need? The total rainfall
    * so either recalculate total, or call the function that calculates the total
    * that function requires the rainfall array, therefore
    * *input: rainfall array*
  * Print the output in this function, or in the calling function?
    * if displaying the average in the calling function, then...
      * *must return average rainfall*
* display the months with the highest and lowest amounts of rain (*create a function*)
  * what info do we need? The amount of rainfall for each month
    * *input: rainfall array*
  * need to calculate the minimum and maximum amount of rain
    * *use standard calculations for minimum / maximum* (another function maybe?)

### Create a top level look at how things are called and used

**Entry Point**

1. Call function **`A`** that asks user to enter rainfall amounts, save data in an array (`rainfall`?)
2. Call function **`B`** that calculates the total rainfall (have this function return the total)
   1. Pass in the rainfall array
   2. Save the total
   3. Print to screen
3. Call function **`C`** that computes and return the average monthly rainfall
   1. Pass in the rainfall array
   2. Save the average
   3. Print to screen
4. Call function **`D`**that display the months with the highest and lowest amounts of rain 
   1. Pass in the rainfall array
   2. Do not want to use globals, so returning highest and lowest amounts of rain AND their months would be difficult, so let that function do the printing

### Flesh out Details about the Functions

Function `A`:

* Input: nothing
* Output: rainfall
* Loop:
  * Calls:
    * Function to read in numbers
    * Function that converts numbers to months

Function `B`:

* Input: rainfall
* Returns: total
* Prints: nothing

Function `C`:

* Input: rainfall
* Call Function `B` to get the total
* Calculate the average
* Returns: average

Function `D`:

* Input: rainfall
* calculates highs and lows
* Calls function that converts integer into month name
* Prints info
* Returns: nothing

