# Javadocs

## Introduction

In an object-oriented language, there are a potentially infinite number of classes that can be used as object types. Knowing how to approach and use a new class that you've never seen before is an important part of using such a language. Fortunately, the overall structure of documentation for a class is similar across various languages - while we'll be learning the Java version, generalizing to other object-oriented languages is straightforward.

## Java Documentation ("Javadoc")

Classes often include a special comment syntax to leave documentation comments. These comments are set up to explain how to use a class. To create such a comment, you can use the following template:

```
/**__________________________*/ 
   (any text for a comment)
```

There are tools that will extract and format these comments into a useful summary, often available online. For example, the javadoc for the Random class that we saw last class can be found here: [Javadoc for Random](https://docs.oracle.com/javase/8/docs/api/java/util/Random.html) 

You'll notice there's a lot of information there\! Javadocs typically include:

- Any **constructors**, which are the special method-like calls combined with **new**  
- Any **methods**, including parameters and return values

They may also include an overall description of the class, and sample code for how to use the class and its methods.

The two most useful sections of the Javadoc are the **constructor summary** and the **method summary** \- this gives you an overview of how to create an object of this type, and what objects of that type can do.

**Assignment Classes**

For many of the assignments going forward, there will be new classes included in the assignment. Whenever that happens, the assignment will include the **javadoc** for each class, with the constructor and methods that you can use.

## Using a New Class

When in doubt, try out some code\! To start using a class, you first need to **construct** an instance of it. For example purposes, we'll consider the following class

`class Goat`

Constructor

`public Goat(int age)`  
Takes in the age in years of the goat

Methods

`public void baa()`  
Prints the noise the goat makes to the console

`public String getName()`  
Returns the goat's name


To construct a new goat, we'll need to call a constructor \- in this case, there's only one option, a constructor that has one parameter. To see exactly what a Goat object can do, we'll make a small program:

`Goat exampleGoat = new Goat(1);`

To start, this creates an exampleGoat of type Goat, where we're passing a value of '1' for the age of the goat in years. The variable name and age value here are for example purposes \- you could pick any name/age combo that you want.

## The **static** keyword

You'll notice that unlike the methods we've been creating so far, the methods in the section above are **not static**. A **static** method is one that can run with just the information that's publically available from its parameters. On the other hand, if an object type has a method that depends on private, internal data related to that object, it will define a method that must be **called on a particular object**.

For example, the `isClear` method on the Robot class must be called on a specific Robot (such as Binky). Whether or not Binky is clear to move forward depends on where exactly he is in the world \- it doesn't really make sense to ask "are Robots, generally, clear to move forward?", but it does make sense to ask "is this specific Robot, Binky, clear to move forward?". When creating a new object type, the methods involved are usually **not static**, which means that in order to use them, a program first needs to create a **variable of that type**.


## Calling a Method

Now we want to see what noise the goat makes \- the description of the baa() method gives an idea of what's going to happen, but it would be nice to get more details. Since baa() is not static, we need a variable of type Goat to call it. Fortunately, we just created one that we can use:

```
Goat exampleGoat = new Goat(1);  
exampleGoat.baa();
```

Running this code, the following shows up in the console:

`Meh!`

Interesting\! Now we have a sample of the sort of noise a Goat will make. Of course, there's no guarantee that that's **always** the noise a goat will make \- in fact, given the description of the method, there probably are other options (folks who write Javadocs will try not to be misleading or purposefully vague) \- but it's a useful piece of information nonetheless. If instead of printing "Meh\!", the method had printed

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
```

That might change how we'd use the baa() method in a program (for example, adding a scroll bar or ellipses around it might make sense in the latter case, but not the former). Alternatively, the whole program might have crashed with

```
InvalidGoatException: All goats must be at least 2 years old to baa
```

which would also provide some useful information about how to use the Goat class. Using a new class almost always involves a bit of experimentation combined with the documentation.

## Using a New Class in a Program

Suppose you were trying to write a program with the following goal: Simulate a small barnyard by having 3 goats all make noise one after another.

Breaking this down into pseudocode, we could get:

```
// Create 3 goats  
// For each goat, have it make noise
```

As you write the pseudocode, keep an eye out for any parts of the problem that can be solved by the new class you've just encountered. In this case, because we have access to a Goat class with a baa() method, we don't need to break the problem down any further \- the new class we've found already solves the sub-problems from the pseudocode:

```
// Create 3 goats  
Goat goatOne = new Goat(1);  
Goat goatTwo = new Goat(2);  
Goat goatThree = new Goat(5);

// For each goat, have it make noise  
goatOne.baa();  
goatTwo.baa();  
goatThree.baa();
```

Note: if you saw that 'for each' and thought 'that seems like a loop', good call\! We'll see a way to combine data and loops when we get to arrays and Lists.