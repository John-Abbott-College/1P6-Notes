# Console Game Programming Techniques 

This section will introduce best practices and basic techniques for developing console games using C#.

Concepts covered:

1. Program Flow for Console Games.
2. Use of Global Variables.
3. Processing Key Strokes.


## General Program Flow

Below is a common program flow for your Main function.

1. Do the initial variable setup and display things that will only be shown once.
2. Use a function that processes key strokes in a continuous while loop.
3. Update global variables according to key strokes (or other user interaction).
4. Use a 'draw' function that gets called when there is movement or periodically with a timer (explained next class).
	- Only redraw what is necessary (the areas of the console that have changed).
	- How often it gets called is the 'frame rate' (how often you want to update game elements).


```csharp  
// ===============================================================
// Global Variables
// ===============================================================
static bool gameover = false;

// keeping track of location
static int row = 0;      // current row position
static int col = 0;      // current collumn position

// ===============================================================
// Entry point
// ===============================================================
static void Main(string[] args)
{
	ShowHelp();

    // initialize the game

    Console.Clear();
	// initial position in the middle of the console
	row = Console.WindowHeight / 2;
    col = Console.WindowWidth / 2;
    // make the cursor invisible. See next sections
    Console.CursorVisible = false;

    // play the game
    while (!gameover)
    {
	    ProcessKeyStrokes();
		Draw();
    }
}
```


## Global Variables

**Global variables are strongly discouraged in modern programming.** 

> Without using object orientated programming (OOP) you will have no choice other than using global variables.
> **Keep the use of global variables to a minimum, only when strictly necessary.** 


## Processing Key Strokes

Normally, when data is entered into a program, the program does not receive the input *until* the `ENTER` key is pressed.

In game programming, that is not practical and we'll learn how to **read the keys being pressed while the program is running**.

### `ReadKey()`

This function will immediately return the key that you typed on the keyboard, without having to follow by pressing the `ENTER` key.

Look at the documentation for [ReadKey](https://docs.microsoft.com/en-us/dotnet/api/system.console.readkey?view=net-5.0) . Notice that the return type of `ReadKey` is [ConsoleKeyInfo](https://docs.microsoft.com/en-us/dotnet/api/system.consolekeyinfo?view=net-5.0).  (see examples to understand how to use it).

#### Comparing keystrokes

There are have two options::
- Comparing the character that was typed (Ex.: "a", "w", "s", "d").
- Comparing the actual key that was hit.

It is recommended that you compare the `key` as there is no distinction between 'Q' and 'q', for example.

#### Using `ReadKey()`

```csharp
ConsoleKeyInfo key;   // variable that will store keystrokes
do
{
	key = Console.ReadKey();
	Console.WriteLine("You hit key: " + key.Key);
	Console.WriteLine("You entered character: " + key.KeyChar);
}
while (key.Key != ConsoleKey.Q);
```


Note that the key that you typed is also being displayed on the screen (very annoying).
To get rid of that, call `ReadKey` with the argument `true`:

```csharp
key = Console.ReadKey(true); // does not print the typed character to the screen
```

#### `ReadKey` is a blocking action

When you are using `ReadKey` to capture a keystroke, the program sits and waits for the user to type the key. 

> This prevents you from doing anything else (update your drawing, move the aliens, etc).

*Example*
```csharp
ConsoleKeyInfo key;
int i = 0;
ConsoleKeyInfo key;   // variable that will store keystrokes
do
{
	key = Console.ReadKey();
	i++;
	Console.WriteLine("i="+i+", You hit key: " + key.Key);
}
while (key.Key != ConsoleKey.Q);
```

*Result* - Notice that `i` only increments if you hit a key.

```text
i=1, You hit key: A
i=2, You hit key: B
i=3, You hit key: C
i=4, You hit key: D
i=5, You hit key: E
```


### `KeyAvailable` - Non blocking read

To understand how this works, you need to understand the 'innards' of what is happening when you press a key.

1. You press a key.
2. The OS notices, and keeps this information stored in memory, and sets a flag indicating that a key has been pressed.
3. Your program gets the status of `KeyAvailable`
   1. If the user has already pressed a key, then the OS will answer 'yes', and `KeyAvailable` will be true
   2. If the user has not already pressed a key, then the OS will answer `no` and `KeyAvailable` will be false
4. Your program executes `ReadKey()`.
   1. If the user has already entered a key, the OS know about it, and gives the appropriate information to the function, else, the program halts, and waits for a user to enter a key.

So, if we execute the following code:

```csharp
// declare a ConsoleKeyInfo variable that will store the key presses.
ConsoleKeyInfo key;
int counter = 0;
bool readKeyPress = true;
do
{
    counter++;
    // if user has pressed a key, then
    if (Console.KeyAvailable)
    {
        // get the key that was pressed
        key = Console.ReadKey(true);
        Console.WriteLine("i=" + counter + ", You hit key: " + key.Key);
        if(key.Key == ConsoleKey.Q) readKeyPress = false;
    }
}
while (readKeyPress);
```

*result* - Notice that the `i` is constantly incrementing

```text
i=247734, You hit key: A
i=623707, You hit key: B
i=935336, You hit key: C
i=1237750, You hit key: D
i=1781236, You hit key: E
```

### Keystrokes to Position

Once keystrokes can be accurately detected, they need to be converted to movements.

1. Decide the functionality of each keys.
	- Example:
		- "Q" will exit the game
		-  "Arrow Up" moves the character up one row.
		- "Arrow Right" moves the character one column position to the right.
	
2. Use a **loop** to continuously read available keystrokes.

3. Use a switch-case statement to translate each keystroke into movement.

Below is an example (using the game setup show in the beginning of this section):

```csharp
// ===============================================================
// Change direction of character by detecting specific keys
// ===============================================================
static void ProcessKeyStrokes()
{
	ConsoleKeyInfo key;
    if (Console.KeyAvailable)
	{
		key = Console.ReadKey(true);
        switch (key.Key)
        {
		    case ConsoleKey.Q:
		        gameover = true;
                break;
            case ConsoleKey.UpArrow:
	            ChangeDirection(-1, 0);  // function containing movement logic
                break;
            case ConsoleKey.RightArrow:
                ChangeDirection(0, 1);
                break;
			// ... pattern continues
        }
    }
}
```

