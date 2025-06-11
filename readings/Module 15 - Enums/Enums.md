# Enumerations

## Introduction

It’s common in a program to have a number of related constants - these are pre-established values that have some additional meaning that the programmer knows about that the compiler doesn’t. For example, when randomly flipping a coin, the fact that 0 means ‘Heads’ and 1 means ‘Tails’ is something the programmer must track. To make code easier to read, this might involve creating two constants:

```
public static final int HEADS = 0;
public static final int TAILS = 1;
```

This is fine for coins, but as the number of constants goes up, it gets harder to keep track of them. For example, imagine having someone choose a color at random - if there are 6 colors to choose from, there needs to be a switch statement that maps (ie, transforms) all the numbers from 0 - 5 to a particular color. You might be thinking, wait a minute, we just learned about a way to efficiently handle “many” of something - surely there’s a way to combine arrays and constants to improve this? There is! It’s called an **enumeration**, or **enum** for short.

## Syntax

To create an enum, you do something similar to creating a new class, except with an exciting new keyword. Instead of `public class SomeClass {}`, now you’ll write `public enum SomeEnum {}`. 

Within the {}’s, you’ll list the constants, separated by commas (and usually by newlines for readability). No type information, no initialization, just the name of the constant - the type is the name of the enum (ex: SomeEnum), and the initialization is handled automatically.

For example:

```
public enum ColorOption {
RED,
GREEN,
BLUE
}
```

To use the enum, the syntax is the same as for constants, but notice that the type is specified by the **name of the enum**:

`ColorOption chosenColor = ColorOption.RED;`

Much like classes come with a few built-in methods (`.equals`, `.toString`), enums come with a useful built-in method as well: `values()`.

`values()` is a static method - you call it on the enum type itself. It returns an array of all the possible options for the enum. This creates a new option for handling all the constants in a unified way - while you can still interact with a specific value by name, you can also work with all values as a group.

## Picking a Random Color

Using the ColorOption enum, there’s now a better version of selecting a color at random:

```
Random rng = new Random();
int colorIndex = rng.nextInt(3);
ColorOption chosenColor = ColorOption.values()[colorIndex];
```

No switch statement required! Here you can also see how convenient it is that both nextInt and array indexes start counting at 0. However, this code isn’t quite as general as it could be. What if we wanted to add another color option to the program? You’ll notice we can’t do this dynamically (ie, while the program is running) with enums - because they’re a replacement for long lists of related constants, they still maintain the property that they can’t change while the program is running. However, we can still change the code and then re-run the program:

```
public enum ColorOption {
RED,
GREEN,
BLUE,
YELLOW
}
```

If we just made that change, though, our random color selection would never select yellow! That’s because

`int colorIndex = rng.nextInt(3);`

is still only choosing from 3 options. Rather than having to remember to update that number every time the enum changes, we can instead get the enum to tell us how many options it has, once again using the `values()` method. Since `values()` returns an array, we can get the length of the array to find the number of options:

```
int numColors = ColorOption.values().length;
int colorIndex = rng.nextInt(numColors);
```

Now, the code:

```
Random rng = new Random();
int numColors = ColorOption.values().length;
int colorIndex = rng.nextInt(numColors);
ColorOption chosenColor = ColorOption.values()[colorIndex];
```

is a general solution to picking a color at random from any list of colors - any updates to the options in ColorOption automatically get handled correctly by this code.

## Further Reading

If you’re wondering if there’s a way to make the contents of an enum dynamic, ie able to be updated while a program is running, the answer is yes, but it doesn’t involve enums: generally, that’s accomplished by having a configuration file for a program (if you’ve ever wondered what’s in the mysterious .metadata folder in an Eclipse workspace, it’s storing config files - feel free to go look at them, they’re pretty much all text files. Be careful about changing them, though - they’re designed to be human-editable, but there are no safety rails).
