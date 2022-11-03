# Passing Information to Functions

## Counting candies (aka - pass by value)

Make groups of three:

- One person is the function `Foo`
- One person is the function `Main`, which calls `Foo`
- One person is the computer.

Teacher:
- write simple function for `Foo` taking two parameters, both # of candies


## Round 1

*Function call*
```csharp
static void Main() {
	choco red_box = 3;
	jolly blue_box = 2;
	
	blue_box = Foo(red_box, blue_box)
}
```

*Function Definition*
```csharp
static jolly Foo(choco pink_box, jolly green_box)
{
	return green_box = (jolly) pink_box % green_box
}
```

Students:

`main` fills two boxes with any number of candies they want

`computer` matches the two arguments (two boxes that `main` has), with the two parameters (two boxes that `foo` has), and puts the same number of candies in `foo`'s boxes as what was in `main`.' 

Example.  

* `main` has 3 candies in red box, and 4 candies in blue box.  Calls `foo(red_box, blue_box)`

* `foo` was defined as `foo(purple_box, green_box)`
* `computer` counts the candies in `red_box`, and puts the same number of candies in `purple_box` (Does not transfer candies, just makes sure both boxes contain the same number of candies).  `computer` does the same thing with `blue_box` and `green_box`

Now `foo` performs whatever operations have been specified for this function.
Example:
> `purple_box+=green_box`




NOTE: Most important

* The number of candies in `red_box` and `blue_box` remain unchanged, regardless of what happens in `foo`.
* If `foo` is called as `foo(blue_box, red_box)`, then `computer` matches `blue_box` with `purple_box`, and matches `red_box` with `green_box`, because ORDER MATTERS



**Rinse and Repeat**