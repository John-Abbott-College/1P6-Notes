# Game Timing


This section will explore how to control the game's frame rate.
In other words, **control how fast the game happens**

We'll cover two simple techniques:

- Controlling game execution by "freezing" the game at specific intervals using `Thread.sleep`.
- Using a `timer` to execute a function at specific time intervals.

## Starter Code

The starter code below is a simple game where the 'X' character continuously advances on the screen.

**Notice the following:**

- Function `UpdatePosition()` is being called at every game loop.
	- This function moves character 'X' in the direction specified by function `ProcessKeyStrokes()`.
	- 'X' has a initial direction in the positive row direction (downwards).
	- This function will run as fast as the CPU can process this code.
		- The character will eventually run out of the Console and crash the program.
- The **ONLY** thing that the `draw` function should do is update the display.

> We need a way to control how fast the position of 'X' is changing.
> We must control the game's **frame-rate**


```csharp
        // ===============================================================
        // Global Variables
        // ===============================================================
        static bool gameover = false;

        // keeping track of location
        static int row = 0;      // current row position
        static int col = 0;      // current column position
        static int rowMove = 1;      // direction of row movement (+ or -)
        static int colMove = 0;      // direction of row movement (+ or -)


        // ===============================================================
        // Entry point
        // ===============================================================
        static void Main(string[] args)
        {
            // ShowHelp();

            // initialize the game
            // ===============================================================
            Console.Clear();
            Console.CursorVisible = false;
            // initial position in the middle of the console
            row = Console.WindowHeight / 2;
            col = Console.WindowWidth / 2;

            // play the game
            // ===============================================================
            while (!gameover)
            {
                ProcessKeyStrokes();  // Function not shown. See previous chapter
                UpdatePosition();
                DrawPlayer();
            }
        }       
        
        private static void UpdatePosition()
        {
            // Erase previous position
            Console.SetCursorPosition(col, row);
            Console.Write(' ');

            row += rowMove;
            col += colMove;
        }

        private static void DrawPlayer()
        {
            char player = 'X';
            Console.SetCursorPosition(col, row);
            Console.Write(player);
        }
```

## Frame rate with Sleep

The simplest way to control the speed of the game is by "freezing" the code execution for a specif amount of time. This is called **sleeping the program**.

> Sleeping the program is a blocking action meaning that **nothing will happen or be processed.**
> 
> - Use the system function `Thread.Sleep`, which takes the sleep time in **milliseconds**.
>
> See [documentation of `Thread.Sleep` here](https://learn.microsoft.com/en-us/dotnet/api/system.threading.thread.sleep?view=net-7.0)

```csharp
using System;
using System.Threading;  // Must include the 'System.Threading' namespace ("module")

class Example
{
    static void Main()
    {
        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine("Sleep for 2 seconds.");
            Thread.Sleep(2000);
        }
        Console.WriteLine("Main thread exits.");
    }
}
```


## Frame-rate with  `timer` 

If you would like other things to happen while your program is waiting to be updated, use a timer.

> The `System.Timers.Timer` works similarly as a watch timer:
> 
> 1. Setup the **amount of time to wait** before the timer elapses ("goes off").
> 2. Setup whether or not the timer will **auto reset** (start counting again).
> 3. Setup **what will happen** when the timer elapses (ex.: sound an alarm or play a song).
> 4. Start the timer.
>
> - See [documentation for `System.Timers.Timer`](https://learn.microsoft.com/en-us/dotnet/api/system.timers.timer?view=net-7.0).


### Setting up a Timer

```csharp
static System.Timers.Timer gameTimer;  // Instantiate a global Timer called gameTimer

// This function runs once to setup and start the timer.
static void SetupGameTimer()
{
	int framerate = 100;  // 100 milliseconds
	// Setup ammount of time before it elapses (framerate)
	gameTimer = new System.Timers.Timer(framerate);
	// Setup auto reset once time has elapsed (start it again)
	gameTimer.AutoReset = true;
	// Setup what will happen when the time has elapsed
	// This is a list of functions that will be run (ex. function 'DrawPlayer')
	gameTimer.Elapsed += DrawPlayer;
	// Start the timer
	gameTimer.Enabled = true;
}

// Function to be run MUST HAVE the input parameters Object and ElapsedEventArgs.
static void DrawPlayer(Object source, ElapsedEventArgs e)
{
	// Drawing code goes here.
}
```


#### Timer.AutoReset by Default

> By default,  `Timer.AutoReset`  is set to `true`!
> If you want the timer to only run once, you must **explicitly** set it to `false` .



## A Simple Example

Below is a simple game to control an X around the screen using `System.Timers`.

- Note that invalid moves can crash this program.

```csharp
using System;
using System.Timers;

namespace MoveX
{
    class Program
    {
        // ===============================================================
        // Global Variables
        // ===============================================================
        static bool gameover = false;
        static System.Timers.Timer gameTimer;  // declare global Timer called gameTimer

        // keeping track of location
        static int row = 0;      // current row position
        static int col = 0;      // current column position
        static int rowMove = 1;      // direction of next row movement (+ or -)
        static int colMove = 0;      // direction of next col movement (+ or -)

        // ===============================================================
        // Entry point
        // ===============================================================
        static void Main(string[] args)
        {
            // ShowHelp();
            
            // initialize the game
            // ===============================================================
            Console.Clear();
            Console.CursorVisible = false;

            // initial position in the middle of the console
            row = Console.WindowHeight / 2;
            col = Console.WindowWidth / 2;

            // setup and start game timer
            SetupGameTimer();

            // play the game
            // ===============================================================
            while (!gameover)
            {
                ProcessKeyStrokes();
				// Drawing is done by Timer
            }
        }

        // ===============================================================
        // Setup timer to call DrawPlayer every framerate
        // ===============================================================
        static void SetupGameTimer()
        {
            int framerate = 250;  // in milliseconds
            gameTimer = new System.Timers.Timer(framerate);
            gameTimer.AutoReset = true;
            gameTimer.Elapsed += DrawPlayer;
            gameTimer.Enabled = true;
        }

        // ===============================================================
        // Draw player in new position if movement is allowed.
		// Function is called by game timer.
        // ===============================================================
        private static void DrawPlayer(Object souce, ElapsedEventArgs e)
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

        // ===============================================================
        // Change direction of character by detecting specific keys
        // ===============================================================
        static void ProcessKeyStrokes()
        {
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
                            ChangeDirection(-1, 0);  // (rowDir, colDir)
                            break;
                        case ConsoleKey.DownArrow:
                            ChangeDirection(1, 0);
                            break;
                        case ConsoleKey.RightArrow:
                            ChangeDirection(0, 1);
                            break;
                        case ConsoleKey.LeftArrow:
                            ChangeDirection(0, -1);
                            break;
                    }
                }
            }
        }

        // ===============================================================
        // Change global direction variables 
        // ===============================================================
        private static void ChangeDirection(int newRowDirection, int newColDirection)
        {
            rowMove = newRowDirection;
            colMove = newColDirection;
        }
    }
}

```


## Resources

### Timers

- Brief explanation: [Introduction to Timer in C#](https://www.educba.com/timer-in-c-sharp/) by EduCBA.com (Tutorial)
- Detailed explanation: [C# Timer: Schedule a Task](https://social.technet.microsoft.com/wiki/contents/articles/37252.c-timer-schedule-a-task.aspx) by Microsoft TechNet (Blog)