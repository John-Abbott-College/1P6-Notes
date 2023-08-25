# More Game Programming

Some students want to have games where the movement is controlled solely by the user.

In that case, you need to move the object whenever a key is pressed.

You may decide to have a timer as well, and only update the drawing at regular intervals, *or* update the drawing everytime a key has been entered.

**Examples**

```csharp
using System;

class NamedExample
{
 
    static void Main(string[] args)
    {
        ProcessKeys();
    }
    static void ProcessKeys()
    {
        ConsoleKeyInfo key;
        bool gameOver = false;

        // initialize
        int row = Console.WindowHeight / 2;
        int col = Console.WindowWidth / 2;


        // loop
        while (! gameOver)
        {
            key = Console.ReadKey(true);
            switch (key.Key)
            {
                case ConsoleKey.Q:
                    gameOver = true;
                    break;
                case ConsoleKey.UpArrow:
                    Draw(row, col, row-1, col);
                    row = row - 1;
                    break;
                case ConsoleKey.DownArrow:
                    Draw(row, col, row + 1, col);
                    row = row + 1;
                    break;
                case ConsoleKey.RightArrow:
                    Draw(row, col, row, col + 1);
                    col = col + 1;
                    break;
                case ConsoleKey.LeftArrow:
                    Draw(row, col, row, col - 1);
                    col = col - 1;
                    break;

            }
        }
    }

    static void Draw(int oldrow, int oldcol, int row, int col)
    {
        Console.BackgroundColor = ConsoleColor.White;
        Console.SetCursorPosition(oldcol, oldrow);
        Console.Write(" ");
        Console.BackgroundColor = ConsoleColor.Black;
        Console.SetCursorPosition(col, row);
        Console.Write(" ");
    }
}
```

```csharp
using System;
using System.Timers;


class NamedExample
{

    static int row;
    static int col;
    static int oldrow = 0;
    static int oldcol = 0;
    static System.Timers.Timer gameTimer;   // timer


    static void Main(string[] args)
    {
        SetupGameTimer();
        ProcessKeys();
    }
    static void ProcessKeys()
    {
        ConsoleKeyInfo key;
        bool gameOver = false;

        // initialize
        row = Console.WindowHeight / 2;
        col = Console.WindowWidth / 2;


        // loop
        while (! gameOver)
        {
            key = Console.ReadKey(true);
            switch (key.Key)
            {
                case ConsoleKey.Q:
                    gameOver = true;
                    break;
                case ConsoleKey.UpArrow:
                    row = row - 1;
                    break;
                case ConsoleKey.DownArrow:
                    row = row + 1;
                    break;
                case ConsoleKey.RightArrow:
                    col = col + 1;
                    break;
                case ConsoleKey.LeftArrow:
                    col = col - 1;
                    break;

            }
        }
    }
    static void SetupGameTimer()
    {
        gameTimer = new System.Timers.Timer(50);
        gameTimer.Elapsed += Draw;
        gameTimer.AutoReset = true;
        gameTimer.Enabled = true;

    }



    static void Draw(Object source, ElapsedEventArgs e)

    {
        if (oldrow != row || oldcol != col)
        {
            Console.BackgroundColor = ConsoleColor.White;
            Console.SetCursorPosition(oldcol, oldrow);
            Console.Write(" ");
            Console.BackgroundColor = ConsoleColor.Black;
            Console.SetCursorPosition(col, row);
            Console.Write(" ");
            oldrow = row;
            oldcol = col;
        }
    }
}


```

