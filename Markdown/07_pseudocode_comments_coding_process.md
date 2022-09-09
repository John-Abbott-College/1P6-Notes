# Pseudo-code, Comments & Coding Process

## Pseudo-Code

When designing code, it can be very useful to **quickly capture your ideas and strategy** before diving into the details or caught-up in syntax.

**Pseudo Code** is a syntax-free language of instructions in English.
Basically you write what you want to do in the correct order. Once your logic is established, it is much easier to convert your pseudo-code into a computer language.

**Example 1**
Pseudo-code to put on shoes in the morning.  

>1. sit up from bed 
> 2. put socks on 
> 3. put shoe on 
> 4. tie shoelaces 

**Example 2**

> 🤖🍴🥜🥪 The robot instructions you wrote to make a peanut-butter sandwich in the first week of the course.

**Example 3**
Huffman Compression Algorithm

> 1. Find all unique letters in the text to be compressed.
> 2. Count how many time each letter is used and create a frequency table.
> 3. Sort the frequency table from lowest frequency to highest frequency
> 4. Group the lowest two frequency occurrences together, combine their frequencies and re-sort the table.
> 5. Construct a partial tree with the combined elements.
> 6. Repeat steps 3 to 4 until there is only one tree
> 7. Create a dictionary by traversing the tree from the top to the desired letter, each left traversal is represented by a 0, and a right traversal is represented by a 1.
> 8. Using the dictionary, create the sequence of zeros and ones to represent the original text

Pseudo-code needs to reflect the **understanding of the audience** on a specific context.

Pseudo-code does not have many rules, its purpose is to **explore the solution** (check for logic errors) before worrying about syntax errors.  It must describe the algorithm in a step-by-step fashion.


## Coding Comments 

In code we can and should include comments. These are not compiled and are invisible to the computer.

Coding comments describe what is going on in the code and explain anything that might not be obvious. 

### What should my comments say?

Comments should explain **_what_ you want to accomplish**, not **_how_ you will accomplish it**.


**Example 1**

```csharp
// Bad comment:

// increase age by 1
age = age + 1
```

```csharp
// Better comment

// In Korea, people define their age by 1 years old at birth,
// so we need to convert European age to Korean age because this program is being used in Korea exclusively.
age = age + 1
```


**Example 2**

```csharp
// Bad comment: it's stating what is being done (the obvious)

nameColumn = tableSize - 2 // subtract 2 from tableSize
```

```csharp
// Better comment: explainming why

// Names are found in the second last column in the table
nameColumn = tableSize - 2 
```


### Who is your audience?

When writing comments, ask yourself "Who will have to read this in the future?"
- Future self?
- Teacher?
- Co-worker?

> **As a general rule**, write comments for a slightly less skilled version of yourself who will be reading the code 1 year from now.


### Comment Syntax

In `C#` we use double-slash `//` to denote comments. Anything between the `//` and the end of the line will be a comment. 

```csharp
// this is a line comment
a = a + 3;    // this is an end of line comment
b = b * 55 // + 35;  <=== this is an error because the "+ 35;" should not be part of the comment!
```

**Styles**

In addition to adding explanations, code comments can help you organize your code and make certain parts more visible.

For example, you can break up code using the equivalent of **headers**, which make it easier to find an important section:

  ```csharp
  // =======================================================
  // this is a major section (most likely a function)
  // =======================================================
  
  // --------------------------------------------------------
  // sub-section ... almost like a paragraph title
  // --------------------------------------------------------
  
  // just a description of what I am doing
  // get user input
  
  ```
  
  It is also recommended to use comments to describe variables whose meaning and use might not be obvious.

```csharp 
// =============================
// Very important code 
// =============================
  
double sigma; // The `uncertainity` of the answer to a least squares fit (statical analyzis)
```


### Block comments

Lets assume that you want to write a very detailed description or explanation in your code, such as a `EULA` (End User's License Agreement),  and you don't want to have to keep adding slashes (`//`).

Comments that span many lines of code can be written as a  **block comments.**

Block comments start with a `/*` (*forward slash* and *star*), followed by one or many lines, and end with `*/`  (*star* and *forward slash*).

```csharp
/*
This code has been written by a very important person, and before yo use this program, you must agree to the following.
	
1. You must name your first child Sandy
    1.1 Alexander or Alexandra is permitted, but additional requirements will be added
2. You never disparage the taste of licorice again.
3. You acknowledge that 'red licorice is not a licorice'!
.... and so on
*/

using System;
namespace Candy
{	class Licorice
    {	static void Main(string[] args)
        {
            Console.Write("Licorice is good! ");
        }
    }
}

```

**Style**

The following is valid commenting, but is considered bad for style since multi-line comments are not required.

```csharp
int tableSize = 9; /* Total number of columns in table */
```

Instead, for an end of line comment, use `//`

```csharp 
int tableSize = 9; // Total number of columns in table
```

**_BLOCK COMMENTS CANNOT EMBED OTHER BLOCK COMMENTS_**

```csharp
// Before
a = b * c; 
a = a/100;  /* block comment on one line */
y = 3;
```

```csharp
// After
/* 
a = b * c; 
a = a/100;  /* block comment on one line */
y = 3;                /// LINE IS NOT COMMENTED OUT
*/				      /// LEAVING THIS LINE AS AN ERROR
```


### Short-cuts for Comments

In Visual Studio there are keyboard shortcuts to help you comment code:

**Comment out the selected lines** button on the Text Editor toolbar. If you prefer to use the keyboard, select **Ctrl**+**K**, **Ctrl**+**C**.

![Showing the button to comment code in the Text Editor toolbar](https://docs.microsoft.com/en-us/visualstudio/get-started/media/vs-2022/tutorial-comment-out.png?view=vs-2022)

**Uncomment the selected lines** button on the Text Editor toolbar. If you prefer to use the keyboard, select **Ctrl**+**K**, **Ctrl**+**U**.

![Showing the button to uncomment code in the Text Editor toolbar](https://docs.microsoft.com/en-us/visualstudio/get-started/media/vs-2022/tutorial-uncomment.png?view=vs-2022)

*Source: [Learn to use the code editor](https://docs.microsoft.com/en-us/visualstudio/get-started/tutorial-editor?view=vs-2022#comment-out-code) by Microsoft.


## Coding Process - Step 1 - Design

Understand the task to be performed, determine logical steps to be taken.

### IPO - Input, Process, Output

Start by creating a chart, detailing what inputs are needed, what you are going to do with those inputs (i.e. process), and what outputs are needed by the user.  

 * What variables are needed, what concept or information is related to the variable, what datatype (`int`, `string`, `double`, `bool`) should they be.

#### Example 1: Calculate pay program.

| Input                                       | Processing                                                   | Output      |
| ------------------------------------------- | ------------------------------------------------------------ | ----------- |
| `Number of hours worked`, `Hourly pay rate` | Multiply the `Number of hours worked` by the `Hourly pay rate` and the result is the `Gross pay` | `Gross pay` |

In this case, the processing and the output would happen automatically after the input is entered.

Your job: Create a detailed algorithm using pseudo code for the problem above.

*Answer in Pseudo code:*

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

**Question:** Should you use integers, or doubles?


#### Example: Calculating Cell Phone Charges

Suppose your cell phone charges you 35 cents for each minute. 

Manual Algorithm (Using pencil and paper, or calculator) 

1. You get the number of minutes that you have used. 
2. You multiply the number of minutes by 0.35. 
3. The result of the calculation is your current charge. 

  

Ask yourself the following questions about this algorithm: 

| *Question:* |  What are the inputs, calculation, and outputs I need for this program? |
| ----------- | ------------------------------------------------------------ |
| *Answer:*   | I need the number of minutes.                                |
| *Question:* | What must I do with the input?                               |
| *Answer:*   | I must multiply the input (the number of minutes) by 0.35. The result of that calculation is the charge |
| *Question:* | What output must I produce?                                  |
| *Answer:*   | The monthly charge                                           |

 
In pseudo code: 

> Output: How many minutes did you use? 
> Input: number of minutes 
> Calculate charge = number of minutes * .35 
> Display the charge 
> Done

