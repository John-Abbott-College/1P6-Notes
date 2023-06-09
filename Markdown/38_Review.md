# Example Test Questions

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



# Review

In class, we did some code *live*.

Here is the code that we did in class.

```csharp
using System;
using System.Diagnostics;


namespace testing
{
    class MainClass
    {


        // main
        public static void Main(string[] args)
        {
            question2();


            int[] array = new int[] { 3, 5, 6, 8, 3, 2 };
            int[] newarray = new int[6];
            int counter = 0;
            foreach (int tmp in array)
            {
                newarray[counter] = tmp * tmp;
                counter++;
                Console.WriteLine(tmp);
            }


            for(int i=0; i< array.Length; i++)
            {
                array[i] = array[i] * 2;
            }


            // We want the first element of the array to
            // goto the last element
            // shift all elements 'up'


            // save the first element
            // starting at the second element, move it to the first
            // take the third element, and move it to the second


            int first = array[0];
            for (int i = 1; i < array.Length; i++)
            {
                array[i - 1] = array[i];
            }
            array[array.Length - 1] = first;




            // Question from sample test3 questions
            int sneezy, sleepy, grumpy;
            sneezy = sleepy = 5; // 5
            grumpy = sneezy * 2; // 10


            Console.WriteLine("Main: sneezy={0}, sleepy={1}, grumpy={2}", sneezy, sleepy, grumpy);


            sleepy = crazyfunc(ref grumpy, out sneezy);
            // sleepy = 37, // grumpy =20 // sneezy = 13

            grumpy = crazyfunc(ref sneezy, out grumpy);
           // grumpy = 40, // sneezy = 23 // sleepy = 37
          
            Console.WriteLine("Main: sneezy={0}, sleepy={1}, grumpy={2}", sneezy, sleepy, grumpy);


        }


        static int crazyfunc (ref int db, out int da)
        { 
          								// line 63			// line 66
            da = 12;  		// sneezy = 12  // grumpy = 12
            db = db + 10; // grumpy = 20 	// sneezy = 23
            da = da + 1; 	// sneezy = 13 	// grumpy = 13
            int dc; 


            Console.WriteLine("Func: da={0}, db={1}", da, db);
            dc = da + db + 4; // dc = 37 	// dc = 40
            return dc;
        }




        static void question2()
        {
            double temperature = -273; 
            int userinput;
            bool good;
            userinput = int.Parse(Console.ReadLine());
            
            good = calculateit(userinput, ref temperature);
            if (good)
            {
                Console.WriteLine("Nice weather");
            }
            else
            {
                Console.WriteLine("Bad weather");
            }
            Console.WriteLine("It is" + temperature + "degrees C");
        }


        static bool calculateit(int input, ref double celcius)
        {
            celcius = (input - 32) * 5 / 9;
            if (celcius > 20)
            {
                return true;
            }
            else
            {
                return false;
            }
        }
    


    }




}
```

