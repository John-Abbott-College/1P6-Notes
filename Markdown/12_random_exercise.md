# Random Exercise

## Generating Random Integers

There is a special function in C# that can generate a random `int` between a low and a high value (including the low but not including the high values).

This function belongs to a `Random` object so this object needs to be created first. Objects are not covered in this course so consider the code below a "recipe" to be copied.

```csharp
int min = 10;    // lowest random value to be generated (included)
int max = 50;    // highest random value to be generated (not included)

Random randomizer = new Random();    // create an object of type Random
int randomInt = randomizer.Next(min, max);   // generates a random int between min and max.
```

Where:

- `Random` is the name of a class (classes are covered in a later course).
- `Random randomizer` defines a variable called `randomizer` to be an object of type `Random`
- `Random()` is a function (method) that creates the object (also known as constructor).
- `Random randomizer = new Random()` creates a new Random object and saves it in the variable `randomizer`.
- `randomizer.Next(min, max)` call method `Next` with the parameters (inputs) `min` and `max` on the object `randomizer`.
	- The random number generated includes `min` but does not includes `max`.
	- Therefore, the code above will generate an integer in the range 10, 11, 12, 13, ..., 47, 48, 49.


## Exercise

🎲 Use the random number generator above to create a dice roll game with the following rules:

- The player rolls 2 dice at a time.
- If the two dice have the same number, it's an instant win.
- If the sum of the dice is 7, it's an instant loss, except when it's a "one six", that is one dice is 6 and the other is 1.
- Otherwise, the sum of the dice is the user's score for that round.

For now the program should play a single round, inform the user of the dice roll, the score and exit. The user can manually tally the score if they want.

*We'll eventually improve this game to have multiple players with several rounds.*


