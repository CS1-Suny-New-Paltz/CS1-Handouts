# Variables

## Introduction

Variables are a powerful tool for making large programs easier to write and reason about. However, they work a bit differently in programs than they do in a mathematical context \- while  a mathematical variable often shows up as 'solve for x in the following equation', in a programming context, not only do you get to decide what value variable x starts as, but you can change, or **vary** what value it has over the course of the program.

## Variable syntax

The syntax template for a variable is similar to a parameter, and it's syntax that we've already seen for creating Binky (Binky is actually a variable of type Robot). To create a variable, you must both declare the variable and initialize it, which you can either do like this:

```
  __________________   ________________;
  (type of variable)   (name of variable)
  
  __________________ = _____________________________;
  (name of variable)    (initial value for variable)
```

or you can combine these into one line:

```
   __________________   ________________  = _____________________________;
  (type of variable)   (name of variable)   (initial value for variable)
```

For example:

```
  Robot binky;
  binky = new Robot();
```

or

```
  Robot binky = new Robot();
```

Usually, the **variable declaration**, which is the name and the type, is combined with the **variable initialization** where the variable gets an initial value. However, if the initial value to use depends on other parts of the program, sometimes the two steps are separated. 

## Why use a Variable?

In an object-oriented language, one of the major reasons to have a variable is to have access to a specific object type. For example, all of our programs so far have involved the Robot class, which is able to draw graphics on the screen and respond to simple commands via methods. However, variables are often introduced for two other major reasons: **readability**, which refers to how easy it is to follow along with code by reading it, and **calculations**, which take advantage of the fact that variables don't have a fixed value.

## Variables for Readability

As programs get more complex, they often involve manipulating data. While it's possible to represent these manipulations "in line", ie, with one long, complex line of code, it's hard to both read and debug code that's written that way. As an alternative, you can use **variables**, which add **descriptive names** to each piece of **data**. This is similar to how methods add descriptive names to pieces of **logic**.

**Variable Example**

Consider some code to check if Binky is standing on a gray square:

`if (binky.getSquareColor().equals(Color.GRAY))`

Recall that when evaluating this code, Java first calculates the return value of binky.getSquareColor(), then uses that value to call the .equals method with Color.GRAY as a parameter. Suppose we wanted to be very clear about this ordering, though, by making each method call its own statement/step of code. To do that, we could introduce a **variable** representing the result of the first method call \- this essentially lets us add a name into the code for clarity. The pseudo-code looks like:

```
// Check what color square Binky is standing on - call it squareColor  
// Now, see if squareColor is equal to GRAY
```

The corresponding Java code would be:

```
Color squareColor = binky.getSquareColor();  
if (squareColor.equals(Color.GRAY))
```

Now there's only one method being called per line, which makes the code easier to read as well as easier to step through methodically in order to debug any problems.

## Variables for Calculations

Variables get their name from the fact that their value can change ('vary') during the program. Whenever you're talking about the value of a variable, it's important to be clear about **what line** (and for a loop, possibly which iteration) of the program you're considering, since the value can change. 

For example, suppose we wanted to write a program where Binky would walk along the top row of the world, changing gray squares to white, and white squares to blue.

The pseudo code looks like:

```
// Until Binky reaches a wall  
// Check what color square Binky is standing on \- call it squareColor  
// if squareColor is equal to gray, change the square to white  
// if squareColor is equal to white, change the square to blue  
// Move to the next square
```

The code would then be:

```
// Until Binky reaches a wall  
while (binky.isClear()) {

  // Check what color square Binky is standing on - call it squareColor  
  Color squareColor = binky.getSquareColor();

  // if squareColor is equal to gray, change the square to white  
  if (squareColor.equals(Color.GRAY)) {  
    binky.paintSquare(Color.WHITE);  
  }

  // if squareColor is equal to white, change the square to blue  
  if (squareColor.equals(Color.WHITE)) {  
    binky.paintSquare(Color.BLUE);  
  }

  // Move to the next square  
  binky.moveForward();  
}
```

You'll notice that the **value** of squareColor changes each time through the loop \- it's the color of the square Binky is standing on. Sometimes, that value might be Color.GRAY, sometimes it might be Color.WHITE, sometimes it might be a different color (depending on the world Binky is in). What's also notable here is that this is the color of the square **before** Binky makes any changes to the square. This is an important distinction, and it makes the code much more straightforward, because it makes it explicit when the "color we're considering" should change. Imagine writing the code without a variable:

```
// Until Binky reaches a wall  
while (binky.isClear()) {

  // Check what color square Binky is standing on

 // if the square is gray, change the square to white  
  if (binky.getSquareColor().equals(Color.GRAY)) {  
    binky.paintSquare(Color.WHITE);  
  }

  // if the square is white, change the square to blue  
  if (binky.getSquareColor().equals(Color.WHITE)) {  
    binky.paintSquare(Color.BLUE);  
  }

  // Move to the next square  
  binky.moveForward();  
}
```

This program doesn't do the same thing as the version with the variables\! Take a moment to see if you can figure out why (spoilers in the next paragraph).

### Spoilers\! 

In the non-variable version, when Binky is on a gray square, first he changes the color to white, and then **checks again** what color the square is \- because it's now white, he'll update it to blue. So while the variable version will replace gray squares with white ones and white ones with blue, the non-variable version will change both gray and white squares to blue. To actually mimic the behavior of the variable program, we'd need to use an else statement:

```
// Until Binky reaches a wall  
while (binky.isClear()) {

  // Check what color square Binky is standing on

  // if the square is gray, change the square to white  
  if (binky.getSquareColor().equals(Color.GRAY)) {  
    binky.paintSquare(Color.WHITE);  
  } else {  
    // if the square is white, and we didn't just change it,   
    // change the square to blue  
    if (binky.getSquareColor().equals(Color.WHITE)) {  
      binky.paintSquare(Color.BLUE);  
    }	
  }

  // Move to the next square  
  binky.moveForward();  
}
```

This is more complicated to read, and likely required at least one **debugging pass** to come up with \- using a variable often **avoids** the entire problem of data **changing unexpectedly**. Since the easiest way to debug a program is to not have it contain bugs in the first place, using coding techniques that avoid common bugs will make your programming experience more efficient.

## Variable Types

You may have noticed that the syntax for a variable is very similar to that for a parameter \- a **type**, followed by a name. This syntax is Java-specific \- other languages, such as JavaScript, don't require you to include the type (instead, you'd use a keyword such as const or var). Java is what's known as a **strongly typed** language, which means you have to be very (some might say excessively) clear about exactly what type all of your data is all of the time. There's actually a good reason for this \- it lets the compiler check for and alert you to certain types of bugs before you ever run your program. It can also make complex programs easier to follow \- when a program becomes thousands (or millions) of lines of code spanning hundreds (or thousands) of files, it's helpful to know if you're dealing with a Color, a Robot, or a String without having to go read through every relevant file. We won't be creating programs that large this semester, but being clear about **data types** is good practice both for programming and for other aspects of computer science \- formal logic proofs in a discrete math class, for example, require that you always have a series of boolean statements created by applying various operators in a specific order.

So what happens when you have data of one type, and want to **transform** it into another type? Generally, you'll use a method that will take the pieces of the first type and "reassemble the legos" into a different type \- we've seen this already with the ability to turn a String representing a file ("threeTurns.world") into a Robot in a specific world (`Robot binky = new Robot("threeTurns.world")`). Tracking your data types makes it easier to spot when you need a method to do this transformation \- otherwise you might accidentally write code like 

`binky = "threeTurns.world";`

which definitely won't work\! Having the compiler let you know that the types are incompatible makes that problem easier to fix right away, rather than waiting until you try to run the program and having it crash.
