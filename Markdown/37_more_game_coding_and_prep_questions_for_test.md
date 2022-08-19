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

# Test 3 Info

## Need to know

Things to make sure that you know up to know 

- Variables 
- Counter and Accumulator 
- Loops - all flavours of loops 
- Function return values 
- Function arguments - and the fact that they're not related to function return values 
- Arrays 
- Using loops to control the index of your array 
- Pass by reference 
- Passing array pointers 

## Example Test Questions

### Question

If I call a function `foo` in the following manner...

```csharp
int x;
double y;
bool z;
x = foo(y,z);
```

... how would you declare the function?

### Question 

*You are not allowed to change the code*. You must write `calculateit`. 

```csharp 
Double temperature; 
Int32 userinput; 
Boolean good; 

// code here. 
// the user is to type in a Fahrenheit temperature, and you  
// display a message saying "nice weather" or "bad weather" if  
// temperature is above 20 Celsius 
// C = (F-32) * 5/9 

// extra code above here to accept user input 
good = calculateit(userinput, ref temperature); 

if (good) 
{ 
	Console.WriteLine("Nice Weather"); 
} 

else 
{ 
	Console.WriteLine("Bad Weather"); 
} 

Console.WriteLine ("It is "+temperature+" degrees Celsius outside"); 
```

### Question

What is the output?

```csharp
static void Main(string[] args)
{
    int a, b, c;
    a = 10;
    b = 5;
    c = 4;
    Console.WriteLine("Before the function a={0} b={1} c={2}", a, b, c);
    // kind of pointless to give 'c' a value - it will be passes as an out argument
    // so it will become 'undefined' when it enters the function 'go'.

    go(a, ref b, out c, ref a);
    Console.WriteLine("After the function a={0} b={1} c={2}", a, b, c);

}
public static void go (int da, ref int db, out int dc, ref int dd)
{
    da *= 2;
    db *= 3;
    // dc *=2 // NO!!! dc is undefined as it comes into the functon
    // (because it uses the 'out' keyword).  You cannot say
    // dc = dc * 2; because dc is undefined

    dc = 37; // okeay - this is a MUST
    // dc must equal something BEFORE you return back to the calling function
    dd *= 4;

    Console.WriteLine("IN the function da={0} db={1} dc={2} dd={3}", da, db, dc, dd);
}

```

### Question

What is the output

```csharp
static void Main(string[] args)
{
    int sneezy, sleepy, grumpy;
    sneezy = sleepy = 5;
    grumpy = sneezy * 2;

    Console.WriteLine("in main I see this: sneezy={0} sleepy={1} grumpy={2}", sneezy, sleepy, grumpy);
    sleepy = crazyfunc(ref grumpy, out sneezy);
    grumpy = crazyfunc(ref sneezy, out grumpy);
    Console.WriteLine("in main I see this: sneezy={0} sleepy={1} grumpy={2}", sneezy, sleepy, grumpy);
}
public static int crazyfunc (ref int db, out int da)
{
    da = 12;
    db = db + 10;
    da = da + 1;
    int dc;

    Console.WriteLine("In the function da={0} db={1}", da, db);
    dc = da + db + 4;
    return dc;
}

```

### Question

Write the function `PrintReport`.  Output should look like:

```text
1001: sandy     78.2
1002: bob       55
1003: betty     91.6
1004: alex      87.7
1005: michael   67.3
1006: ken       78.3
```

*Code*

```csharp
static void Main(string[] args)
{
    string[] names = new string[]
            { "sandy", "bob", "betty", "alex", "michael", "ken" };
    int[] id = new int[] { 1001, 1002, 1003, 1004, 1005, 1006 };
    double[] grade = new double[] { 78.2, 55, 91.6, 87.7, 67.3, 78.3 };

    PrintReport(names, id, grade);
    
}

```

