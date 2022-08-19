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

