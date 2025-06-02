# Strings

## Introduction

While "text" doesn't sound like that interesting or complex of a topic at first, it turns out that Strings are one of the most powerful building blocks for programs: any data can be represented in text form, and that data can be arbitrarily changed and updated by manipulating that text. We'll go over some of the more common ways to use and manipulate Strings.

## The String class

In some programming languages (such as C++), a string is a predefined type (much like an int). In Java, a String is an object type, but it has some unique syntax that means it behaves like a hybrid of primitive and object types: it supports operators (such as '+') and can be declared as a literal with double-quotes (similar to a primitive type), but it's stored in memory as a pointer to data, and supports having methods called on it.

## Initializing a String

As an object type, you would expect to create a new String object by calling some variation of `new String()` \- just as a robot is created with `Robot binky = new Robot();`, a String should be created with `String text = new String();`. Good news\! You can, in fact, create a String that way \- String has two commonly-used constructors, a 0-parameter version (`new String()`) that creates an **empty String**, and a 1-parameter version that takes in another String and makes a copy of it (`new String("Hello World")`). More commonly, though, a String is created by declaring a **string literal** using double-quotes: 
  
`String text = "Hello World";`

While it doesn't come up that often, it's good to keep in mind that literals (such as Color.RED, "Hello World", or 1\) all have a type, and using them to initialize a variable requires that the types match.

## The Empty String

Much like 'what is the sound of one hand clapping', 'what is text with no letters' sounds like another unanswerable Zen koan. However, this actually has a well-defined meaning in programming \- the **empty string** is a String that isn't null, but which contains no actual letters; it's the text equivalent of 0 for numbers. To declare an empty String, you can use either the 0-argument constructor or two double-quotes with nothing between them \- so while `"a"` creates a String with one letter, `""` creates a String with no letters. This is a surprisingly common element in programs, because it makes a good **initial value** for "building up" a String. Just as you would start a counter at 0 when counting the breadcrumbs in a square and then increment the value, if you're building a complex piece of text, you can start with "" and build up from there.

## Converting to/from other types

When converting between types, you'll use an appropriate **static method** for the type you're converting to. For example, to create an int from a String, you'd use Integer.parseInt \- that method takes in a String as a parameter, and returns the corresponding int (assuming the String represented an integer in the first place). To convert any type of data (primitive or not) back to a String, use the method `String.valueOf`. This method is **overloaded** for every possible primitive and object type, so you can pass in any value and get the String representation back.

For example:

`int value = Integer.parseInt("1");`

converts a String to an int, while

`String value = String.valueOf(1);`

converts an int to a String. You can also pass in a variable:

```
int original = 13;
String textVersion = String.valueOf(original);
int convertedBack = Integer.parseInt(textVersion);
```

## Working With Strings

Strings in Java are what is known as **immutable** (or "not mutable"). A mutable object is one that can be changed (or "mutated"), so conversely, an immutable object is one where the **data can't change**. Specifically for object types, this means the data stored in the **pointee** cannot change \- the **pointer** can be updated to point to new, updated data. This means that for immutable objects, if you have two variables that both point to the same pointee, you don't have to worry about the data changing out from under you (unlike in the Binky Pointer Fun video, where updating the value stored in the pointee for x ended up changing the value for y as well). 

**Manipulating Strings**

Given that Strings are immutable, every way of "manipulating" a String is actually creating a new, updated String and returning that. This means that in your code, you'll never call a method to manipulate a String without also assigning the return value to a variable \- this is very different from how Binky operates. So while you could call

`binky.moveForward();`

and Binky would move, if you call

`textValue.toLowerCase();`

nothing would end up happening \- instead, you'd need to write

`textValue = textValue.toLowerCase();`

which will update the textValue **pointer** to refer to the pointee returned by toLowerCase() (don't worry, we haven't talked about that method yet, although I bet you can guess what it does).

**Combining Strings**

We've already seen the concatenation operator, \+, for combining Strings, or Strings and other values. If you're writing performance-sensitive code, there's another useful class called StringBuilder that can perform repeated concatenations more efficiently \- it's unusual to actually need this class in practice, but sometimes people on the internet like to show off, so it shows up on places like stackoverflow more than you'd expect. If you see it, now you know what it is, but you won't need it for this class.

**Formatting Strings**

It's often helpful to "standardize" Strings for certain problems \- by default, Strings are case-sensitive ("Hello" is not the same as "hello") and whitepace sensitive ("Hello " is not the same as "Hello"). For certain situations (such as user passwords, or building up long sentences), both of these features are useful, but for other situations (ex: searching for a word on a page), you might want to "opt out" of that behavior.

To avoid case sensitivity issues, you can convert strings to all upper (or all lower) case letters with toUpperCase() and toLowerCase() respectively \- while "The cat sat on the mat" doesn't contain the String "Cat", if both String objects are converted to lowercase versions ("the cat sat on the mat" and "cat"), now there is a match for the text being searched for.

Removing whitespace usually happens when dealing with user or file input that might be a bit "messy". Recall our todo list example, with one task per line \- it would be easy to accidentally include a space at the end of one of the lines when creating the file, because as a person reading the text file, whitespace at the end of a line is invisible. The method trim() removes spaces, tabs, and newlines ("whitespace" characters because they show up as blank space \- traditionally, that space was white back before dark mode became a common feature) from the beginning or end of a String. For example, " Hello ".trim() would return the String "Hello". 

**Separating Strings**

To grab a single letter from a string, you can use the method charAt (short for “character at”), which takes a single integer parameter:

`char charAt(int index)`

The “index” here refers to where the character is \- is it the first, second, third, etc letter in the String. As with most things programming-related, this is 0-indexed \- “Hello”.charAt(0) will return ‘H’, and “Hello”.charAt(1) will return ‘e’. It can often be helpful to draw a visual for working with a String to mark each  character with the corresponding index:
```
H  e  l  l  0  
0  1  2  3  4
```

A piece of larger text is known as a **substring** \- for example, “Hello” is a substring of “Hello World” (so is “el” \- substrings don’t have to be words). The text must be a single, contiguous piece, though \- “eo” is **not** a substring of “Hello”. For extracting a multi-character substring, you can use the method `substring(int startIndex, int endIndex)`. It’s important to note that endIndex is **exclusive** (it’s all the characters up to but not including the character at endIndex). So “Hello”.substring(0,2) would return “He” \- double-check the labelled version above to verify that this result makes sense.

**Searching Strings**

A common problem when parsing structured text is finding a particular character or substring in a larger String \- for example, if you wanted to write a program that extracted email addresses from text messages (to, say, offer to add someone’s email to their saved contact info if they texted you their email), you might want to start by looking through the text for an “@” symbol.

To search one String for another, smaller, String, use the `int indexOf(String toFind)` method \- this method will return the position of the start of the smaller String in the larger String (specifically, the first such index \- “Hello”.indexOf(“l”) will return 2), or **\-1 as a sentinel value** if the smaller String isn’t found. This method is often combined with substring to figure out what index to pass to substring.  

If you want to find not just the first instance of the smaller String, but also subsequent instances, you’ll repeatedly call indexOf, but with a second parameter: 

`int indexOf(String toFind, int startingIndex)`

lets you specify where to start looking (by default, indexOf starts looking at the beginning of a String). If you ask indexOf to “start looking” at the next character after the first index of toFind, it will find the second instance of toFind. 

As an example:

```
String example = "First, Second, Third";  
int indexComma = example.indexOf(","); // returns the comma after "First"

// returns the comma after "Second"  
int secondComma = example.indexOf(",", indexComma + 1); 
```

## Combining Methods For Complex Programs

Problem: Personalize a greeting \- take some greeting text "Hello World" or "Hi Person" and replace the second word with your name (so for me, I'd change these to "Hello Katherine" or "Hi Katherine).

If you feel like this is ramping up the difficulty of problem solving, you're not wrong \- dealing with Strings (or eventually, any abstract data representation in code) involves adding another mental layer of abstraction to your programs. The best way to handle this is to stick with pseudo code as long as possible while describing your solution to the problem. For these sorts of problems, the trick is figuring out **how to break down the problem** in the first place \- once you solve that, the code writes itself!

Some tricks to help break down the problem:

- Imagine someone has hired you as a filing clerk of some sort and told you that your job is whatever the program problem is. Mentally walk through how you would actually do the task, and write down those steps.  
- Imagine you have an energetic 5 year old who wants to help you do your work, but who can't really handle complicated instructions just yet. How would you talk them through the problem? **Note:** if your answer involves "I would draw it out", grab a piece of paper and do that\! That can be an excellent way to identify how to break down the problem. Professional programmers typically have whiteboards by their desks for this exact reason.  
- Identify the parts of the problem that are **fixed** (ie, what is always true), and what parts are **general** (what parts can change in a way that your program needs to handle any version). A common first step for a program is to tease apart the fixed aspects from the general aspects.  
- Analyze the problem description; words like 'then' or 'and' usually indicate multiple steps, 'repeatedly' or 'until' indicate a loop, 'if' or 'otherwise' will involve an if/else statement.

Take a moment to try to break down the above problem into two separate steps \- note that neither of those steps will be ready to turn into code just yet. Try to use **only** two steps \- don't get too specific too quickly\!

**Spoilers\!**

Hopefully, you came up with something along the lines of "identify the greeting" and "replace the rest with your name" as the two steps (everyone will have their own way of phrasing these). If you went straight to "create a variable", that can get you into trouble as programs get more complicated \- it's easy to get lost in the details if you immediately jump into writing specific lines of code. **Note:** as you get more comfortable with programming, you'll naturally start breaking problems down this way in your head, and you won't need to make the whole process quite as explicit.

Keep in mind that breaking a problem down is a multi-step process: each step can feel like you aren't making much progress towards a solution, but as they say, the journey of 1,000 miles starts with a single step (and then a for loop).

Let's see how this might look in pseudo-code:

```
// Start with some initial text  
// Update it with your name, and give this result back to whoever asked
```

Anytime you find yourself "starting with something", there's a good chance that you want to create a method that takes in the "something" as a **parameter**:

```
// Start with some initial text 
public String updateGreeting(String initial) {  
   // Update initial with your name, and give this result back to whoever asked 
}
```

Here, we're using a method to be clear about what we want to start with (the parameters) and what we want to end up with (the return value).

```
public String updateGreeting(String initial) {  
    // separate out the "greeting part of the string"  
    // replace the rest of the string with our name  
}
```

Now we've got the two steps, but we're not exactly done \- how to do those things?

Your turn: How can you tell what part of the text is the greeting, and what part ("the second word") should be updated?

**Spoilers!**

Just considering the example inputs, the "second word" is the part of the initial String that comes after the first space (this is a situation where picturing a confused toddler and having to explain what a "word" is can be helpful for identifying the program steps).

So now we have:

```  
public String updateGreeting(String initial) {  
    // separate out the "greeting part of the string"  
       // separate out the part of the String before the first space

    // replace the rest of the string with our name  
      // remove the part of the String after the first space  
      // add on our name instead  
}
```

Breaking the problem down should feel a bit like you're just restating the same thing with more words \- that's exactly what breaking the problem down is\!

Next: how to find the first space in a String?

**Spoilers\!**

It's a good idea to have a reference sheet of common classes and methods that you can refer back to while breaking down a problem \- if you come across a step that lines up with one of those methods, you don't need to break things down any further. Instead, you'll call the method \- if you aren't sure exactly how you'll do that yet, you can put the method name in the pseudo code and come back to it. In this case, we're looking for something in a String, and the method to search a String is indexOf()

```
public String updateGreeting(String initial) {  
    // separate out the "greeting part of the string"  
       // separate out the part of the String before the first space  
         // use indexOf to find the first space  
         // separate out the part of the String from the start to that index

    // replace the rest of the string with our name  
      // remove the part of the String after the first space  
      // add on our name instead  
}
```

Next: how to get just part of a String?

**Spoilers\!**

Here, we want to use the substring method, and now we can start converting the pseudo-code to code:

```
public String updateGreeting(String initial) {  
    // separate out the "greeting part of the string"  
       // separate out the part of the String before the first space  
         // use indexOf to find the first space  
         // separate out the part of the String from the start to that index  
           // use substring to do this

    // replace the rest of the string with our name  
      // remove the part of the String after the first space  
      // add on our name instead  
}
```

becomes

```
public String updateGreeting(String initial) {  
    // separate out the "greeting part of the string"  
       // separate out the part of the String before the first space  
         // use indexOf to find the first space  
         int spaceIndex = initial.indexOf(" ");
		 
         // separate out the part of the String from the start up that index  
           // use substring to do this  
           String greeting = initial.substring(0, spaceIndex);

    // replace the rest of the string with our name  
      // remove the part of the String after the first space  
      // add on our name instead  
}
```

Now we're getting into the details \- this is when you want to start asking 'do I include the space in the greeting or not?', or 'wait, is substring inclusive or exclusive?'. Usually, you'll end up double-checking your notes (or in Eclipse, the javadoc for a method). Here, let's say we do want the space as part of the greeting, and since substring is 'everything from \<first index\> up to but not including \<second index\>', we'll need to adjust that second parameter:

```
public String updateGreeting(String initial) {  
    // separate out the "greeting part of the string", plus the space  
    int spaceIndex = initial.indexOf(" ");  
    String greeting = initial.substring(0, spaceIndex + 1);

    // replace the rest of the string with our name  
      // remove the part of the String after the first space  
      // add on our name instead  
}
```

Great\! Now on to part 2, replacing the rest of the String. The good news is we've already actually done the first part \- substring effectively removed the rest of the String. To add on a new name, we'll use concatenation \- this could use a string literal, a new parameter, or a named variable:

```
public String updateGreeting(String initial) {  
    // separate out the "greeting part of the string", plus the space  
    int spaceIndex = initial.indexOf(" ");  
    String greeting = initial.substring(0, spaceIndex + 1);

    // replace the rest of the string with our name  
    String updated = greeting + "Katherine";  
}
```

or, for an even more general version,

```
public String updateGreeting(String initial, String newName) {  
    // separate out the "greeting part of the string", plus the space  
    int spaceIndex = initial.indexOf(" ");  
    String greeting = initial.substring(0, spaceIndex + 1);

    // replace the rest of the string with our name  
    String updated = greeting + newName;  
}
```

Now there's one last step\! Eclipse will always remind you of this, but make sure to double-check for quizzes that you've **returned** any results that you created:

```
public String updateGreeting(String initial, String newName) {  
    // separate out the "greeting part of the string", plus the space  
    int spaceIndex = initial.indexOf(" ");  
    String greeting = initial.substring(0, spaceIndex + 1);

    // replace the rest of the string with our name  
    String updated = greeting + newName;
	
    // now we're done, give this solution back to whoever called the method  
    return updated;  
}
```
