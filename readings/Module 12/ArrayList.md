# ArrayList

## Introduction

We've already seen how to repeatedly perform actions in code \- for loops and while loops both let a program specify "do something repeatedly" in a compact format. There's a similar concept for storing data \- if you want to create multiple copies of some object, you can use an **ArrayList**.

## ArrayList class

ArrayList is part of the Java Collections package; we'll see some other useful classes from that package later in the semester. At a high level, it supports a few basic operations: adding items to a list, removing items from a list, getting a specific item from a list, updating a specific item in the list, and checking how many items are in the list. However, before we get into the Javadoc for the class, there's a new piece of syntax involved \- if you were wondering "wait, what's an 'item'?" for the previous sentence, you've already identified the problem this syntax will solve

## Generics: Background Info

There are two ways to structure a class like an ArrayList to work for a variety of types. Long ago, in the before times (aka for versions of Java before 1.5), ArrayList accomplished this by saying it stored "Object" type data, but this had some problems. Specifically, any code using an ArrayList had to **cast** data to the correct type in order to use any items in the list. This frequently led to bugs where a programmer would accidentally use the wrong type (which will crash the program with a ClassCastException). For example:

```
ArrayList oldeList = new ArrayList();  
oldeList.add("Numbers to add");  
oldeList.add(1);  
oldeList.add(2);

int sum = 0;  
for (int i = 0; i < oldeList.size(); i++) {  
  int numberToAdd = (int)oldeList.get(i); // this is a cast  
  sum = sum + numberToAdd;  
}
```

Note: We haven't covered the add, size, or get methods in detail yet, but you can take a pretty good guess at what they might do in the context of a list.

That code will crash\! The problem is that a descriptive heading got added to the list along with the numbers. Starting in Java 1.5, a new piece of syntax was added to fix this problem: Generics. 

## Generic Syntax

To indicate a generic type, there's a new symbol: the angle brackets, \< \>, that are part of the **type information** for a variable, field, or parameter The syntax template for this is

```
__________________________<________________>      _____________________;  
(Name of "generic" class)  (Specific type)        (variable/field name)
```

Right now, the only generic class we've seen is ArrayList, and the type that can be specified is 'what type of items can be added to this list'. For example, an ArrayList that stored Strings would be:

`ArrayList<String> listOfStrings;`

while an ArrayList of Colors would be:

`ArrayList<Color> listOfColors;`

## Javadoc for ArrayList

The exact method signatures for an ArrayList **depend on the generic type**, which is often represented as a single capital letter (for ArrayList, it's E for 'element type'). If you were to look at ArrayList.java, you'd see methods that look like:

`public void add(E elementToAdd)`

For an ArrayList\<String\>, that method would become

`public void add(String elementToAdd)`

For an ArrayList\<Color\>, on the other hand, the method would be

`public void add(Color elementToAdd)`

The method names, what they do, and the number of parameters are the same regardless of the generic type, but the return types and parameter types can depend on the generic type. The good news is that, since variables can't change their type once they're declared, any **specific** ArrayList will be consistent in how to use its methods.

The ArrayList methods that we'll use for this class are:

Constructor: 

`ArrayList<E>()` \- for example, `new ArrayList<String>()`

Methods:

`public int size();` \- similar to `length()` for String, this returns the number of items (or 'elements') in the list

`public void add(E elementToAdd)` \- adds an item of the list type to the list. For example, an ArrayList\<String\> would have `public void add(String elementToAdd)`

`public E get(int index)` \- this returns the item at the specific position in the list (starting at 0)\. So to get the first item in a list, you'd use get(0); to get the second, you'd use get(1).

## Using ArrayList

While generics and ArrayList can look a little confusing if you start examining them in detail, from a high level perspective, they're very intuitive. Use an ArrayList whenever you want to have "many" of "something" \- the "something" is the generic type. For example, if you wanted your SquirrelSimulator to have many Squirrels, you could create:

`ArrayList<Squirrel> squirrels = new ArrayList<Squirrel>();`

and then add as many Squirrels to the list as you want for your particular simulator (you could even have someone using the program select how many squirrels to add).

**When to Use an ArrayList**

Common problems that you can use an ArrayList to solve:

- Have some large, but variable, number of objects of the same type; this might be Squirrels in a simulator, Students in a course registration program, or “guessed letters” in a Hangman program (these can also be modelled as a String, as we saw; an ArrayList is a more general version of the same concept)  
- Need to “save” data for later, rather than processing it all at once. Reversing an output (lines in a file, calculated Fibonnaci numbers, etc) is a common situation here.  
- As an instance variable, represent the concept of one noun having “many” of some other noun. For example, if you had a PettingZoo class and an Animal class, the PettingZoo might have an instance variable: `ArrayList<Animal> animalsInZoo;` This comes up frequently as programs get more complex \- Classrooms have many Students, Banks have many Accounts, Buildings have many Classrooms, etc. Using an ArrayList lets you break down problems into more intuitive relationships between object types.

## Iterating over an ArrayList: Shorthand

For in-class examples class, we’ll stick to the classic way to iterate over an ArrayList: for each index from the beginning to the end, consider the element at that index:

```
ArrayList<String> list = new ArrayList<String>();  
for (int i = 0; i < list.size(); i++) {  
   String element = list.get(i);  
  // do something with element  
}
```

There’s also a shorter version that’s often used that you may run across. It’s roughly equivalent to the loop above (when we start looking at Sets, we’ll see the precise equivalent), and you’re free to use either one in your code:

```
ArrayList<String> list = new ArrayList<String>();  
for (String element : list) {  
   // do something with element  
}
```
