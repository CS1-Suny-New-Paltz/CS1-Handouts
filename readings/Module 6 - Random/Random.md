# Random Number Generation

## Introduction

Many programming problems require that the program behave **differently** each time it runs \- for example, a poker playing game would get quite boring if it dealt you the same cards each time it ran. In order to do this, a program needs a source of **randomness**. There are two types of randomness in programming \- pseudorandom numbers, which look random to the casual observer, and cryptographically secure random numbers, which still look random even when closely examined by the intelligence arm of large countries. For this class, we're fine with pseudorandom numbers.

## The Random class

Creating pseudorandom numbers is done by creating a complicated mathematical sequence, where the elements of the sequence appear to be effectively random. One of the advantages of many modern programming languages (Java, Python, Javascript, C++, etc) is the ability to leverage code that other folks have already written to solve common problems, which is what we'll be doing here \- Java comes with a built in random number generator that already handles all the math involved. This class is called **Random**, and you can create your very own random number generator in much the same way you can create your own Robot. Instead of 

`Robot binky = new Robot();`

you can write

`Random rng = new Random();`

and now you have a random number generator named 'rng'. You'll notice that to create that code, we're applying the syntax template for creating a new object, using `Random` as the type, and `rng` as the name - as the semester goes on, you'll start using new classes that we haven't covered specifically. It's a good idea to try to recognize the **patterns** for how to create an object now, so that you'll be able to apply them on your own in a few weeks.

## Useful Methods

Just as Binky comes with useful skills like turnRight and isClear, any object of type Random also has a number of useful methods. We'll focus on one specifically:

`int nextInt(int upperBound)`

This method will return a randomly chosen integer between 0 (inclusive) and upperBound (exclusive). Conveniently, that also means upperBound is the number of unique possible values that could be returned. For example:

```
Random rng = new Random();  
int firstNum = rng.nextInt(3);
```

might end up with firstNum having any of 3 possible values: 0, 1, or 2\. 

Treating the parameter to nextInt as "number of unique values" makes it easier to use after you've written out your pseudo-code. If you had

`// Roll a 6 sided die and keep track of the result`

as your pseudo code, you would need a way to randomly generate 1 of 6 possible values. That means you could use

```
// Roll a 6 sided die and keep track of the result  
Random rng = new Random();  
int dieRoll = rng.nextInt(6);
```

as the translated-to-Java code.

## Using the Random Number

Generally, the choices you want to randomly choose between aren't integers starting at 0\. Often, they aren't integers at all \- choosing a restaurant at random from a list, picking a random card from a deck, or turning in a random direction are all examples of random choices you might encounter in a programming problem. After generating a random number, you'll need to **translate,** or **map**, that number to one of the values that you're actually interested in. For example, if you wanted to simulate tossing a coin, you might write down the following **mapping**:

0 \= Heads  
1 \= Tails

It's a good idea to include that mapping in your pseudocode\!

Once you have the pseudocode, you'll create the Java code that will **map** the random value to the corresponding choice. For example:

```
// Flip a 2 sided coin  
// 0 = Heads  
// 1 = Tails

Random rng = new Random();  
int coinFlip = rng.nextInt(2);

if (coinFlip == 0) {  
  System.out.println("Heads");  
}  
if (coinFlip == 1) {  
  System.out.println("Tails");  
}
```

**Caution**

Random has a **lot** of methods, including methods that are **overloaded** \- these are methods that have the same name, but different numbers of parameters. In particular, there's a version of nextInt() with no parameters, and a version with two parameters \- both of these work slightly differently than the version we're using. Be careful not to accidentally call one of those methods \- nextInt with no parameters will return a value from (roughly) \-2 billion to \+2 billion, which is rarely useful. The version with two parameters is less surprising \- it lets you specify some value other than 0 as the inclusive lower bound \- but more prone to off-by-one errors, because it loses the mnemonic of specifying the number of unique options that you want for your random choices.

## Other Ways To Generate Randomness

As with most concepts in programming, there are many ways to generate random numbers in Java; aside from the Random class, the static method Math.random() and the class SecureRandom are both ways to do so. For assignments for this class, you'll need to use Random specifically, since the goal of the assignments is to practice the content we're covering in class. The specific pros and cons of other ways of generating randomness are outside the scope of this course, but if you'd like to learn more about them, feel free to come to office hours to chat!
