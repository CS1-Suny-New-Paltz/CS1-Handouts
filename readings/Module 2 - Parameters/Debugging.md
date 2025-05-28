# Debugging

## Introduction

Building a computer program involves 3 major steps:

- Problem solving: break down the overall problem into smaller and smaller steps, represented with pseudo code  
- Translating to code: once you have steps that are small enough that they can be represented in a single line of code, fill in each step with code  
- Debugging: find and fix the differences between what you **intended** the code to do, and what it **actually did**

As it turns out, the better you get at programming, the more time you spend on the last step \- a professional software engineer will spend about 70% of their time debugging. Fortunately, there are a number of tools and techniques to help with this process\!

## What not to do

It’s tempting to try to find bugs by “looking at the code” \- especially because you may notice your TA and professor doing that\! While giving the code a quick once-over is never a bad idea, it’s not **systematic** \- if you don’t immediately see the problem, there’s no way to just “look harder”. The more experience you have, the more often you’ll be able to spot bugs just by looking, but the art of debugging picks up when looking doesn’t work. 

## What to do Instead

Debugging is like solving a mystery \- you assemble clues, form theories, and check whether those theories fit all the data. 

First, identify exactly what causes the problem:

- An automated test failing  
- If manual testing (you ran the program and did some things, and then it either crashed or behaved unexpectedly): what steps did you do precisely?

For example, suppose you were dealing with this code, which crashes into a wall:

```
	public static void main(String[] args) {  
		Robot binky = new Robot();  
		  
		while (true) {  
		    binky.moveForward();  
		}  
	}
```

The cause of the problem would be "Running the program". This is a nice, simple cause, but it's important to identify, because the steps to trigger the problem are what you're going to do repeatedly to track down the bug. One **common mistake** that students make is to try to fix a problem where the cause is "Running the Checklist" by repeatedly running through steps of "Running the program" \- while that can sometimes be useful (see: "reproducing a bug", below), you usually don't want to start with that.

Next, clarify what and where the problem is:

- What does the “not working” look like? This might be an exception causing a crash, a test failure, or an unexpected/incorrect behavior (2 \+ 3 \= 4 is incorrect behavior, 2 \+ 3 \= Unexpected Arithmetic Exception is a crash)  
- Where does the problem happen? Use breakpoints in your code or a stack trace to find **one** place that something is incorrect or unexpected

In our example, the problem is a crash \- when the program runs, it crashes, and prints 

```
Exception in thread "main" binky.BadBinkySituationException: Binky can't go there! Illegal position: (5, 10)  
	at binky.Robot.moveForward(Robot.java:55)  
	at binky.HelloWorldBinky.main(HelloWorldBinky.java:9)

```
 to the console. 

## Gather Data

Programs crashing are actually easier to debug than incorrect behavior \- it's a lot easier to figure out where to start looking\! When a Java program crashes, it generates a **stack trace**: this is a record of what line of code it was trying to run when the crash happened, and context about how it got there. For simple programs, "how the program got there" is usually easy to spot, but as programs get more complex, this becomes increasingly useful.

**Note:** you might notice that a stack trace looks very similar to what shows up in the 'Debug' view when you stop at a breakpoint \- that's not a coincidence\!

## How to read a stack trace:

The exact line where something went wrong is often not useful, because it's within some library \- while IRL you will occasionally find (and have to work around) a bug in 3rd party code, that's unusual and out of scope for this class. Scan down the stack trace, starting from the top, until you find a reference to a file you can edit. This will give you both a file and a **line number** in that file \- for both the console and JUnit views in eclipse, you can **double-click** on that line in the stack trace to open the specific code in the editor.

The other very **useful part** of the stack trace is the **message**: this is right at the top, just before the list of files and line numbers. This message will give you any hints or relevant information that your program had about what went wrong \- sometimes it's just a description of what happened ("dividing by 0"), but sometimes it's more detailed ("There aren't any breadcrumbs on square (0,0)").

Let's apply that to our stack trace from earlier:

```
Exception in thread "main" binky.BadBinkySituationException: Binky can't go there! Illegal position: (5, 10)  
	at binky.Robot.moveForward(Robot.java:55)  
	at binky.HelloWorldBinky.main(HelloWorldBinky.java:9)
```

The Robot.class file isn't one that's editable in any of the assignments \- it's part of the starter code. So moving down the list, we see the problem is in HelloWorldBinky.java, specifically the main method, on line 9 \- there's no line numbers in the earlier code snippet, but that's the line that says 

	binky.moveForward();

The **message** says "Binky can't go there\!", and includes some position information: row 5, column 10\.

Now we have some data\! The crash happens when Binky moves forward, and it's happening because Binky is going somewhere he shouldn't (walking into a wall or off the edge of the world). We also know where on the grid this is happening, which happens not to matter for this bug but is often very useful.

**Form a hypothesis:**

What could cause this behavior? You don't need to know the full chain of logic that leads to this point \- tracking down a bug involves working backwards from where the problem is **observed** (what you found previously) to the **root cause**. While you can always jump ahead if you "see" the bug, this is the process you follow if you don't immediately see what's wrong. For example, in our problem, the hypothesis could be that we aren't checking for the edge of the grid before moving forward. This may sound a bit silly \- of course that's the problem\! What else could it be? Keep in mind, though, you wouldn't be debugging in the first place if the program worked exactly the way you thought it did. The really exciting part of debugging is when you form what you think is an obvious hypothesis, and then it turns out to be wrong.

Part of forming a hypothesis is being specific about **what your code is actually doing** \- while it sounds a bit backwards, sometimes the easiest way to find why your code isn’t doing what you want is to focus on what it’s actually doing instead.

**Test the hypothesis:**  
Run through the code and see if the hypothesis is true by setting a **breakpoint** on a relevant line of code, and checking what specifically is happening. This might involve looking in the **Variables** view to see what values are stored in memory, or using the "Step Over" button to see what line of code runs when (button highlighted in orange below).

![][image1]

If the hypothesis is true, repeat the process to figure out the next cause one back in the chain. If it’s not, come up with an alternate hypothesis.   
	  
In our example, we'd set a breakpoint on the line with the while loop, and then repeatedly step over until Binky was right at the edge of the world. We'd then step over one more time to check the hypothesis \- isClear() would return false (you can double-check this with the **Expressions** view), and yet the moveForward in the while loop is still being run. Therefore, the hypothesis is true \- our while loop isn't checking isClear().

At some point, you’ll find a cause that you can fix (the while loop should check binky.isClear()), and now you’re done\! While for smaller programs, there's often just this one step, by the end of the semester, you'll have programs that will likely involve multiple steps in this process. It's a good idea to **practice** the debugging process now, so that you can effectively tackle more complex bugs later. 

**Reproducing a Bug:**

Sometimes, the steps to trigger the original crash in a program are annoying to have to do repeatedly. Finding a smaller, shorter, more automated, or more informative way of triggering the crash is called **reproducing** the issue, and makes the process of repeatedly triggering the bug more efficient. For example, you may notice that there aren't any graphics when you run the Checklist for an assignment, but being able to visually see what's happening (particularly with Binky) can be useful. If you're able to create a bug in a different way (for example, using a particular world file for Binky and running your program with the graphics), you can use that instead. However, if you **aren't** able to recreate the bug, you may be stuck with running through the original process of triggering the bug.

**Debugging a Checklist Item**

Sometimes, if you run the checklist, you'll see a failure that looks something like this                      →

Which isn't terribly easy to read. While you can scroll right to figure out what's up, you can also click the highlighted icon to copy this information to the **console**, where it's easier to read. 

For this example, you'd then get ![][image2]

which is more like the stack traces we've seen before.

What happens when a test fails, and the stack trace doesn't seem to involve your code at all? Often, it's easiest to treat these failures as a type of **incorrect behavior** (the above example happens when the program claims that 2 \+ 3 \= 4\) rather than a crash \- you can use the **error message** to find out more details about exactly what was incorrect. The checklist items are sometimes deliberately vague, however \- when that happens, you should see if you can **reproduce the bug** outside the checklist framework.

If you aren't able to reproduce the bug, you can use **breakpoints** in your code to get a better sense of what the Checklist is doing \- put a breakpoint somewhere plausible, and then run the checklist item in **Debug Mode** (Debug As \> instead of Run As \>). You'll be able to use the **Variables** view to see what's going on in your program, which can help track down the problem.

If you get completely stuck: you can ask your TA or professor to take a look at the code on github. Make sure you include what steps you've already tried when you ask\! Otherwise you may just get advice to try those steps again, since we won't generally just tell you the answer \- you'll just get advice on how to move forward in the debugging process yourself.  
