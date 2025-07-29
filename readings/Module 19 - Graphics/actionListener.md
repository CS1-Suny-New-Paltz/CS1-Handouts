# Action Listeners

## Introduction

Most programs that have graphics have some way for users to interact with the graphics - clicking on an icon, entering text into a field, dragging items around the screen, etc. Interacting with a program involves **peripherals**, which is a general term for something external to your computer that can interact with the world - a mouse, keyboard, touch screen, or webcam are all examples of peripherals. Getting that interaction into your program involves **action listeners**, which are a bit different from code that we've seen so far

## Action Listener Syntax

Action listeners are implemented in different ways in different programming languages - in Java, they use something called "anonymous inner classes" (or, frequently, "lambdas"). You'll see more details on exactly what that is and how it works in CS2, but for now, we're going to focus on what an action listener does (rather than how it does it). An action listener provides a **hook** into your code that allows the **peripherals** for your device to alert you to what a user has done. 

The action listener specifies two things:

- What **event** it's listening for (a mouse click, for example)
- What **code should run** (ie, what action to take) when the event happens

**Syntax**

We'll be using **lambda syntax** to specify the action listener - it looks a bit unusual, but minimizes the amount of extra syntax surrounding your code:

```
____________________________.addActionListener(e -> {
(name of component variable)
      _________________________________;
      (what code should run when the event takes place; can be multiple lines of code)
});
```

`e` in this case is actually a parameter, although you'll notice no type is explicitly specified - if you look at the javadoc for addActionListener, you can find where the type of e is defined (it's a parameter of type ActionEvent). Lambdas don't require restating that type definition - this is unusual for Java, but very convenient in cases where you often won't use the parameter at all. For the components we'll be using, we won't ever use the parameter `e`.
