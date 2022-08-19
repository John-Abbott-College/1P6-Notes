# Live Action Game Programming - general

When programming a 'live action' game, there are some standard 'best practices' that are best followed.

> NOTE: Although global variables are strongly discouraged in programming, if you are programming a game without using object orientated logic (you are not, we are using procedural programming), then you will have to use global variables.

* Have a function that processes key strokes in a continuous while loop.
  * Adjust whatever global variables need adjusting.
  * Do not draw anything!
* Have a 'draw' function that gets called periodically.  How often it gets called is the 'frame rate'.
  * Only redraw what is necessary

# Processing Key Strokes

Normally, when you enter data into a computer program, the program does not receive your input *until* you press the `ENTER` key.

But, in game programming, we do **not** want to have to press the `ENTER` key every single time we hit an arrow.

So, what do we do?

### `ReadKey()`

This function will immediately return the key that you typed on the keyboard, without having to follow by pressing the `ENTER` key.

If you look at the MSDN documentation for [ReadKey](https://docs.microsoft.com/en-us/dotnet/api/system.console.readkey?view=net-5.0) you will notice that the return type of `ReadKey` is [ConsoleKeyInfo](https://docs.microsoft.com/en-us/dotnet/api/system.consolekeyinfo?view=net-5.0).  (I leave it to the reader to read the documentation).

#### Comparing keystrokes

Comparing the keys, you have two options, comparing the character that was typed, and comparing the actual key that was hit.

If you are comparing the `key`, then there is no distinction between 'Q' and 'q', for example.

#### Using `ReadKey()`

```csharp
ConsoleKeyInfo key;
while (true)
{
	key = Console.ReadKey();
  if (key.Key == ConsoleKey.Q) break;
  Console.WriteLine("You hit key: " + key.Key);
  Console.WriteLine("You entered character: " + key.KeyChar);
}

```

But it is annoying that the key that you typed is also being displayed on the screen.  To get rid of that, call `ReadKey` like this:

```csharp
key = Console.ReadKey(true); // does not print the typed character to the screen
```

#### `ReadKey` is a blocking action!

When you are using `ReadKey` to capture a keystroke, the program sits and waits for the user to type the key.  This prevents you from doing anything else (update your drawing, move the aliens, etc).

**example**
```csharp
ConsoleKeyInfo key;
int i = 0;
while (true)
{
	i++;
	key = Console.ReadKey(true);
  if (key.Key == ConsoleKey.Q) break;
  Console.WriteLine("i="+i+", You hit key: " + key.Key);
}

```

*result* - Notice that `i` only increments if you hit a key.

```text
i=1, You hit key: A
i=2, You hit key: B
i=3, You hit key: C
i=4, You hit key: D
i=5, You hit key: E
```



### `KeyAvailable` - Non blocking read

To understand how this works, you need to understand the 'innards' of what is happening when you press a key.

1. You press a key
2. The OS notices, and keeps this information stored in memory, and sets a flag indicating that a key has been pressed
3. Your program gets the status of `KeyAvailable`
   1. If the user has already pressed a key, then the OS will answer 'yes', and `KeyAvailable` will be true
   2. If the user has not already pressed a key, then the OS will answer `no` and `KeyAvailable` will be false
4. Your program executes `ReadKey()`.
   1. If the user has already entered a key, the OS know about it, and gives the appropriate information to the function, else, the program halts, and waits for a user to enter a key.

So, if we execute the following code:

```csharp
ConsoleKeyInfo key;
int i = 0;
while (true)
{
	i++;
  
  // if user has already pressed a key, then
  if (Console.KeyAvailable) {      
    
    // get the key that was already pressed
		key = Console.ReadKey(true);
  
    if (key.Key == ConsoleKey.Q) break;
  	Console.WriteLine("i="+i+", You hit key: " + key.Key);
  }
}
```

*result* - Notice that the `i` is constantly incrementing

```text
i=247734, You hit key: A
i=623707, You hit key: B
i=935336, You hit key: C
i=1237750, You hit key: D
i=1781236, You hit key: E
```

# Using `timer` to set a game frame

The **ONLY** thing that the `draw` function should do is update the display.

It is too early to describe what all of the code is doing, so I will just show the required code:

**setting up a timer**

```csharp
// global var
static System.Timers.Timer gameTimer;

static void SetupGameTimer()
{
  int framerate = 50; // 50 milliseconds
  
  // set a time for framerate milliseconds
	aTimer = new System.Timers.Timer(framerate);
  
  // when the time has elapsed, call the function 'Draw'
  aTimer.Elapsed += Draw;
  
  // once the time has elapsed, start it again
  aTimer.AutoReset = true;
  
  // timer is eanbled
  aTimer.Enabled = true;
}

// MUST HAVE a 'Draw' function, with the following signature
// (it can be named something else, but then you have to adjust line 12)
static void Draw(Object source, ElapsedEventArgs e) {
  // your drawing code goes here.
}


```



# A Simple Example

```csharp
using System;
using System.Timers;

namespace MoveASquare
{
    class Program
    {
        // ===============================================================
        // Global Variables
        // ===============================================================
        static System.Timers.Timer gameTimer;   // timer
        static bool gameover = false;           // when is the game over?

        // keeping track of location, direction, and speed
        static int drow = 0;
        static int dcol = 0;
        static double speed = 0.5;
        static double row = 0;
        static double col = 0;

        // ===============================================================
        // Entry point
        // ===============================================================
        static void Main(string[] args)
        {
            ShowHelp();

            // initialize the game
            drow = 1;
            Console.Clear();

            // make the cursor invisible
            Console.CursorVisible = false;

            // play the game
            SetupGameTimer();
            while (!gameover)
            {
                ProcessKeyStrokes();
            }
        }

        // ===============================================================
        // Show the instructions
        // ===============================================================
        static void ShowHelp()
        {
            // instructions
            Console.Clear();
            Console.WriteLine();
            Console.WriteLine(" MOVE A SQUARE ");
            Console.WriteLine("");
            Console.WriteLine(" Use arrow keys to change directions of movement");
            Console.WriteLine("");
            Console.WriteLine("Press 'Q' key to quit");

            // wait for user to start
            Console.WriteLine();
            Console.WriteLine();
            Console.WriteLine();
            Console.WriteLine("Press any key to start");
            Console.ReadKey();
        }

        // ===============================================================
        // Setup the timer for the game
        // ===============================================================
        static void SetupGameTimer()
        {
            gameTimer = new System.Timers.Timer(50);
            gameTimer.Elapsed += Draw;
            gameTimer.AutoReset = true;
            gameTimer.Enabled = true;

        }


        // ===============================================================
        // Change direction of "*" by pressing certain keys
        // ===============================================================
        static void ProcessKeyStrokes()
        {
            ConsoleKeyInfo key;
            while (Console.KeyAvailable)
            {
                key = Console.ReadKey(true);
                switch (key.Key)
                {
                    case ConsoleKey.Q:
                        gameover = true;
                        break;
                    case ConsoleKey.UpArrow:
                        drow = -1;
                        dcol = 0;
                        break;
                    case ConsoleKey.DownArrow:
                        drow = 1;
                        dcol = 0;
                        break;
                    case ConsoleKey.RightArrow:
                        drow = 0;
                        dcol = 1;
                        break;
                    case ConsoleKey.LeftArrow:
                        drow = 0;
                        dcol = -1;
                        break;
                }

            }
        }


        // ===============================================================
        // Update the Console
        // ===============================================================
        static void Draw(Object source, ElapsedEventArgs e)
        {

            // erase the old '*'
            Console.SetCursorPosition((int)col, (int)row);
            Console.Write(" ");

            // update position of '*'
            row = row + drow * speed;
            col = col + dcol * speed;
            if (row > Console.WindowHeight - 1) row = 0;
            if (row < 0) row = Console.WindowHeight - 1;
            if (col > Console.WindowWidth - 1) col = 0;
            if (col < 0) col = Console.WindowWidth - 1;

            // draw the new '*'
            Console.SetCursorPosition((int)col, (int)row);
            Console.Write("*");
        }

    }
}
```







