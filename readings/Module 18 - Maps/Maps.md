# Maps

## Introduction

We’ve seen one way to store “many” of a particular data type already - an array (or an ArrayList) will handle that nicely. However, there are a number of more specialized ways to store many objects, which make solving certain programming problems much easier. One example is a **map** - in Java, we’ll be using the specific class HashMap, but the concept is fairly universal. Maps are also sometimes referred to as **dictionaries** or **lookup tables**.

## What is a Map

We’ve covered the idea of a mapping already - a way to **transform** one value into another. For example, to simulate flipping a coin, you might randomly generate a 1 or 0, and then map that to either "Heads" or "Tails" as an output. A map is a way to **programmatically store many mappings**; you can also think of it as a way to **look up a value** corresponding to an initial key - in the same way that a key will (usually) correspond to a single lock that it opens, a key in a map "unlocks" a single specific value (note: while "look up", "transform" and "map" are all commonly used terms to describe a map, "unlock" is not commonly used - it can be helpful as a way to visualize the concept, but not as a way to describe your code to someone else).

As you might imagine, writing down an entire mapping is only useful if you'll be looking up values multiple times. As a result, maps often show up as instance variables or when parsing information from a file, so that they can be used many times in different parts of a program or across multiple runs of a program.

A classic example of a map is storing phone numbers in your phone - the "key" is the name you associate with the number. Later, you can look up the phone number for a specific person by selecting their name from a list of contacts.

## Syntax

Creating a HashMap is similar to creating an ArrayList, except there are two types that are specified using the generic <> syntax - the first is the key, the second is the value. When you look things up in the map, you'll provide a key and get a value back - for example, if you were storing a mapping of randomly chosen integers to Color objects, the types for the HashMap would be Integer and Color:

`HashMap<Integer, Color> colorLookup = new HashMap<Integer, Color>();`

To add values to the map, you'll use a method called `put`, and to get values from the map, you'll use a method called `get`:

```
colorLookup.put(0, Color.RED);
Color result = colorLookup.get(0); // returns Color.RED
```

If the parameter for `get` doesn't correspond to a value in the map, `get` will return null as a sentinel value.

## Iterating

Much like an ArrayList, HashMap has a method called size() to determine how many key/value pairs it contains. Unlike ArrayList, though, there's no clear ordering for the elements - getting the 'first' key doesn't have a clear meaning. Originally, in order to consider each element in the map, you would have to use a method called `iterator()` that returns a new type, Iterator, with 2 useful methods: `hasNext()` and `next()`. You'd then create a `while` loop that continues to call `next` until `hasNext` returns false. Fortunately, Java since added a shorter version of this code, but the shorter version still **compiles to the iterator version** - if you step through the code in detail, you'll find your program making calls to hasNext() and next(). 

The shorthand version is commonly used with the keys in a HashMap, which are available via the `keySet()` method, and nicely lines up with the pseudo-code for this:

```
// for each key in the map
for (Integer key : colorLookup.keySet()) {
   // look up the corresponding value
   Color value = colorLookup.get(key);
}
```

## When to Use a Map

Much like an ArrayList, a HashMap is useful when you're storing "many" of something. You can often recognize that a map is a better solution than a list, though, by considering how you'll access the individual items. If you usually want one item at a time, based on matching some criteria, that's a good use case for a map - on the other hand, if you usually want to consider all the items in order (or you're looking for some element based on its order), that's a better fit for an ArrayList.

For example, copying all the colors in the top row of Binky's world to the bottom row is a good use for an ArrayList - the order is important, and the program will want to consider each square in order. On the other hand, your phone contacts are better modelled as a map: you usually use contacts to look up the phone number for a specific name, and it's rare that you would care about the order that you created the contacts in.

If your pseudocode includes things like "find" or "look for", that's a good sign you want to use a map - "find the student with this id", "look for the phone number that corresponds to this name", etc.

