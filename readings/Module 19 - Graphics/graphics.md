# Graphics Frameworks

## Introduction

Computer graphics are an entire field by themselves, with a large number of frameworks and approaches. We're going to be using a very simplified framework to get a sense for the basics. The code we'll be using is based off something called Java Swing, but we're going to focus on the more universal aspects that any graphics framework will include. Swing itself is neither particularly modern nor user-friendly, but it does lend itself nicely to being simplified.

## Components

The first part of creating graphics for a program is to decide on the pieces, or **components**, of the visual and interactive parts of the program. This might be something as simple as "a red circle", or as complex as "an auto-scrolling image gallery". Each component should be able to function independently of other components - a red circle doesn't need to know if there's also an image gallery on the screen. Much like instance variables in classes allow you to nest one class within another, it's possible to nest smaller components within larger components to build more complex visuals.

We'll be using a couple of components for this course, some of which are built in to Swing, and some of which are simplified wrappers around Swing components. As a general rule, if a component name starts with a capital 'J', it's built into **J**ava Swing; if it starts with 'CS1', it's a wrapper for this class. 

JButton
JTextField
CS1Image


## Layout

Once you have several components, the next part of creating graphics is deciding how the components will **be laid out on the screen**. For example, if you have a red circle and an image gallery, does the circle go on the left of the gallery, or above/below/to the right? Perhaps you want to add an animation so that one component moves across another! The **layout** for the graphics determines where each component goes in relation to all the others.

We'll be using an extremely simplified version where you specify the location of a component on the screen in (x,y) coordinates in terms of pixels. This is fairly easy to work with for learning purposes, but not actually a good idea for any real world program: since everyone uses a different computer with different screen sizes and resolutions, specifying locations in terms of absolute pixels tends to work poorly for programs that need to run on phones, tables, overhead projectors, laptops, and desktop monitors. More commonly, a layout manager will allow you to specify fractional positions and relative sizes of components - if you take any additional graphics courses, you'll get to see these types of layouts.

To specify the layout of a component, we'll use a method that's defined on all the components:

setBounds

## Action Listeners

Most programs that have graphics have some way for users to interact with the graphics - clicking on an icon, entering text into a field, dragging items around the screen, etc. Adding this logic to your program involves a new programming concept: an **action listener**. Action listeners are implemented in different ways in different programming languages - in Java, they use something called "anonymous inner classes" (or, frequently, "lambdas"). You'll see more details on exactly what that is and how it works in CS2, but for now, we're going to focus on what an action listener does (rather than how it does it). An action listener provides a **hook** into your code that allows the **peripherals** for your device to alert you to what a user has done. A **peripheral** is a general term for something external to your computer that can interact with the world - a mouse, keyboard, touch screen, or webcam are all examples of peripherals. Common action listeners are set up to get information about when a user types on a keyboard, or moves or clicks the mouse.

The action listener specifies two things:

- What **event** it's listening for (a mouse click, for example)
- What **code should run** (ie, what action to take) when the event happens

**Syntax**

## Example Program





