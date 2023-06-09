# Boundary Collision & 2D Arrays 

Let's look at how to manage movement limits when dealing with the Console.

For example:

- Stops a character from moving beyond the limits row and column limits of the console.
- Stop a character from "walking through" a wall.

> This section is mostly a guided exercise, rather than "ready notes".


## Starter Code

Assume the previous chapter's code show in [section ***Simple Example***.](https://john-abbott-college.github.io/1P6-Notes/#/Markdown/33_game_timing?id=a-simple-example)

In particular, let's focus on functions `DrawPlayer` and `MoveAllowed`:

```csharp
// ===============================================================
// Draw player in new position if movement is allowed.
// Function is called by game timer.
// ===============================================================
private static void DrawPlayer(Object source, ElapsedEventArgs e)
{
	char player = 'X';
	// Check that movement is allowed
    
    if (MoveAllowed(row, col, rowMove, colMove))
    {
	    // Erase previous position
        Console.SetCursorPosition(col, row);
        Console.Write(' ');

        // Update new position
        row += rowMove;
        col += colMove;

        // Draw in new position
        Console.SetCursorPosition(col, row);
        Console.Write(player);

        // Stop moving
        rowMove = 0;
        colMove = 0;
        }
    }
}

// ===============================================================
// Returns true if moving in a specific direction is allowed
// ===============================================================
private static bool MoveAllowed(int row, int col, int rowIncrement, int colIncrement)
{
	// yolo, assume everything is possible!
    return true;
}    
```


## Checking for Console Limits

Note the following from the code above:

- Function `DrawPlayer` has an `if-statement` to only draw the player in a new location if the movement is allowed.
- Function `MoveAllowed` receives player's current position (`row`, `col`) and the intended movement direction (`rowMove`, `colMove`) and is supposed to check that the intended movement is allowed.
	- However, it is currently allowing any movement (`return true`).

### Exercise 1: Checking Console Limits

Start with the code from ***Simple Example*** (previous chapter) and refactor function `MoveAllowed` to work properly:

- return `true` if the intended movement will place the player withing the limits of the `Console`.
- return `false` otherwise
	- E.g.: movement would lead the player outside of the `Console`'s valid values for row and column.

Verify your code is correct by trying to crash the program when placing 'X' outside of the Console.


## Building Walls

Some games might have boundaries (such as walls) that are not at the extremities of the Console.

In this case, you will have to create functions to draw these boundaries and keep track of where they are in the "map".

### Using Wall Geometry

The following code creates a wall in the middle of the console, leaving a small passage for the player to walk through.

```csharp
// Define global variables to keep track of wall position
const int wallColPosition = Console.WindowWidth / 2;  // where wall will be drawn
const int passageHeight = 5;  // in rows
const int wallLength = Console.WindowHeight - passageHeight;

// Function to drow wall on Console
private static DrawMiddleWall()
{
	for (int row = 0; row < wallLength; row++)
	{
		Console.SetCursorPosition(wallColPosition, row);
	    Console.Write('█');
	}
}
```

Then the code to check the wall limits would be:

```csharp
// Function checks if new movementwill collide with middle wall
private static bool MoveAllowed(int row, int col, int rowIncrement, int colIncrement)
{
	 // Check for middle wall
     if ((row + rowIncrement < wallLength) && col + colIncrement == wallColPosition) return false;
     else return true;
}
```


### Using 2D Arrays

An alternative method for creating walls is by using 2D arrays to create a "map".

```csharp
static int[,] gameGrid = {
		{1,1,1,1,1},
	    {1,0,0,0,1},
	    {1,0,0,0,1},
	    {1,0,0,0,1},
	    {1,1,1,1,1},
	};
```

In the 2D array above, the number 1 represents a wall, while 0 represents an empty space.

Let's see how to use 2D arrays in c#.

## Intro to 2D Arrays

We've looked at arrays that contain a single data type:
```csharp
// 1D array with 5 int elements
int [] marks = new int[5]  { 99,  98, 92, 97, 95};
```

A 2D array is an array that contains other arrays inside. 

There are 2 types of 2D arrays in C#:
- [Multidimensional Arrays](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/arrays/multidimensional-arrays?source=recommendations)
- [Jagged Arrays](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/arrays/jagged-arrays)

> For simplicity, Multidimensional Arrays are recommended.

Declaring a 2D array:

```csharp
// Declare 2D array with 3 rows and 2 columns (3x2)
// Method 1 - declaration only
int[,] arr2d = new int[3, 2];

// Method 2 - declare and initialise
int[,] arr2d = {
	{ 1, 2 },
	{ 3, 4 },
	{ 5, 6 },
	{ 7, 8 }
};
```

![](https://www.tutorialsteacher.com/Content/images/csharp/twodimensional-array.png)
*Source: [tutorialsteacher.com](https://www.tutorialsteacher.com/csharp/csharp-multi-dimensional-array)*


To access an element inside the array, you must specify both indices: the row and the column

```csharp
Console.Write( arr2d[0,0] )  // Output: 1
Console.Write( arr2d[2,1] )  // Output: 6
```

### Printing with 2D Arrays

Considering again the 2d array previously mentioned:

```csharp
static int[,] gameGrid = {
		{1,1,1,1,1},
	    {1,0,0,0,1},
	    {1,0,0,0,1},
	    {1,0,0,0,1},
	    {1,1,1,1,1},
	};
```

In the 2D array above, the number 1 represents a wall, while 0 represents an empty space.

This array can be printed using the RC pattern with nested for-loops covered in lesson 23:


> **Note**
> The method `array.GetLength(int d)` returns the number of elements in the specified dimension `d` of the Array.
> 
> - Since we are dealing with a 2D array:
> 	- The 1st dimension - `array.Getlength(0)` - is the number of rows in the array.
> 	- The 2nd dimension - `array.Getlength(1)` - is the number of columns in each row.


```csharp
int rowLimit = gameGrid.GetLength(0);
int colLimit = gameGrid.Gellength(1);

for (int row = 0; row < rowLimit; row++)
{
	for (int col = 0; col < colLimit; col++)
	{
		Console.Write( gameGrid[row , col] );
	}
	Console.WriteLine();
} 
```


### Exercise 2: From Numbers to Wall

Use the RC patter above to print the character '█' when there is a 1 inside the grid and an empty character ' ' when there is a 0.

The final result should look like the following:

```text
█████
█   █
█   █
█   █
█████
```


## Boundary Check with 2D Array

If we use the 2D array as "map", we can now re-write the `MoveAllowed` function to check if the future player position would overlap with a `1` inside `gameGrid`.

> All we need to do is check if the intended move would put the character in a grid position containing `1`.
> 
> - You can use the character position `row`, `col` plus the intended increment as the indexes of your game grid.


```csharp
// Function checks if new movement is allowed
private static bool MoveAllowed(int row, int col, int rowIncrement, int colIncrement)
{
	// Check if gameGrid[row + rowIncrement, col + colIncrement] contains 0 or 1
	// If it containes a 1, we have a "collision" with the wall.
}
```



## Resources

<iframe width="560" height="315" src="https://www.youtube.com/embed/G1kYoPr1Ru8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
