# Parameters

## Introduction

Recall that programming is **general problem solving**. For that to be true, there has to be some way to specify the "generalized" part \- for example, if you want an mp3 player to play a song, you have to tell it what song to play. In order for that to be truly general to **any** mp3 file, the syntax must allow you to specify a large, potentially infinite, variety of options. The syntax that we've seen so far doesn't have any way to do that \- while we could enumerate a fixed number of methods on an object, that's going to quickly run into practical limits.

## Parameters

A **parameter**, sometimes called an **argument**, is a piece of data that you provide to an object alongside a method or constructor. For example, if we were writing a program with an Mp3Player object, it might have a method playSong that takes in a **parameter** of the name of the song. Parameters can be specified in two ways \- as either **fixed** values, or **variable** values. For right now, we'll focus on fixed values, as we haven't covered variables yet.

**Vocabulary Note**

Many concepts in programming go by a variety of names, and it's good to be familiar with all the ways someone might refer to a concept. "Fixed" is **not** standard terminology for this type of parameter, but it's a convenient descriptive name. The more common name for these are **hardcoded values**, a phrase that often has a slightly negative connotation \- if you take more advanced courses in CS, you'll find that in larger systems using fixed values almost always causes problems in the long run. Fortunately, we're not currently building a million line code base that will persist for decades, so they're fine for our purposes (typically, using fixed values in smaller, simpler programs is more efficient than building a generalized configuration framework).

Within the larger aegis of **hardcoded values**, there are two subtypes that we'll see: **literals**, which use special Java-specific syntax, and **constants**, which allow a programmer to create their own descriptively-named fixed values. You've already seen an example of a literal (specifically, a **string literal**) in the HelloWorld program \- "Hello world" is a specific piece of text that's provided to the System.out.println method to tell it what text to print to the console.

## Literals

**String Literals**

<img align="right" src="images/bday.png" alt="Happy Birthday Balloons" width="20%"/>

The name for a piece of text in programming (Java or otherwise) is a "string", short for a "string of characters" - as a helpful visual mnemonic, picture a balloon sign with letters strung together. Strings are deceptively complicated, and we'll revisit them later in the semester, but for now when you see 'string', think 'word' or 'text'. To specify a string literal in Java, use double-quotes around it \- "Hello world", "Never gonna give you up.mp3", "It was the best of times, it was the worst of times", and "123" are all strings. Strings can contain spaces, letters, numbers, and punctuation ("special characters") \- depending on the encoding, they can contain other things as well (such as emojis), but we'll stick with things you can type on a standard keyboard for right now.

**Numeric literals**

To specify a literal number, you can generally just type the number:

`123`

or

`3.14`

We'll talk about exactly what's going on with these more when we get to variables, but for now, specify a particular number by just typing the number, no special syntax required. 

## Constants

A **constant** is a bit more flexible than a literal, because any programmer can create one. The first constants that we'll be dealing with relate to colors \- red, green, blue, etc. By convention, constants are in all caps in Java, and are preceded by the **class** where they're defined, followed by a '.'.

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_.\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_  
(Name of class)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(all-caps name of constant)

The color constants we'll be using come standard with the JRE (Java Runtime Environment), which means any Java program has access to them. They live in the Color class, and include a basic palette of colors:

WHITE  
BLACK  
GRAY  
LIGHT\_GRAY  
DARK\_GRAY  
RED  
GREEN  
BLUE  
PINK  
ORANGE  
YELLOW  
CYAN  
MAGENTA

So to refer to the color red, you'd use `Color.RED` in your program.

## Parameter Syntax

Parameters can be used when creating a new object (with a **constructor**), or when calling a method, and the syntax for both is the same \- you provide the parameter inside the **parentheses** for a method or a constructor.

Recall our previous syntax template for a constructor (used to create a new instance):

\_\_\_\_\_\_\_\_\_\_\_\__\_\_\_\_&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \= new \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ ();  
(Type of object)&nbsp;&nbsp;&nbsp;(name for this specific instance)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(Type of object, same as before) 

Ex:   
`Robot binky = new Robot();`

To pass a parameter, we're going to update that template:

\_\_\_\_\_\_\_\_\_        \_\_\_\_\_\_\_\_\_\_ \= new \_\_\_\_\_\_\_\_ (**\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_**);  
(Type)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(name)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(Type)&nbsp;&nbsp;**(comma-separated list of 0 or more parameters)**

Ex:  
`Robot binky = new Robot("wholeNew.world");`

Previously, we were just always using the 0-parameter version, which is still valid

Similarly, for a method:

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_.\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_(**\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_**);

(name of instance)     (name of method)   **(comma-separated list of 0 or more parameters)**

## What can you use as a parameter/when can you use one?

Just as you can only call a method that is defined for a particular type (you can ask Binky to move forward with a moveForward method, but since there isn't a moveBackward method defined, he can't move backward just with a single method call), you can only use parameters with methods or constructors that have defined parameters.

Every method we've seen up until now has had a **method signature** that just included open/close parentheses. For example:

`boolean isClear();`

Methods that accept parameters will include that in their **method signature**, and for each parameter, they will include what **type** the parameter needs to be, as well as a descriptive name, which for our purposes right now just serves as a hint for what the method will do with that parameter. If a parameter is optional, multiple versions of the method will be defined, one with and one without the parameter (this is called **overloading** a method). Typically, parameters are not optional.

## Parameters and Binky

The first parameter we'll look at is to the constructor for Binky. This is a situation that uses **overloading** \- you can either create a Robot with no parameters, which will create a Robot in a default world, or you can specify a particular world.

In Robot.java, these look like:

```
Robot()  
Robot(String worldFile)
```

Because there are two, you can choose whether or not to specify a particular world. Let's look more closely at this parameter:

`String worldFile`

You can see this is very similar to part of the template for creating a new object \- specifically, there's a type (String) and then a name (worldFile). The type must be a valid object type (technically, it must be any valid type, either object or primitive, but we haven't covered primitive types yet), and the name can be anything, although it's good practice to make it descriptive. Since the type is String, we know we're passing in text, and the name gives us a hint \- it should be the name of a file that represents a world that Binky can navigate. Just like programming code files have a .java extension, compressed files have a .zip extension, and images can have a .png or .gif extension, Binky's world files have a .world extension. For the assignments, you'll be able to specify a variety of .world files that are available in the 'resources' folder in your project directory.

To use the parameter version of the constructor, you provide a **string literal**; to use the parameter version **usefully**, you provide a string literal that corresponds to a specific file name. For example, if in the 'resources' folder you have a file 'hello.world', you could create a Robot named binky with that world by writing:

`Robot binky = new Robot("hello.world");`

If you provide something other than a String (ex: Color.RED), you'll get a compile error (red squiggle, program won't run). If you provide a String that doesn't correspond to a valid world file (ex: "gibberish"), you'll get a runtime error (no red squiggle, program will crash when it gets to that line). This highlights the difference between valid code and semantically valid code \- just having your code compile doesn't mean it will do what you want\! That's where the interesting part of programming comes in (debugging).

The next parameter we'll look at is for a new, non-overloaded method \- in order to use this method at all, you must always provide a parameter. This is a method defined for the Robot type:

`void paintSquare(Color color)`

Here, we can see the type is Color \- we'll need to provide one of the constants defined in the Color class (technically, you can also create your own custom colors, but we'll stick with the constants for now). The name of the variable, lowercase-c color, doesn't provide a lot of additional information \- by convention, that means that **any** parameter with the correct type should work reasonably well (if the variable were named something like 'primaryColor' or 'greyscaleColor', that would be a hint about what specific values of type Color will work well). As you might expect from the name of the method, calling this will cause Binky to change the color of the square he's standing on to the one that you specify.

Given what the method does, it should make sense why this parameter is not optional \- if you're going to paint something, you have to have a color that you're painting it. Method parameters are similarly required \- overloaded methods are generally ones where there are sensible and commonly used **default** behaviors (if you look under the hood, that's what happens with the Robot constructor \- when no file is specified, it uses the file "default.world").

Putting this all together: suppose we wanted to have Binky appear in a specific world represented by the file singleSquare.world, and paint the square he starts on blue (note: the preceding sentence serves as our **pseudo code** that we're going to now translate directly to code, one line per clause in the sentence). The code for that would look like:

```
Robot binky = new Robot("singleSquare.world");  
binky.paintSquare(Color.BLUE);
```

## Comparing Values

Now that we can change the color of a square, there's another useful method in the Robot class:

`Color getSquareColor()`

This is a slightly more complicated return value than the true/false values for isClear() and squareHasBreadcrumb() \- here, we'll actually get a Color object back, representing the current color of the square. For example, if the square that Binky is standing on is red, then getSquareColor will return Color.RED.

Of course, the immediate question is, how can you tell what color the Color object represents? In Java, there are a few methods that are automatically defined for all object types. One of those methods is called `equals`, and it has both a parameter and a return value:

`boolean equals(Object obj)`

This method will return true if the parameter is equal to the object that the method is called on \- that sounds convoluted, but the code is readable:

`binky.getSquareColor().equals(Color.RED)`

will return true or false depending on whether the square Binky is standing on is red or not. This can be used in 'if' or 'while' statements in much the same way as isClear():

```
if (binky.getSquareColor().equals(Color.RED)) {  
  binky.moveForward();  
}
```

will make Binky move forward one square if he's currently standing on a red square.

## Breaking down the syntax

**Reading** code and **writing** code are two fairly different skill sets \- skimming through code that follows coding conventions around whitespace and uses descriptive variable names can give you the **gist** of what a program is doing even when you don't know what the constructions are doing in detail (this is a good thing, and part of why coding conventions and descriptive variable names are valuable). On the other hand, writing code (and even more so, debugging code) requires that you understand **exactly what each piece of syntax is doing**. So let's go through that if statement above in more detail to see exactly what's going on. This is a bit like doing a **close reading** of a piece of text in a literature class.


**if (** binky.getSquareColor().equals(Color.RED) **) {**  
&nbsp;&nbsp;&nbsp;&nbsp;binky.moveForward();  
**}**

The first thing Java will do when running this code is parse the conditional (the 'if'). Recall the syntax template for an if:

```
if ( ________________________ ) {  
     (some true/false condition)  
     
    ___________________________________________________________________
    (one or more lines of code to only run if the condition is true)

}
```

So the code here says that if the thing in the parentheses (`binky.getSquareColor().equals(Color.RED)`) is true, then the code in the curly braces ( `binky.moveForward();`) will run, otherwise it won't.

Next, Java will call each method in the conditional statement **in left-to-right order** so that it can determine if the whole statement evaluates to true or false.  
First, that's `binky.getSquareColor()`. This method will return a Color object representing the color of the square. As the program runs, the JVM (Java Virtual Machine) will then use that to evaluate the rest of the line. Let's consider a case where Binky is standing on a blue square:

`binky.getSquareColor().equals(Color.RED)`

becomes

&nbsp;&nbsp;&nbsp;&nbsp;Color.BLUE  
~~binky.getSquareColor()~~.equals(Color.RED)

`Color.BLUE.equals(Color.RED)`

is calling a method on Color.BLUE (the 'equals' method) with a parameter of Color.RED \- calling a method on an object is equivalent to asking it a question or telling it to do something. In this case, we're asking Color.BLUE if it is equal to Color.RED \- Color.BLUE will say no, it's not.

So now Java can update

`Color.BLUE.equals(Color.RED)`

to

&nbsp;&nbsp;&nbsp;&nbsp;false  
~~Color.BLUE.equals(Color.RED)~~

meaning the if statement now looks like:

```
if (false) {  
  binky.moveForward();  
}
```

So Binky will not move.

But what if Binky had been standing on a red square?  
Now we'd have

`binky.getSquareColor().equals(Color.RED)`

becomes

&nbsp;&nbsp;&nbsp;&nbsp;Color.RED  
~~binky.getSquareColor()~~.equals(Color.RED)

When we ask Color.RED if it's equal to Color.RED, it will say yes:

`Color.RED.equals(Color.RED)`

becomes

&nbsp;&nbsp;&nbsp;&nbsp;true  
~~Color.RED.equals(Color.RED)~~

Now we have an if statement that looks like:

```
if (true) {  
  binky.moveForward();  
}
```

In which case, Binky **will** move\!

This close reading technique is something you can use when **debugging** code \- go through each piece of each line to see what the code is actually doing, which will make it easier to find the piece that you need to change to get the code to do what you wanted it to do instead.

## Order of Operations

If you remember PEMDAS from high school (parentheses, exponent, multiplication, division, addition, subtraction), then you're familiar with the order of operations \- when given a long, potentially ambiguous set of instructions, what do you do first? Using that, you can determine that 2 \+ 3 \* 4 \= 14, while (2 \+ 3\) \* 4 \= 20\.

Programming similarly has an order of operations, but there are significantly more operations than just 6\. As a result, coding conventions dictate that you only rely on one: parentheses. Whenever you run across ambiguous or potentially ambiguous code, add parentheses around it. From a coding perspective, 2 \+ 3 \* 4 will compile and run, but it is **bad code** \- you should write **either**  (2 \+ 3\) \* 4 **or** 2 \+ (3 \* 4), because programming is complicated enough without layering anything else on top of it.

If you're ever unsure about the order that things will run on a line of code, add parentheses (later, we'll go over how you can also **extract variables** to help with this). As a very rough guideline, though, Java will:

- work from the innermost expression out  
- for non-nested expressions, work from left to right except for assignment (=)  
- calculate the right-hand side of assignments first

You'll notice this doesn't cover PEMDAS \- technically, Java does respect that multiplication comes before addition, but you should never write code that relies on this, so in practice that's just a fun bit of trivia. If you're curious what the full list is, you can see them here: [https://introcs.cs.princeton.edu/java/11precedence/](https://introcs.cs.princeton.edu/java/11precedence/) (I especially like this list for including the caveat "Most programmers do not memorize them all, and, even those that do, use parentheses for clarity" \- words to live by).
