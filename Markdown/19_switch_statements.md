# Switch Statements

In C#, the switch statement offers an alternative to `if-statements`. It offers a more concise syntax that is easier to maintain.

Below is the standard structure of a switch statement:

```csharp
switch(expression) 
{
	case x:
	    // code block
	    break;
	case y:
	    // code block
	    break;
	case y:
	    // code block
	    break;
	default:
	    // code block
	    break;
}
```

> The details of how the switch statement works are well explained in the two resources below:
>
> - [C# Switch Statements by W3Schools](https://www.w3schools.com/cs/cs_switch.php)
>
> - [The `switch` statement by Microsoft's C# reference](https://learn.microsoft.com/en-US/dotnet/csharp/language-reference/statements/selection-statements#the-switch-statement)

## Error: cannot fall out of switch

The error below is very common while writing `switch` statements:

> Error: Control cannot fall out of switch from final case label

This typically means that you are missing a `break;` line below a `case` statement.

Example:

```csharp
string color = "red";
switch(color) 
{
	case "blue":
	    // code block
	    break;
	case "red":
	    // code block missing break line!
	default:
	    // code block
	    break;
}
```

## Examples

The program below prompts the student for a percent grade and displays the equivalent letter grade.

A version of this program **written with if statements** was shown to you in lesson 10 on week 4 of the course:

```csharp
int gradePercent;
string letterResult;

Console.WriteLine("Please enter your grade %");
gradePercent = int.Parse( Console.ReadLine() );

Console.Write("Letter grade is: ");

if (gradePercent >= 90)
{
	letterResult = "A";
}
else if (gradePercent >= 75)
{
	letterResult = "B";
}
else if ( gradePercent >= 60)
{
	letterResult = "C";
}
else
{
	letterResult = "F";
}

Console.WriteLine( letterResult );
```

The same program could be written **with `switch` statements**:

```csharp
int gradePercent;
string letterResult;

Console.WriteLine("Please enter your grade %");
gradePercent = int.Parse( Console.ReadLine() );

Console.Write("Letter grade is: ");

switch (gradePercent)
{
    case >= 90:
        letterResult = "A";
        break;
    case >= 75:
        letterResult = "B";
        break;
    case >= 60:
        letterResult = "C";
        break;
    default:
        letterResult = "F";
        break;
}

Console.WriteLine( letterResult );
```
