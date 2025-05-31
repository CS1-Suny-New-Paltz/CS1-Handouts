# For Loops

## Introduction

Programming languages often include more features than are strictly necessary for Turing completeness, which make it either easier or faster to write programs. For loops are an example of that \- they provide a shorthand version of a very common use case for `while` loops. 

## Looping a Known Number of Times

For most of the `while` loops that we've seen so far, the loops will execute an unknown number of times depending on what Binky's world looks like. For example, `while (binky.isClear())` is a loop that will keep running until Binky finds a wall, which might be once, twenty, or any number of times \- it depends on where the walls are in the world.

Sometimes, though, a loop will execute for a **fixed** number of times, generally stored in a **variable**. For example, if you had Binky count the number of breadcrumbs in a square and then move forward that many squares, you might have a loop that looks like:

```
int numBreadcrumbs = countBreadcrumbs(binky);

int numSquaresMoved = 0;  
while (numSquaresMoved < numBreadcrumbs) {  
   binky.moveForward();  
   numSquaresMoved = numSquaresMoved + 1  
}
```

In this code, numSquaresMoved is sometimes called the **counter** or **loop variable** \- the loop should execute a fixed number of times (numBreadcrumbs times), and numSquaresMoved counts the number of loops until it reaches the target count. 

## For Loops: Avoiding Common Bugs

It turns out that looping a fixed number of times is a very common piece of code, and it's also prone to a very common bug: forgetting to update the counter.

```
int numBreadcrumbs = countBreadcrumbs(binky);

int numSquaresMoved = 0;  
while (numSquaresMoved < numBreadcrumbs) {  
   binky.moveForward();  
}
```

is an easy piece of code to write, but it will loop forever (or until Binky runs into a wall), because numSquaresMoved isn't getting updated. The `for` loop construction lets the compiler double check that you haven't missed any pieces of the loop, by putting them all in one statement:

```
for (______________________________;  ___________________;   __________________) {  
     (declare and initialize counter)   (loop condition)       (update counter)

   ___________________________________
        (code to run repeatedly)

}
```

Applying that template to our earlier code: 
 
`int numSquaresMoved = 0;`   

is the line that declares and initializes the counter  

`numSquaresMoved < numBreadcrumbs`
  
is the loop condition  

and   

`numSquaresMoved = numSquaresMoved + 1`
  
is the update step for the counter.

Important note: the update step always runs at the **end** of the loop \- that matches our `while` loop example in this case, but it's good to keep in mind when you write your own loops.

So using a `for` loop, the previous code becomes:

```
int numBreadcrumbs = countBreadcrumbs(binky);

for (int numSquaresMoved = 0; numSquaresMoved < numBreadcrumbs; numSquaresMoved = numSquaresMoved + 1)  
   binky.moveForward();  
}
```

## Incrementing Shorthand

Remember the shorthand for incrementing a value by 1?   
`numSquaresMoved = numSquaresMoved + 1`  
Can be rewritten as  
`numSquaresMoved += 1`  
or  
`numSquaresMoved++`

The most common reason to use the `++` shorthand is in a `for` loop \- because the update step is very often just an increment-by-one, you can then write:

```
int numBreadcrumbs = countBreadcrumbs(binky);

for (int numSquaresMoved = 0; numSquaresMoved < numBreadcrumbs; numSquaresMoved++)  
   binky.moveForward();  
}
```

## i: The Universal Counter

In many cases with a `for` loop, the counter is only used to count the number of times through the loop. Giving the counter a descriptive name can become tricky and feel contrived. By convention, if the counter is **just for counting** and doesn't have any other semantic meaning, it gets the name 'i'. So our loop now simplifies even further:

```
for (int i = 0; i < numBreadcrumbs; i++)  
   binky.moveForward();  
}
```

There's a lot of interesting semantics packed into that one line\! As a practical shorthand, you can often use the template

```
for (int i = 0; i < ______________________________; i++) {  
                   (number of times through the loop)

    __________________________________
      (code to loop through)

}
```

However, it's important to know what all the pieces are actually doing \- when we get to Strings and arrays, we'll see examples of `for` loops where the counter is used **inside the loop**; those are situations where all three pieces of the loop may end up getting changed slightly. For example, if it were important to count down from numBreadcrumbs rather than up, you could use the loop

```
for (int i = numBreadcrumbs; i > 0; i-- )  
   binky.moveForward();  
}
```

When in doubt, you can always write your code as a **while loop first**, and then convert to a `for` loop to double-check that you've included the 'update the counter' step. Eventually, the `for` loop will start to feel natural to use directly.