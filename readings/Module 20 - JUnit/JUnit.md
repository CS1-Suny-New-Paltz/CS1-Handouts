# JUnit Testing

## Introduction

As you've been writing your programs all semester, you've been doing a lot of **manual testing** - any time you've run your program to see if it works, that's a test. As you've probably experienced, that's somewhat time consuming and often inefficient - as it turns out, there's a better way! **Automated testing** takes steps that you would otherwise have to do by hand to test your code, and has the computer run them for you. In Java, the standard framework for doing this is called **JUnit**, short for "Java Unit Testing".

## What is a "Unit Test"?

When testing your code, it turns out it's a good idea to test small pieces (or "units") individually, make sure they all work, and then test how they combine together (technically, this second part is an **integration** or **end-to-end** test, but it turns out you can often use the same framework that works for testing small pieces). A **unit test** is a test of a single small piece of code - for our purposes, we're not going to worry about the distinctions between the different types of testing, although those can become relevant for larger and more complex software systems. You can think of a unit test as an automated test of some or all of a program.

## Why is a "Unit Test"?

Automated testing ends up being a great time-saving device in the long run, but it can feel a little contrived for small programs. In the wild, you rarely spend a few hours writing a program and then never look at it again. Large software projects are under continuous development for decades (GMail, for example, still has dozens of developers working on it even though it's existed for over 20 years), and even a small project will typically be worked on by several people for months. These projects will include dozens up to hundreds or thousands of tests, all of which can be run automatically any time the code changes - definitely not something you'd want to have to do by hand! These tests let you **iterate on a bug** quickly and easily by automatically creating certain conditions (for example, fixing a SlotMachineProgram that only crashes when the first two slots are grapes is much easier when you can run a test that lets you decide what each slot should be), plus they check that as you build more pieces of a program, you aren't accidentally breaking anything that was already working.

## Writing a Good Test

We'll be writing automated tests in Java, which means the code will look very similar to what we've been writing all semester. However, tests are a bit trickier than a regular program, because it's much harder to tell if you've gotten them right. With a program, you can run it and see if it works correctly. With a test, "works correctly" means "detects any bugs if there are any", which is obviously much harder to measure directly. To write a good test, you need to be careful about exactly what the code you're writing does, which means that it's conceptually more challenging than just writing a program.

**Pieces of a test**

An automated test has five parts:

- Set up initial conditions
- Run part or all of a program
- Keep track of what **actually** happened
- Compare that to what was **expected** to happen
- Fail the test if the actual and expected results were different

These parts are usually fairly simple, with 1-3 lines of code for each part. For example, if I had a method called `paintSquareGreen(Robot binky)` in a program `ExampleProgram` that tries to make Binky paint the square he's standing on green, I might write a test for that method that looked like:

```
// Initial conditions: create a Robot and make sure he's standing on a non-green square
Robot binky = new Robot();
binky.paintSquare(Color.RED);

// Run the part of the program we're testing
ExampleProgram.paintSquareGreen(binky);

// Check what actually happened: what color is the square now?
Color actualColor = binky.getSquareColor();

// We expect the color to be green:
Color expectedColor = Color.GREEN;

// Fail the test if the results differ by throwing an exception:
if (!actualColor.equals(expectedColor)) {
  throw new RuntimeException();
}
```

**Making a test fail**

In JUnit, a test fails if and only if it **throws an Exception** - this is a design decision made by the folks who built the framework, and it's not quite as odd as it sounds. It makes sense that if your program were to crash, that's a bug that a test should notice, so a test that throws an Exception should fail. The folks who built JUnit decided that they wanted to keep things simple on their end by deciding that that's the *only* way a test can fail. There are a number of complex ways you can get your code to throw an Exception, but for now we'll stick with `throw new RuntimeException()`. If you're curious and want to write more complex tests, you can poke around a JUnit class called `Assertions` that provides some useful methods for throwing exceptions under certain conditions.

**Common Mistake: Not Fully Automating the Test**

The most common mistake that programmers make when starting to write tests is to have the test print the actual result to the console, and then manually check whether it's what they expected. There are a few problems with doing this: you as the programmer have to keep remembering (or figuring out from scratch) what the expected result actually was for each test, and there's no way to have some other program (such as Github) run all the tests and check the results for you. When you only have one or two tests, this doesn't seem like a big deal, but once you've got a few hundred or thousand tests, you don't want to check each one by hand.

Always include the last two pieces of the test, where you specify the expected result and then throw an Exception if it doesn't match the actual result!

## Syntax To Write a Test

So how do you actually go about writing a JUnit test? To write a Java program, you use `public static void main(String[] args)`, and then the JVM starts running your program from the first line in the main method. To write a JUnit test, you use 

```
@Test
public void ____________() {
            <name of test>
  // your test code here
}
```

The **@Test annotation** looks similar to another annotation we've seen, `@Override` - it's a programmatic marker for a framework (such as JUnit or the Java compiler) to indicate something about your code. JUnit will run any method with the @Test annotation as a test; if you have multiple @Test methods in a class, they will each get run sequentially and you'll get the results of all the tests in a nice list of checkmarks (this is called a **suite of tests**). Under the hood, the various Assignment Checklists are all JUnit test suites, with each item being a single test.

Notice that the test must be **public, void, and with no parameters**. There are unusual and complex tests that have other syntax, but they're uncommon even in real, large programming projects - we won't be writing those.

## Running a Test

To run a test from Eclipse, right-click in the test file and select `Run As > JUnit Test` instead of `Run As > Java Application`. To run your tests automatically from Github, just make sure they're in the test/ folder (next to the src/ folder) in your AssignmentProject. If you're curious how that magically works, go check out the *Continuous Integration* module!
