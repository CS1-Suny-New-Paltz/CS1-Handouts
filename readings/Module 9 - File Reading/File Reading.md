# Reading From Files

## Introduction

Data stored on a computer falls into two categories: in memory (RAM) storage, and on disk (hard drive) storage. Data that’s in memory only lasts as long as a program is running \- to store data more permanently, it needs to be **written to disk**. Reading data from disk is how programs can load saved data when you start them.

## What is a File

At its core, a file is a collection of bits \- it’s arbitrary data stored somewhere on the hard disk (also known as **non-volatile storage**). In order for a file to be useful, those bits need to be arranged in a specific **format**, but what that format is can vary depending on the data. Some common file formats show up as file extensions: for example, catPic.gif will use a GIF format, funnyMeme.jpg will use a JPEG format, info.txt will use a text format. It’s important to note that file extensions are not part of the format itself \- they’re a hint to the computer about the format type, but they aren’t a guarantee (you can change file extensions to whatever you like). Most commonly, programs will combine a new, unique file extension with an existing, well-supported format \- you’ve seen this already with files that end in .java or .world (both of which use a text format). 

## Reading a File

Reading a file comes in two parts: moving the underlying bits from the hard drive into computer memory where a program can interact with them (this is also often called **loading** a file), and **parsing** the bits into something useful. For very common file formats, those two steps can be combined using existing **libraries** of code. For now, we’re going to focus on reading files that use a text format for their data \- text formatting is nice because it’s both human readable (you can open the file in notepad and see what’s actually in there) and can express any data. Other formats are often more **compact** than text formatting (meaning they can store the same amount of information in fewer bits) but that comes at the expense of being more complicated to read.

## File Reading Libraries

In Java, there are a **lot** of different ways to read a file, all of which have their own pros and cons. For this class specifically, we’re going to use a class called **BufferedReader**, which is a nice general-purpose text file reading library \- you can safely use it to read any text file, with no fine-print caveats. Internet resources may suggest other options (such as Scanner) \- this is one of the few times that you’ll be required to solve programming problems specifically with BufferedReader rather than any of the other options.

## BufferedReader Javadoc

If you haven’t read the handout on Javadocs, go check that out first. The link for the full javadoc for BufferedReader is: [BufferedReader Javadoc](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedReader.html)   
We’ll be using a subset of the constructors and methods: specifically, we’ll always use the constructor that takes a Reader, and the method readLine(). For reading from files, the constructor call will always look like:

```
BufferedReader _______________ = new BufferedReader(new FileReader(______________));  
	         (name of variable)				                  (name of file as String)
```

For example:

```
BufferedReader binkyWorldReader = new BufferedReader(new FileReader(“default.world”));
```

The readLine() method has two interesting features that we haven’t seen before: it can **throw an exception** and it has a **sentinel value** as a possible return value.

## Throwing an Exception

We’ve already seen Exceptions \- if Binky runs into a wall, that throws an exception and causes the program to crash. Binky throws what are called **unchecked Exceptions**, which don’t require a program to use any special syntax \- if the exception is thrown, the program will crash, but otherwise it runs normally. Some types of exceptions in Java are known as **checked Exceptions**. These, sadly, are one of those mistakes of the past that we’re still living with today \- they largely introduce extra syntax for no benefit. Newer code written in Java will generally use unchecked Exceptions, but file reading has been around for a long time, so it still has this vestigial syntax. When a method throws a checked exception, any code that calls that method must either **catch** the exception, or declare that it will **re-throw** the exception. For the moment, we’ll just always re-throw \- this involves adding

`throws IOException`
   
or
  
`throws Exception`

to any of the methods involved, just after the parentheses in the method signature. For example:

```
public static void main(String[] args) throws IOException {  
  // code goes here  
}
```

We’ll talk about catching exceptions (checked or unchecked) when we get to error handling.

## Sentinel Values

Normally, the return value for a method can be treated as an “answer to a question”: isClear() returns true or false depending on whether there’s a wall in front of Binky, getSquareColor() returns a Color corresponding to the color of the square Binky is standing on, etc. Sometimes, though, the answer to a question includes a “does not apply” response \- this can be represented as a **sentinel value**. It’s important to note that sentinel values are not part of Java syntax \- they’re strictly part of the semantics of using a method. This makes them tricky, since you as the programmer have to find out about them from the Javadoc and then remember to check them yourself in your code.

`readLine()` in BufferedReader is an example of using a sentinel value. This method will return the next line of text in a file, or, if the end of the file has been reached and there is no next line, it will return a special value that we saw in the context of pointers: `null`. Null is a possible value for any object type; in the context of pointers, we saw that it's the value of a pointer when there is no pointee. Semantically, it's often used to mean “there is no value for this variable”. Checking for `null` is one of the few times that you can safely use \== with an object. 

In the context of `readLine()`, the question being asked is “What String can store the next line of text in the file?”, and the answer is a pointer to a specific String object. But if there is no next line of text, the question is more accurately answered with “does not apply, there is no next line of text in the file” \- here, `null` is chosen as the sentinel value to represent that answer. 

Sentinel values are **fundamentally arbitrary**; this is why they must be documented in the javadoc, because there’s no way to infer them otherwise. Null is a common sentinel value, but it’s not the only one \- the only requirements of a sentinel value are that it not be a possible **actual answer** to the question the method is asking, and that it’s of the correct **type**. For example, if you had a method that counted the number of breadcrumbs on the square in front of the one Binky is on, you might use \-1 as a sentinel value to represent the case where Binky is facing a wall. This is a good situation for a sentinel, since if Binky is facing a wall, there is no “square in front of this one”, and the question doesn’t apply. \-1 is never a valid answer to “how many breadcrumbs are on this square”, so it’s acceptable as a sentinel value, but you could just as easily choose \-2, \-10, or some other value. You couldn’t use 0 as a sentinel value, because that’s a possible valid answer, and you couldn’t use the String “Not valid” either, as that’s not the correct type (if the method returns an int, the sentinel must also be an int).

## Parsing a File

Now that we can read the actual text in the file, what does it mean? That’s a question that’s answered by parsing the file, and requires knowing what **semantic information** is in the file (this is also sometimes called the **file layout** to distinguish it from the **format**, which is often text). This is less complicated than it sounds \- you’ve likely dealt with parsing out structured information many times when reading websites. For example, on the SUNY schedule of classes website, the information is laid out visually in a table, with headers for each column. Based on those headers, you’re able to look at a specific line on the table and know what each piece corresponds to \- that’s how you can tell the ‘Title’ of a course from its ‘Attributes’, even though the actual contents of those two columns can look similar.

Parsing a file follows the same logic \- you and whoever created the file agree on how the data is laid out, so your program can look at specific text and know what that text represents (fun fact: “you” and “whoever created the file” are very often the same person). For example, in a .world file, the first line contains two numbers: a number of rows followed by a single space followed by a number of columns. If a file doesn’t follow that pattern, and you try to have Binky load that world, your program is highly likely to crash.

## Common Problem: Converting a String to an int

One of the downsides of Java being strict with types is that it doesn’t “just do what you mean” when converting types (this turns out to also be one of the upsides, since it never guesses incorrectly). If you have a String literal of “1”, you can’t assign that to an int:

`int value = “1”;`

won’t compile, because the types don't match - the left-hand side is of type `int` and the right-hand side is of type `String`. That’s a problem, since everything that’s being read from a file is a String, and it’s pretty common to want to include numbers in the file layout. Fortunately, Java includes a built in class with a static helper method: `Integer.parseInt(String s)`, which takes in a String parameter and returns an int. You'll notice this method is static, which we haven't seen on a class before! The syntax for calling a static method from another class is a bit different - instead of calling it on a specific variable of the relevant type, you use the `.` syntax on the **class name itself**:

```
______________._______________(_______________________________________);
(Object type)   (method name)   (0 or more comma-separated parameters)
```

What we're saying with this method call is "Hey Integer class, what int is equivalent to this String?". You'll notice that nothing in that question refers to any specific Integer instance; declaring that a method is **static** is roughly equivalent to saying that the question or behavior for the method doesn't depend on a specific object instance. 

The updated version of converting a String to an int is:

`int value = Integer.parseInt(“1”);`

This is also a good example of where you might get an unchecked exception \- if you were to write:

`int value = Integer.parseInt(“This isn’t a number, but it is a String”);`

the code would compile, but it would crash when you tried to run that line with a NumberFormatException. This is similar to passing a String to the Robot constructor that doesn’t actually correspond to a .world file \- it’s a runtime error that the compiler can’t help you with. When we get to validating user input, this will become more important, because your programs will need to handle invalid input; right now, though, you can assume that data is correctly formatted.