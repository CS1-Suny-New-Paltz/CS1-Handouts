# Primitive Types

## Introduction

**Note:** if you haven't read the 'Variables' handout yet, read that first. 

There are two kinds of data types in Java \- object types (Robot, String, Color, etc) and **primitive types**. Primitive types are the building blocks for all the other types \- you can think of them as single legos. These types work slightly differently from the object types we've used so far.

# Why Primitive Types?

Fundamentally, primitive types exist because of memory management \- every piece of information in a program must be written down in memory. This in turn runs into a bootstrapping problem \- if you ask the computer for, say, 400 bytes to store some information, the computer will reserve those 400 bytes for you, and give you a **memory address** to refer to them. This works much like a physical address \- it's a short way to reference some location. Unfortunately, in order for your program to keep track of the address, it needs to write it down in memory, and now it needs to keep track of where it wrote down that address. To keep from having an infinite chain of addresses, a program starts with a list (called a **stack**) of small, fixed size memory spaces (this is a slight simplification, an operating systems or assembly class will give you more details, but it works for our purposes). 

A primitive type is a **small, fixed size** piece of data where it would take just as much, if not more, memory in the stack to record an address for the data as it would to just write the data down directly. The syntax for these types is a holdover from earlier languages (C and C++), and continues in many other languages \- programming languages are heavily influenced by their predecessors. Unfortunately, that means that the code for interacting with a primitive type can look fairly different from the code for interacting with an object type \- clear pseudocode can help keep you out of trouble here.

# Primitive Type Syntax

Unlike object types, where you can create new ones of your own (and therefore have a potentially infinite variety), primitive types are built into the Java language, and there are only a few of them. The main ones, which we'll be using for this course, are the following:

`boolean` \- we've already seen this type a bit, it represents either true or false

`int` \- short for 'integer', this type represents whole numbers (1, 2, \-35, etc)

`char` \- pronounced 'car' and short for 'character' (the pronunciation matches neither how it's spelled nor how 'character' is pronounced, but instead is a mishmash of the two, just to keep things interesting), this type represents a single letter. Unlike String, which can represent arbitrary text and uses double-quotes (" "), char uses single quotes around a specific character (ex: 'a', 'x', '?', ' ').

`double` \- the least-obviously named type, double is short for 'double precision floating point number', but it's most easily thought of as a decimal (ex: 3.14, 1.23456).

Other primitive types tend to be related to those four \- for example, a long is an int that uses 8 bytes instead of 4, and can therefore represent larger numbers (ints max out at around 2 billion); a short is an int that only uses 2 bytes, and can only represent numbers up to about 65,000. For our purposes, boolean, int, char, and double are fine, since we're not getting into the details of memory management based performance tuning.

## Primitive Types and Operators

Unlike object types, primitive types don't support methods, and instead use operators. We've seen one operator already: **\!** to apply **negation** to a boolean type. Other operators in Java are basic mathematical ones:

\+  addition  
\-   subtraction  
\*   multiplication  
/   division

and boolean logic operators:

	\!   negation  
            &&   conjunction ('and')  
	||      disjunction ('or' \- note that true || true is also true; this is an 'inclusive or' where at   
least one or possibly both sides are true)  
            \==    equality  
            \!=     inequality  
            \<, \>  less than, greater than; ie, true when the value on the wide side is bigger than the   
value on the narrow side  
            \<=, \>=   less than or equal, greater than or equal

There are a few other specialized operators that we won't cover, but you should be aware that a single & or | is both a valid operator and almost certainly doesn't do what you want (those perform a bitwise and/or of the binary representation of the two values). Make sure to use && and || for a logical and/or.

The syntax for the operators likely looks familiar:

`int x = 2 + 3;`

will apply the '+' operator to the two values on either side, calculate a result of 5, and store that value on the stack \- the variable x will then refer to that value (at least initially \- remember, variables can change their values\!).

## Object Types and Operators

For the most part, using operators with object types will not compile, which makes sense \- it's not clear what

`binky + Color.RED`

would even mean. However, there are two exceptions, one of which is common and correct, and the other is a common source of bugs.

**String Concatenation**

If you want to combine two pieces of text, or text and a primitive type, you can use \+. String is often a special case in Java, and this is an example. "Hello" \+ " World" will produce the String "Hello World". Be careful with ordering when combining this with mathematical operators:

```
int x = 2;  
int y = 3;  
String result = "Result is: " + x + y;
```

will have a result of "Result is: 23" instead of "Result is: 5"

To avoid unexpected behavior, make sure to always use parentheses\!

```
String result = "Result is: " + (x + y);
```

or

```
String result = ("Result is: " + x) + y;
```

are both much clearer about the intended behavior.

**Object Equality**

A really common source of bugs is using \== with object types instead of .equals \- this compiles, and has a meaning that means it **sometimes** works (which is the worst kind of bug), but what it's doing under the hood is comparing **memory addresses**. This is often, but not always, the same as **semantic equality**, which is what .equals uses. So for example:

```
"Hello".equals("Hello"); // returns true  
"Hello" == "Hello"; // returns true
```

but:

```
"Hello World".equals("Hello" + " World"); // returns true  
"Hello World" == ("Hello" + " World"); // returns false
```

The difference is whether or not the computer is storing the particular String in the same spot in memory or not, which isn't usually what you care about when seeing if two Strings are "the same". As a best practice **never use \== with object types**, even though the compiler will let you.

## Optional: Shorthand with Operators

When reading other people's code (in example snippets, other classes, etc), you'll likely run across at least some shorthand operators. These are not required for this class (although they'll occasionally show up in in-class examples), and don't do anything special \- they're just slightly more compact ways of saying the same thing, for particularly common operations. It's nice to be familiar with them even if you don't want to use them yourself.

| Task | Long-hand version example | Short-hand version of the same |
| :---- | :---- | :---- |
| Updating a value | x \= x \+ 2; // increases x by 2 y \= y \* 3; // increases y by a                 // factor of 3 | x \+= 2; y \*= 3; |
| Incrementing a value by 1 | x \= x \+ 1; | x++; |

If you're wondering how C++ got its name: it's claiming to be "one better" than the programming language C.