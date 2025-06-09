# Method Decomposition

## Introduction

So far, we've just been calling methods that already exist. Now, we're going to start looking at how (and why) to create our own methods. Methods serve a number of purposes:

- Improve code **readability** 
- Simplify the process of **debugging**
- Allow for **encapsulation** and **reuse** of behavior. 

The process of moving code from just the main method into smaller sub-methods is called **method decomposition**.

## How to Create a Method

We've seen **method signatures** for methods on the Robot class already \- we'll be using a similar syntax to create our own. For now, all the methods will use the keyword **static** (you've already seen this with public **static** void main) \- when we get into creating custom object types, we'll talk more about what exactly that keyword means.

Syntax for a public static method:

```
public static ______________       ________________ (_______________________) {
              (return value)      (name of method)    (0 or more parameters)

      _______________________________________________  
       (lines of code that run as part of the method)

}
```

If a method doesn't return anything, the return value is `void`; otherwise, it's what **type** of data is returned. For example, the moveForward() method is `void`, but isClear() returns a `boolean` (a true/false value).

The method name starts with a lowercase letter, and includes only letters and numbers, using camelCase to separate words (ex: thisIsAReallyLongMethodName).

In the above example, 'public' is what's called an **access modifier** \- that becomes relevant once you have multiple class files interacting with each other. For now, since we're just using one class, we'll just use 'public'. 

## When to Create a Method

The first reason to create a method is when you want your program to do the same thing multiple times, and you want to avoid copy-pasting code; if you copy-paste something and later need to change it (for example, to fix a bug, or to make a program more general), you have to manually go find and update **every place** where it was copy-pasted. A method is a way to just write the code once, and reference it from multiple places \- that way, you only need to update a single location to fix a bug everywhere.

Let's use a Binky Checkerboard problem as an example. The pseudo code is:

```
// while there are more rows  
   // fill in an alternating colors row starting with red  
   // reset to the next row  
   // fill in an alternating colors row starting with black  
   // reset to the next row
```

For simplicity, the above pseudo-code omits some of the extra checks to see if a row exists. Looking at this pseudo code, we can see that 'reset to the next row' is something we want to do multiple times. So, we'd create a **method** that contains that logic, and give it a descriptive name. Let's call the method resetRow; it won't return anything, but what about parameters? The parameters that we've seen so far (passing a Color to paintSquare) have been data that's necessary to accomplish a task or answer a question. The same logic applies here \- in order to move Binky to the start of the next row, we need a reference to Binky. Any object that you need to refer to should be specified in the comma-separated list of parameters, with a **type** and then a **name**:

```
public static void resetRow(Robot binky) {  
   // code to reset to the next row here  
}
```

What name should you use for the parameter? Anything you want\! Generally, the name should be descriptive **from the perspective of the method**. For this method, since it's resetting Binky to the next row, 'binky' is a nice descriptive name for the Robot.

## Why 'Robot binky'? Why not just 'binky'?

If you've written code in a language like JavaScript or Python before, all this type information may feel excessive \- in JavaScript, the method would in fact look like resetRow(binky). Java requires that types be specified frequently so that it can provide more guidance at compile time (JavaScript happens to be an interpreted language, so there's no "at compile time" there at all). While the compiler can't check the semantics of the code for you, it can spot certain errors \- if resetRow says it expects a Robot named binky, and you try to call the method with Color.RED, the compiler can tell you that that code won't work. As programs get larger and more complex, this becomes very helpful; it's also useful when learning to program as it forces you to be precise about what your code is doing.

You'll notice that when you **call a method**, you do not specify the type of the value passed in - the syntax is `paintSquare(Color.RED)` not `paintSquare(Color Color.RED)`. The type of the parameter is only included in the **method signature**.

## A Quick Note About Types

It may be helpful to mentally read 'SomeType someName' as 'someName the SomeType' \- Binky the Robot is 'Robot binky', Bob the Builder is 'Builder bob'. You can also have multiple objects with the same type \- for example, if I were telling a story about some of my goats, I might mention Roxanne the Goat (Goat roxanne) and Billie Jean the Goat (Goat billieJean). Those two goats can be distinguished using their names \- once I've introduced Roxanne the Goat, I can then just refer to 'Roxanne', and you'll know I'm talking about a goat. Ditto for the compiler \- if I have a parameter Goat roxanne, I can then use just the name roxanne to call additional methods (for example, roxanne.baa()), and the compiler will know that that's alright \- roxanne is a Goat, so she knows how to baa.

## Implementing a Method

Once you have the **method signature**, now you need to fill in the **method implementation**: that's the code needed to actually make the method work the way it's supposed to. We already came up with this resetting code in class, so the whole method will be:

```
public static void resetRow(Robot binky) {
   // move down one row if possible
   binky.turnRight();  
   if (binky.isClear()) {
     binky.moveForward();

     // turn to face east
     binky.turnRight(); 

     // walk to the beginning of the row
     while (binky.isClear()) {  
       binky.moveForward();  
     }

     // turn back around to face west
     binky.turnRight();  
     binky.turnRight(); 
   }
}
```

You'll notice that the code looks the same when it's in the resetRow method as it did in the main method \- that's not a coincidence\! The syntax for the code remains the same regardless of what method it's in.

## Calling Your Custom Method

So far, we've only called methods on objects (ex: binky.moveForward()). Now, we're going to call a method that isn't defined as a behavior on any particular object, so we can just use the method name (if you're curious, this is part of what the **static** keyword means \- any method that does not include **static** in its method signature must be called on an object, any method that does include **static** is not called on an object):

```
Robot binky = new Robot();  
while (binky.isClear()) {  
   //TODO:  fill in an alternating colors row starting with red  
   // reset to the next row  
   resetRow(binky);  
   // TODO: fill in an alternating colors row starting with black  
   // reset to the next row  
   resetRow(binky);  
}
```

This is the first method we've seen where we aren't passing a constant ("hello.world" or Color.RED). To pass an **object**, you just use the name that you chose when creating that object. You'll notice that when **calling** the method, you don't need to specify a type, just the name \- the compiler will check that the type you used when you created your object (`Robot binky = new Robot()`) **matches the type** in the method signature (`resetRow(Robot binky)`). In this example, the names also match, but that's not a requirement.

You'll notice that there's an extra bonus to using the method, aside from not having to repeat all that code a second time \- we can remove the pseudo-code comment and the code is still **readable**. This is what's called **self-documenting code**, and it makes it much easier to figure out what a program is doing (or remember what your program was doing when you see it again):

```
Robot binky = new Robot();  
while (binky.isClear()) {  
   //TODO:  fill in an alternating colors row starting with red  
   resetRow(binky);  
   // TODO: fill in an alternating colors row starting with black  
   resetRow(binky);  
}
```

## When to Create a Method: Next Level

Noticing that you have the same code copy-pasted in multiple places is relatively easy to do once you know to look for it. Where methods become powerful is when you notice that you have **similar** code in multiple places. Specifically, you want to find code that has the **same logic**, but **different values** for objects that are all of a consistent type. For example, if I have code that feeds Roxanne the Goat, and then a separate piece of code that feeds Billie Jean the Goat, the code won't be identical, but it is similar \- it's the same logic, but with a different Goat. If you find yourself tempted to copy-paste some code and then "fix up" a few things, chances are you're in this situation. 

Recall our useful definition of programming: **generalized** problem solving. You can still use a method to simplify code that is similar-but-not-identical, and you'll use a **parameter** to identify the part of the problem that's "generalized" \- your code will turn into a method that can feed **any** Goat, in much the same way that a music player program can play any mp3 file.

In our checkerboard example, the two remaining steps in the program look very similar:  
// TODO: fill in an alternating colors row starting with red  
// TODO: fill in an alternating colors row starting with black

What's different are the colors: the first row will paint squares red then black, and the second will paint squares black then red. While there are some clever tricks you can use to only specify one of these colors as a parameter, when in doubt, go for code that's easy to read rather than clever: we'll have two Color parameters, one for the first color, one for the second:

```
public static void fillInRow(Color first, Color second) {

}
```

But wait\! As soon as you start to write the code, you'll realize there's another parameter that's needed \- Binky is still a part of this method. This is a very common part of **iterating** on your code \- if you find you need another parameter, go ahead and add it:

```
public static void fillInRow(Robot binky, Color first, Color second) {

}
```

Notice that now that we have multiple parameters, they've become a **list separated by commas**. We'll do the same thing when calling the method, but first, let's finish implementing it. The code to paint a row in alternating red and black squares looks like:

```
// Start with a red square
binky.paintSquare(Color.RED); 
 
// Until we reach the end of the row
while (binky.isClear()) {  
  // move forward  
  binky.moveForward();
  
  // create a black square
  binky.paintSquare(Color.BLACK);  

  // if we still haven't reached the end of the row  
  if (binky.isClear()) {  
    binky.moveForward();
	
    // create a red square
    binky.paintSquare(Color.BLACK);  
  }  
}
```

To **generalize** this code to any pair of first and second colors, we'll refer to the parameter by its **name** \- you only need to include the type in the method signature. You can use any parameter just as you would a **constant or literal** \- instead of paintSquare(Color.RED), you can say paintSquare(first):

```
public static void fillInRow(Robot binky, Color first, Color second) {  
  // Start with the first color
  binky.paintSquare(first); 
 
  // Until we reach the end of the row
  while (binky.isClear()) {  
    // move forward  
    binky.moveForward();
  
    // fill in the second color
    binky.paintSquare(second);  

    // if we still haven't reached the end of the row  
    if (binky.isClear()) {  
      binky.moveForward();
	
      // alternate with the first color again
      binky.paintSquare(first);  
    } 
  }	
}
}
```

Now we have a method that can paint a row in **any** two alternating colors\! The solution has been **generalized**, so we can use it to solve the two very similar problems in the main method:

```
Robot binky = new Robot();  
while (binky.isClear()) {  
   //fill in an alternating colors row starting with red  
   fillInRow(binky, Color.RED, Color.BLACK);  
   resetRow(binky);  
   // fill in an alternating colors row starting with black  
   fillInRow(binky, Color.BLACK, Color.RED);  
   resetRow(binky);  
}
```

To pass in multiple parameter values, use a **comma separated list**, this time with **just the names** of objects or constants.

If you were to debug this code, you'd find that it's missing an important check for whether binky is at the end of the world \- let's add that back in, and remove the now-redundant pseudo-code:

```
Robot binky = new Robot();  
while (binky.isClear()) {  
   fillInRow(binky, Color.RED, Color.BLACK);
   resetRow(binky);  
   if (binky.isClear()) {  
     fillInRow(binky, Color.BLACK, Color.RED);  
     resetRow(binky);  
   }  
}
```

Looking at the above code, you might think 'Wow, that looks a lot like the pseudo-code we started with\!', and in fact, this is the way code is written by actual professional developers \- while pseudocode is rarely written out in comments once you're fluent in a programming language, it's still written out with methods, and then as a second step, the method implementations are added (and then the process is repeated as necessary).

## Encapsulation

A theme for programs written in an object-oriented way is **encapsulation**, where detailed semantics about one part of the program are bundled up ("put into a capsule") and hidden from the rest of the program. Thinking back to the lego dinosaur we saw on the first day, the instructions for how to assemble the dinosaur out of legos **encapsulated** the details of how the dino was built. We were then able to interact with the dinosaur without needing to worry about individual legos. Method decomposition is the first example of how we'll add these different layers of details to programs - the outer program can be written without focusing on the details of resetRow or fillInRow. This makes it easier to break down a problem without getting too lost in the specific details on any sub-problem. We'll ramp this up even more when we start creating custom classes (foreshadowing!).
