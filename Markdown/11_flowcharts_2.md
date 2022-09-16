## Flowcharting

Flowcharting is another method of displaying or creating an algorithm or pseudo code.  It is a very visual tool, so is most helpful if there is a complex program flow (lots of loops and if conditions)

|Symbols| Used for... |
|--------|-----|
|Square with round corners |Start/Stop - called terminal symbols|
|Small circle | connectors (join lines together) |
|Home plate symbol| off page connector (flowchart continues on another page)|
|Parallelogram| input/output|
|Rectangle| processing code|
|Diamond| for if statement|
|Elongated hexagon| start of loops |
|Rectangle with extra lines on side| calling a function |
|lines| indicates the program flow, from top to bottom or left to right |
|arrows| Indicates program flow, indicated by arrow |



### General Rules about Flowcharts

NOTE: I am not talking about flowgorithm,  you can *execute* flowgorithm charts, but a *real* flowchart is just a diagram.

* Includes a `data dictionary`
  * A list of your variables (use short names if possible), and what they represent.  Also the data type if appropriate
* As much as possible, program flow should start at the top and go down, or to the right (not always possible).  Use arrows instead of lines *only* when the program flow is not down, or to the right.
* Lines indicating program flow should never cross each other (that makes it too confusing)
* A good flowchart should be able to fit on a single page... although *sometimes* it might be necessary to fit on two pages, but **never** three.


## Exercises

**Example IPO:** Calculate pay program   

| Input                                       | Processing                                                   | Output      |
| ------------------------------------------- | ------------------------------------------------------------ | ----------- |
| `Number of hours worked`  `Hourly pay rate` | Multiply the `Number of hours worked` by the `Hourly pay rate` and the result is the `Gross pay` | `Gross pay` |

The processing and the output happen automatically after the input is entered.  

Your job: Create a flowchart (using flowgorithm) or create a detailed algorithm using pseudo code for the above.

*Answer*: Pseudo code:

> START
>
> *// Variables*
>
> Integer/double? HoursWorked, PayRate, GrossPay
>
> Output: "Enter number of hours worked"
>
> Input: HoursWorked
>
> Output: "Enter you pay rate"
>
> Input PayRate
>
> *// Calculate gross pay*
>
> Gross = HoursWorked * PayRate
>
> Output: "Your Gross Pay is " Gross
>
> END



![flowchart of above](../Images/11_example1.png)

**Question:** Should you use integers, or doubles?  

**Question** 

This is an error, why? 

!["if" diagram, where the question is: "What time are you leaving?"](../Images/11_example2.png)

The above is an error because an "if" or decision cannot ask a question. 

 

**Question** 

Is this an error, and if so, why? 

 !["if" diagram, where the question is: "Are you leaving at 2pm or 3pm"](../Images/11_example3.png)

The above is better and more logical 

But still the person could be leaving at 5:00 or 6:00. 

It might be better to ask “Are you leaving after 2:59pm”? 



**Question**

Consider this flowchart excerpt (BTW... this is a `nested if`)

 ![Nested if.  First question is "Are you leaving at 2:00", which branches to the left if false.  This leads to another if "Are you leaving at 3pm", this "if" block branches twice as well, and meets at the bottom of the first if block](../Images/11_example4.png)

Note that the above only does things if the person leaves exactly at 2:00 or 3:00. If they leave at 2:01 nothing might be done as you'll pass on the false ends of the decisions. 

 **Tips**

In General testing for equality may not be the best. We usually test `<`, `<=`, `>`, `>=` these cover a bigger range.  

How would you do things if someone was to leave between 2:00 and 3:00? 



![Better flowchart for the above code, now the flowchart "if" statements ask "is time to leave after 2pm?", and "embedded if" asks "is time to leave before 2pm"](../Images/11_nested_if.png)



**Style**

It is good to pull things that are in common out of "decision branches.  Looking at the flowchart below, we have two output blocks, both which are doing the *exact* same thing.

![Flowchart with simple "if/else", question is "hours<10", the "true" branch has 2 blocks, one is code "Pay=9*hours, the second is an output "your pay is " pay.<br> The false branch has 2 blocks, one is code "Pay = 9*hours+(hours-9)*b", and the second is an output "your pay is pay](../Images/11_duplicate_code.png)

Look at the following flowchart... we have moved the output block out of both the true and false branch, and relocated *one* copy of the output until the *end* of the `if/else` construct.

![Same flowchart as the previous, but there is now only one output block, after the "true" and "false" branch merge together](../Images/11_undo_duplicate_code.png)

