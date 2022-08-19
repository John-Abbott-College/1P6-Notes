# Console: Self Learning

Go to the MSDN (microsoft documentation) and look at what is available for the `Console` class.

https://docs.microsoft.com/en-us/dotnet/api/system.console?view=net-5.0



## Things to know about Microsoft Documentation

### Properties

A `console` property is something that describes the console.  It can be '*read only*' or '*read/write*'.

* #### Read/Write

  * Look at the definition.  Check for the keywords `get` and `set`.  If they are both there, then this property is read/write.

  ```csharp
  public static ConsoleColor BackgroundColor { get; set; }
  ```

  * Example of using a read/write property

  ```csharp
  Console.ForegroundColor = ConsoleColor.Black;  // setting the property
  ConsoleColor fg = Console.ForegroundColor			 // getting the property
  ```

* #### Read Only

  * Look at the definition.  Check for the keywords `get`.  If they `get` is there (but not `set`), then this property is readonly.

  ```csharp
  public static bool CapsLock { get; }
  ```

  * Example of using a readonly property

  ```csharp
  if (Console.CapsLock) {
    Console.WriteLine("Caps lock is on!");
  }
  ```

* #### Property Value

  * The property value describes what this propery is.  It also defines what `type` the value must be (`int`, `bool`, *etc*)
  * If the property value is not a simply type (numbers, arrays, strings, etc), there should be a link to a web page that describes that type.

  Example:

  > [ConsoleColor](https://docs.microsoft.com/en-us/dotnet/api/system.consolecolor?view=net-5.0)
  >
  > A value that specifies the background color of the console; that is, the color that appears behind each character. The default is black.

* #### Examples

  * Often, one can only learn things in Microsoft documentation by reading the examples.  *However*, sometimes the examples are too confusing to parse.  
  * At this point, if you know what you want to learn, but do not understand the documentation, google is your friend, although `stack overflow` may not be... it depends.

 

# Interesting Console Properties

* `BackgroundColor`, `ForegroundColor` : Changes the colors used to write text to the screen

* `CursorLeft`, `CursorTop`: defines the location of the cursor row, column)

* `CursorVisible`: Is the cursor visible?

* `KeyAvailable`: will be described next class

* `WindowHeight`, `WindowWidth`: the size of your terminal window in rows and columns

  

# Interesting Console Methods (functions)

* `Beep` - doesn't work on Mac
* `Clear` - clear the terminal of all text, repositions the cursor at row 0, and column 0
* `GetCursorPosition` - where is the cursor
* `ReadKey` - reads a single keystroke (useful with property `KeyAvailable` - to be discussed next class)

