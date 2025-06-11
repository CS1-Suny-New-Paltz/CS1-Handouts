# 2D Arrays

## Introduction

An array can contain any type of data \- that includes another array\! In theory, you can add as many dimensions to an array as you would like, but in practice, more than two is unusual. While the general idea behind a 2D array is relatively straightforward, it's worth discussing the syntax and common use cases in a bit more depth.

## Syntax

Fortunately, the syntax for a 2D array is largely what you would expect: to create a regular array, you use the syntax template:

```
______________[] _________________;  
(type of data)    (variable name)
```

For example,

`int[] arrayOfInts;`

declares an array called arrayOfInts that stores many pieces of data of type int.

To create an array of arrays, the type of data being stored **is itself an array**, so the type of data is the array type. For example,

`int[][] twoDimensions;`

declares an array called twoDimensions that stores many arrays of integers.

To initialize a 2D array, it’s very similar to a 1D array, but you must specify all the dimensions at once:

`int[][] twoDimensions = new int[2][10];`

Creates a 2x10 grid of integers. Similarly, accessing a specific spot in that grid requires two sub-indexes:

`twoDimensions[0][0] = 1;`

stores the value 1 into the spot in the first row and first column of the 2D array.

## Common Uses

2D arrays are typically used to model real-world concepts that are laid out in a grid or board of some sort \- if you’d use rows and columns to describe the real-world object, a 2D array is a good fit; otherwise, you likely want an array of a some new custom object type stored in a different class. For example, let’s say you had 10 students, and each student had an age, number of classes they were taking, and id number. While you *could* represent this as a 2D array of ints, you shouldn’t \- the code to reference the 4th student’s id number would look like   
`studentArray[3][1]`, which is fairly confusing. Instead, you’d create a Student class with 3 instance variables (age, number of classes, and id number), and a 1D array of Student. Now, the code to reference the 4th student’s id number would look like `studentArray[3].getIdNumber()`, which is much clearer.

On the other hand, if you were trying to represent a chess board, you would nearly always refer to squares by a combination of their row and column. In that case, `board[3][2]` would make a bit more sense \- that’s the square in the 4th row and 3rd column (remember, everything starts counting at 0\!).

This explains why higher-dimension arrays are uncommon \- outside of an advanced math or physics context, 4 dimensional hypercubes don’t show up very frequently, so there aren’t a lot of real-world concepts that are naturally modelled with a 4D array.

## Nested For Loops and 2D Arrays: Peanut Butter & Jelly

To deal with a single array, you typically use a for loop. Similarly, to deal with an array of arrays, you use a loop of loops: one loop inside another. These are often called **nested for loops**.

The pseudo-code for this often looks something like:

```
// for every row on the board  
   // for every square in that row  
      // do something with that square
```

And the corresponding Java syntax:

```
for (int i = 0; i < NUM_ROWS; i++) {  
   for (int j = 0; j < NUM_COLS; j++) {  
     // do something with board[i][j]  
  }  
}
```

While it’s a good idea to use the `length` instance variable to iterate over a 1D array (it reduces the chance of ArrayIndexOutOfBoundsExceptions caused by off-by-one errors), the syntax for that with 2D arrays looks a little weird \- `board.length` will give the number of rows, but to get the number of columns, you have to check the length of the row with `board[0].length`. For the sake of readability, using a constant to both initialize and iterate over the 2D array is generally easier.  
