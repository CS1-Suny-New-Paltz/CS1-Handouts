# Introducing Binky the Robot

## Introduction

The idea of an introductory programming robot has been around for a long time \- the first version, named Karel, was introduced in the 1970's by Stanford graduate student Rich Pattis, who wanted a simple way for students to interact with their first programs. He chose to call his robot Karel, named for the Czech playwright [Karel Čapek](https://en.wikipedia.org/wiki/Karel_%C4%8Capek), whose 1923 play [Rossum’s Universal Robots](https://en.wikipedia.org/wiki/R.U.R.) introduced the word "robot" to the English language. We'll be using a similar robot, who was christened Binky by Stanford lecturer Nick Parlante in the early 2000's, for inscrutable reasons of his own. By informal popular vote, previous semesters' students prefer Binky to Karel, so we'll be using that nomenclature. 

## Binky's World

Binky lives in a simple grid of squares. These squares can be different colors or contain walls, and Binky can navigate through them, dropping breadcrumbs (serving as Hansel-and-Gretel style markers) as navigational beacons. To start, we'll have Binky respond to some fairly basic commands: it can move forward by a single square, turn left or right, and drop a breadcrumb.

## Terminology

Java is an **object-oriented** language \- most Java code involves interacting with **objects** via **methods.** Objects generally correspond to nouns, and methods to verbs; as you read Java code, this makes it easy to figure out what real-world or practical application a single line of code corresponds to. For example, if you wanted to describe "a student enters a classroom" in Java, you might call the method enterClassroom() on an object of type Student.

## Syntax

<img align="right" src="images/ameliaBedelia.jpg" alt="Amelia Bedelia" width="20%"/>

While we fortunately don't have to deal with punch cards anymore, giving instructions to a computer still requires precise formatting. This avoids any of the ambiguity so easily found in plain-English communication (for those of you familiar with the children's book character Amelia Bedelia, you'll know all about this). The formatting for these precise instructions is called **programming syntax**, and it varies depending on what programming language you use. Fortunately, there tend to be a lot of similarities \- once you learn one programming language, picking up the syntax for a second is pretty easy\!

As you write more code, the syntax for Java quickly becomes second nature. When you're getting used to programming syntax for the first time, though, it can be helpful to use a mad-libs style **template** \- this is a pattern that you can apply to various scenarios. It's recommended that you include the templates for any syntax you find tricky to remember in your quiz notes\!

To work with Binky, we'll need a couple pieces of syntax:

**Leaving a comment in the code:**

// \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_  
    (any text you want on this line)

To add some plain-English description of what's going on in your program, you can leave a comment with //. Anything after the // on that line will be ignored by the compiler.

For example:  
`// This is our first program with Binky!`

**Creating a new object:**

\_\_\_\_\_\_\_\_\_\_\_\__\_\_\_\_&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \= new \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ ();  
(Type of object)&nbsp;&nbsp;&nbsp;(name for this specific instance)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(Type of object, same as before) 

Binky is a Robot, so to create one:

`Robot binky = new Robot();`

Note that an object type always starts with a capital letter, and a name for a specific instance always starts with a lowercase letter.

**Calling a method on an object:**

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_._\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_();  
(name for the specific instance)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(name of method)

The '.' (dot) here is easy to miss but very important\! 

If we wanted to combine our previous line with a line to make Binky walk forward one square:

`binky.moveForward();`

**Syntax is Precise**

Everything in the previous lines is important \- you must include the parentheses (eventually, we'll see methods where the parentheses aren't empty, but for now they are), you must include the semi-colon, and you need to be careful where you put spaces and how you capitalize things. Any errors in formatting will cause a **compile error**, where Eclipse isn't able to turn your code into the machine-code instructions that the computer will actually run.

## Methods that Binky (or any Robot) can respond to

```
// Has Binky walk forward one square in whatever direction it's facing  
moveForward(); 

turnRight();  // Has Binky turn 90 degrees to the right  
turnLeft(); // Has Binky turn 90 degrees to the left  
dropBreadcrumb(); // Has Binky drop a breadcrumb on this square  
pickUpBreadcrumb(); // Has Binky pick up a breadcrumb from this square
```

If you look up these methods in Robot.class in Eclipse, you may notice they show up a bit differently than what’s written here. Specifically, they show up as something like:

`public void turnRight()`

**void** is a **keyword** in Java that means “this method doesn’t return anything” (a **keyword** is a special piece of syntax with some specific meaning \- we already saw another one of these with the **new** keyword). This raises the question, what does it mean for a method to return something? We’ll get to that in the next section\!

## Return Values

In addition to moving around and interacting with the world, Binky can also answer simple questions about the world. For right now, Binky can answer two true/false questions: is the square in front of Binky clear to move into (ie, not a wall/other obstruction), and does the square that Binky is standing on have at least one breadcrumb. In Java, objects can answer questions (or even return object data) using what’s called a **return value** for a method. This generally lines up well with real world interactions. For example, imagine buying a soda at a convenience store. You give the cashier money for the soda, and the cashier **returns** your change. Similarly, if you ask someone a question, they give you (or **return**) an answer.

The name for a true/false return value is a **boolean** (that’s actually the name for any true/false value anywhere in a program) \- when you see the description of a method (sometimes called the **method signature**), that description will include what (if anything) the method returns. 

Specifically, Binky has the following methods:  
```
boolean isClear(); // Returns ‘true’ if the square in front of Binky is clear and safe to move into

// Returns ‘true’ if the square that Binky is on has one (or more) breadcrumbs  
boolean squareHasBreadcrumb();
```

## Using Return Values: Control Structures

Asking Binky questions isn’t very useful if you can’t do anything with the answers. A **control structure** is a programming concept that lets you do something other than just run lines of code one right after another. The first control structure we’ll look at is called a **conditional**, represented by the keyword **if**. Imagine you wanted to write some code that represented “If Binky is standing on a square with a breadcrumb, pick up the breadcrumb”. You can use a **conditional** to only run some code if a particular condition is true.

Syntax Template:

```
if (____________________________ ) {  
     (some true/false condition)

     ________________________________________________________________ 
     (one or more lines of code to only run if the condition is true)
    
}
```

Syntax note: every time you see a {, the next lines should be **indented** until a } \- this makes it easy to see at a glance what code will only run conditionally.

So the code for “If Binky is standing on a square with a breadcrumb, pick up the breadcrumb” would be:
```
if (binky.squareHasBreadcrumb()) {  
  binky.pickUpBreadcrumb();  
}
```

What about if you want to do something **until** a condition is true or false? For example, “Until Binky is at a wall, keep moving forward”. To do this, we’ll use a **loop** \- the syntax for this is very similar to a conditional. In fact, the only difference in the syntax is using the keyword **while** instead of **if**

```
while ( ______________________ ) {  
     (some true/false condition)  
     
    ____________________________________________________________________  
    (one or more lines of code to only run until the condition is false)

}
```

So to express “Until Binky is at a wall, keep moving forward”

```
while (binky.isClear()) {  
  binky.moveForward();  
}
```

## Error Conditions

What happens if you ask Binky to do something "illegal", such as walk past the walls at the edge of its world, or pick up a non-existent breadcrumb?

If your program gets into an invalid state (dividing by zero, walking into walls, etc), it will **throw an Exception.** For right now, that means the program will **crash** \- it will stop running and print some information about what happened to the console (the console is where "Hello World" showed up when you ran that program). This information contains two things:

- A message about what went wrong (ex: "Binky tried to walk through a wall\!")  
- A **stack trace** showing what line of code was the **immediate** cause of the problem. You'll want to look at the top-most line that's in a .java file you wrote. Keep in mind that this line isn't always the **root cause** of the problem; tracking that down is part of a process called **debugging**. However, this line does give you a place to start. We'll look at debugging in the next set of readings.

