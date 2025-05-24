# Pseudo Code

## Introduction

There are three main stages to writing a program:

- breaking the overall problem down into small steps
- turning those steps into code
- debugging the result.

Many students are tempted to combine step 1 and step 2 as a shortcut, but doing that ends up taking **much longer** (and being kind of a miserable experience along the way). To see what's going wrong here, imagine being asked to write a 20 page research paper about the price of potatoes, but with the additional requirement that the paper be in Swahili (or some other language that you don’t speak at all). Option 1 is to write a paper about potatoes in English, and then translate it into Swahili sentence by sentence. Option 2 is to try to translate it as you go and only write down actual Swahili sentences. As you can imagine, option 2 won’t go particularly well \- you’ll keep losing your train of thought as you look up “potato” in your English \<-\> Swahili dictionary. Essentially, you’ll be trying to craft, memorize, and recite your 20 page paper without ever writing it down and while constantly being distracted by looking up vocabulary and grammar for Swahili. For someone who’s fluent in Swahili, option 2 is great, but for someone who isn’t (yet), splitting out “creating a new thing” from “translating to a specific language” makes the overall process much smoother. The old adage "slow is smooth, smooth is fast" applies here \- take the time to write code methodically, and you'll be done before you know it.

## Pseudo Code

For our purposes, Java is the language that you’re not fluent in yet (by the end of the semester, that will change\!). As you figure out how to write code, it’s helpful to separate the **problem solving** aspect from the specific Java **syntax**. Pseudo code is a series of small instructions written in plain English in comments in a .java file that represents the solution to a programming problem. While it doesn’t use any Java-specific syntax, the instructions are small and precise enough that they can each be translated as a single line of code. 

If you end up interviewing for a programming job, often interviews are done in pseudo code \- this lets the interviewer see your thought process without focusing too much on any particular programming language. This also means you can use pseudo code to write a program in **any programming language** \- getting good at this process will make picking up another language (Python, TypeScript, C\#, or whatever's appropriate for a task) much easier.

## Breaking a Problem Down

Imagine you’re giving instructions to an energetic but slightly confused kindergarten student. If you accidentally give an instruction that’s too complicated, the small child will look at you and say “How do I do that?”. If that happens, you have to break down that particular instruction into even smaller steps. When writing pseudo code, the small child in question is your compiler \- you'll need to break the problem down into small enough steps that you can express each step in one line of code.

In practice, you can do this by leaving comments in code. For example, suppose you want to create a program where Binky will walk in a square, leaving breadcrumbs as it goes (Note: If you haven’t read ‘Intro to Binky', you may want to do that now). To start, our program is short but the steps are too complicated:

`// Have Binky walk in a square, leaving breadcrumbs as it goes`

There’s no clear method that we can call to accomplish this task in a single line of code, so let’s break it down further:

```
// Have Binky walk along the top of the square, leaving breadcrumbs as it goes  
// Have Binky walk along the right edge of the square, leaving breadcrumbs as it goes  
// Have Binky walk along the bottom of the square, leaving breadcrumbs as it goes  
// Have Binky walk along the left edge of the square, leaving breadcrumbs as it goes
```

Great\! Except these steps are still too complex. Let’s simplify the first one:

```
// Have Binky walk forward until it reaches the corner of the square.  
// On each square, leave a breadcrumb
```

Well now. Some of those steps look like methods or control structures that we can express directly in Java\! Let’s rephrase a bit to make sure we’re on the right track:

```
// While Binky is not at the corner of the square (hmm):  
  // walk forward  
  // drop a breadcrumb
```

If we wanted to actually write java code for this, we’d need to clarify what “at the corner of the square” means, but otherwise we've got the problem broken down into small enough steps that it can be directly translated into code by applying a **syntax template**. For example:

```
  // walk forward
  binky.moveForward();
```
