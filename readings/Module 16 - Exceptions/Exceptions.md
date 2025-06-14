# Exceptions

## Introduction

When something “goes wrong” in a program, that often shows up as the program **crashing**. You’ve likely seen this already - lots of red text on the console with a **stack trace** that lists a lot of files, methods, and line numbers. The actual mechanism for how a Java program crashes is by **throwing an exception** - believe it or not, this is a considerable improvement over how earlier programming languages crashed (a “segfault” would often just print out a hex representation of program memory).

Sometimes, an exception can be handled (or **caught**) in a reasonable way by your code; when that happens, you can add logic to your program to prevent an exception from crashing your program.

## Syntax

In order to catch an exception, you’ll specify three things:

- What code you want to try to run, but which might throw an exception
- What type of exception can you catch
- What to do if such an exception gets thrown

The syntax for this looks like:

```
try {
    // lines of code to run go here
} catch(__________________    _______________________________________) {
       (type of exception)  (variable name for the specific exception)

  // lines of code to handle exception go here

}
```

For example:

```
try {
   int userSelection = Integer.parseInt(stringInput);
} catch (NumberFormatExcepion e) {
   System.out.println(“Enter a number, “ + stringInput + “ is invalid.”);
}
```


## When to Use try/catch

Catching an exception only makes sense if there's something your program can do to **recover** from whatever invalid state it has gotten into. As a result, you generally only catch exceptions that are caused by something **external to your program** - a user entering bad data, a wifi connection cutting out, or some other similarly temporary situation. To see what exceptions a method might throw, and under what circumstances, you can check the javadoc for that method - this will let you decide if a situation is recoverable. For example, a common cause of an exception being thrown is calling Integer.parseInt with a String that isn't a number:

`Integer.parseInt("Hello world"); // this will throw a NumberFormatException`

If the String came from a user who's interacting with the program, this is a recoverable situation - your program can tell the user that their input was invalid, and ask them to try again. On the other hand, if the String came from a data file (for example, trying to create Binky with a malformed .world file), that's not usually recoverable. 

## Catch and Rethrow

One other situation where you can catch an Exception specifically relates to how exceptions were added to Java. While checked exceptions (such as IOException) are now recognized as a mistake, for backwards compatibility reasons they're still around. As an alternative to adding 'throws IOException' to every method signature involved in file reading or writing, you can use a catch block to **convert** an Exception from a checked exception to a RuntimeException, using

`throw new RuntimeException(e); // replace 'e' with the variable name for the exception`

This is how some file reading and writing classes manage to avoid the IOException situation - while we haven't covered any of those in this class, you may have run across PrintWriter or Scanner in outside resources (sadly, there's no one perfect file io class in Java yet - both Scanner and PrintWriter have their own interesting issues, as does the Files class). If you look at `Scanner.readInput`, you'll see a `catch(IOException e)` block (fun bonus activity: see if you can figure out what happens to that exception, and why that makes Scanner difficult to use correctly in exceptional situations), which is why it doesn't have to declare throws IOException on many methods.

## How to Use try/catch

Once you've decided to add a try/catch block to your code, now you have to decide what code should go where. Generally, you want to put all code that's **closely related** or **dependent** on the possible-exception-throwing code in the try block - this will ensure that code only runs if an exception is not thrown. Then, in the catch block, you can **fix up** any variables or data that need to be in a consistent state after the entire try/catch block runs - you can think of this as similar to a post-condition for a method.

For example, if you wanted to prompt a user for a lucky number, you might decide to use a default of '13' if what the user entered didn't work:

```
String userInput = input.readLine();
int luckyNumber;
try {
  luckyNumber = Integer.parseInt(userInput);
} catch (NumberFormatException e) {
  luckyNumber = 13;
}
```

Pay careful attention to **scopes** while you do this; variables declared in the try block aren’t valid in the catch block.

As a more interesting example, suppose you were writing a program that would take in a number from a user, and then print out the integer that is twice the number(for example, if a user inputs 4, the program would print 8). Should the doubling logic live in the `try` block or not? Going back to our guidelines, since the doubled value **depends on** the user input, it should be in the try block:

```
try {
   int userSelection = Integer.parseInt(stringInput);
   int doubledValue = userSelection * 2;
   System.out.println(doubledValue + " is twice the value you entered");
} catch (NumberFormatExcepion e) {
   System.out.println(“Enter a number, “ + stringInput + “ is invalid.”);
}
```

Now suppose you wanted to modify this program to let the user choose if they wanted to double their input, or halve it. You give users an old-timey menu (select '1' for doubling, or '2' for halving), and a **default option** (let's say '1' by default):

```
BufferedReader userInput = new BufferedReader(new InputStreamReader(System.in));
System.out.println("Enter '1' to double, '2' to halve (default: 1)");

// get the user action selection
int selection = Integer.parseInt(userInput.readLine());
double multiplier;
if (selection == 2) {
  multiplier = 0.5;
} else {
  multiplier = 2;
}

// handle the user selection
System.out.println("Enter your chosen number");
try {
   int userSelection = Integer.parseInt(userInput.readLine());
   int doubledValue = userSelection * multiplier;
   System.out.println(doubledValue + " is twice the value you entered");
} catch (NumberFormatExcepion e) {
   System.out.println(“Enter a number, “ + stringInput + “ is invalid.”);
}
```

Quick method decomposition practice: what part of that code snippet could be factored out into its own method?

To add a try/catch to the user action selection logic, we need to decide what parts of the later code should be included in the try block. At first glance, you might be tempted to include all of it - after all, each line in the program depends on what came before it. However, because we have a **default** for the user selection, it's possible to **recover** from issues in the first user prompt before reaching the second prompt:

```
BufferedReader userInput = new BufferedReader(new InputStreamReader(System.in));
System.out.println("Enter '1' to double, '2' to halve (default: 1)");

// get the user action selection
double multiplier;
try {
  int selection = Integer.parseInt(userInput.readLine());
  if (selection == 2) {
    multiplier = 0.5;
  } else {
    multiplier = 2;
  }
} catch (NumberFormatException e) {
  System.out.println("Invalid menu option, using the default");
  multiplier = 2;
}

// factor out the doubling/halving logic into a method
multiplyNumber(multiplier);
```

You could also write this code with just `selection` being part of the `try`, and have it set to a default value of '1' in the catch block (this would move the `if/else` outside the try block) - either approach is fine. 


## When **Not** to Use try/catch

Exceptions are for exceptional cases - following the code logic is a bit trickier, and they’re a bit slower program-wise than normal code flow. If there’s a straightforward way to use an if/else statement or sentinel return value instead, prefer to do that rather than throw an exception.

The correlary to that is that **catching exceptions is also unusual** - you should only catch an exception if you can guarantee that your code can do something reasonable and helpful with it. While it can seem tempting to wrap an entire main method in a try/catch block for NullPointerExceptions (now you can guarantee that your program won’t crash due to an NPE!), it’s very unlikely that your catch block can do anything other than immediately end the program (effectively crashing). Worse, it’s very easy to end up removing important debugging information by mistake.

