# Creating Classes

## Introduction

Much like methods are used to separate out individual pieces of a problem, objects can also be used to separate out methods and related data. Generally, objects serve as the "nouns" of a program, while methods are the "verbs". Creating a new object type involves creating a **class**, which has its own syntax and concepts. As a useful example for this reading, we're going to create a Student class.

## Overall Syntax

We've actually been creating classes all semester \- the declaration towards the top of the .java file that looks like

```
public class Student {  
}
```

is a **class declaration**. So far, though, these classes haven't stored any data, and have just had static methods. Creating a class to use as an object type will have an additional piece of syntax

## Instance Variables

An **instance variable** is similar to the variables we've seen so far (often called **local variables** in contrast to instance variables) \- it has a type, a name, and can store data. The difference is the **scope** \- while a local variable only exists within a method, an instance variable can be referenced by **any non-static method in the class**. An instance variable is sometimes called an **attribute** or a **field** for an object \- it's a piece of data that's associated with a **specific instance** of the class. 

For our Student class, we'll have two instance variables \- a name, and number of enrolled classes. The syntax for **declaring** the instance variables is exactly the same as for local variables, except that it happens outside of any methods (typically, at the very top of the class declaration).

```
public class Student {  
     String name;  
     int numClasses;  
}
```

## Constructors

Initializing instance variables is a bit trickier than initializing local variables, because they often depend on the program that's using the class \- there's no way of knowing, from just within the Student class, what any particular student's name should be, or how many classes they're taking. Instead of initializing instance variables when they are **declared**, instance variables are generally initialized in a separate piece of code called the **constructor**. This is a method-like piece of syntax that creates ("constructs") a new object. Calling a constructor is something we've seen many times \- `new Robot("some.world")` or `new Random()` are both examples of using a constructor to **create a new instance** of a class.  
A constructor looks similar to a method, but with a few differences:

- a constructor is never static  
- a constructor has no explicit return value  
- a constructor has the same name as the class, including starting with a capital letter

For the Robot class, the constructor looks like:

```
public Robot(String worldFile) {  
}
```

For our Student class, we'll use:

```
public Student(String name) {  
}
```

Choosing parameters for the constructor is similar to choosing parameters for a method \- you should include all the information that you'll need to **initialize the instance variables.** In our case, we'll say that to start with, Students aren't enrolled in any classes, so the only information we need someone who wants to create a Student to provide is a name.

## The "this" Pointer

The most confusingly-named piece of syntax in Java is a keyword called **this**, and it's a reference to the **instance** of the class that is currently "active". Any instance variable or non-static method must always be called on a particular object (ex: `binky.moveForward()` is calling the moveForward method on Binky), and `this` is a way to refer back to that called-on object. It's also a solution for a new problem that can happen with instance variables: **variable shadowing**. Normally, you can't create two variables with the same name. However, you can have a parameter with the same name as an instance variable, and not only *can* you do that, but it's very common to do that with constructors.

In the same way that you can differentiate between two people with the same name by adding context, you can use the `this` keyword to refer to an instance variable. For example, if there were another Katherine teaching at New Paltz, you might clarify who you meant by saying "The CS1 professor, Katherine". In the above constructor, we have a parameter called `name` and an instance variable also called `name`, so we'll use `this` to clarify which one we mean. By default, the parameter/variable is the one that's meant, and the instance variable requires a `this.` in front of it (notice the '.', that's the "pointer" part of the `this` pointer)

```
public Student(String name) {  
  this.name = name;  
}
```
For the number of classes, since there's no parameter also called numClasses, the `this` pointer is optional:

```
public Student(String name) {  
  this.name = name;  
  numClasses = 0;  
}
```

**Checklist for Constructors**

Once you've written a constructor, you can double-check that it's correct by making sure that **every instance variable** has an initial value set in the constructor. That value can either be a default starting value, or based on a parameter that's passed in.

## Access Modifiers

Now that we have multiple classes, it's worth covering **access modifiers**. Up until now, everything has been `public` \- this means it's accessible to any class. `public` can be applied to methods, instance variables, or classes themselves. There are several other modifiers in Java, but the next-most-common one, and the only other one relevant for this class, is `private`. Anything marked `private` can only be accessed from within that class \- a private method can only be called by another method in that class, and a private instance variable can only be accessed by methods in that class.

If you're curious, there is one other access modifier, and a default level of access if no modifier is used at all. The additional modifier is `protected`, which is the same as private except that subclasses (which you'll see in CS2) are allowed to access the data. The default level of access is what's called package-protected - any classes in the same **package** can access the method or instance variable. Ironically, it's extremely unusual to use the default level of access, so much so that it's a best practice to add a **comment** saying you're using it deliberately and didn't just forget the modifier (ex: `/* package-protected */ void someMethod();`). 

It's generally a good idea to make instance variables `private`, so that the class can control how and in what ways the data in them can be changed. 

The updated version of the Student class is now:

```
public class Student {  
     // Instance variable declaration  
     private String name;  
     private int numClasses;

     // Constructor - initialize all instance variables  
     public Student(String name) {  
       this.name = name;  
       numClasses = 0;  
     }  
}
```

## Methods

Methods on classes are similar to the methods we've already written, except that they are generally **not static.** Aside from the syntax of skipping the static keyword, what that means is that these methods can use the **instance variables** from the object. A non-static method must always be called on a **specific instance** of the class, which determines the values of the instance variable.  
Put in the context of the Student class, you can write code to ask a specific student a question, or to do something. For example, you might want to ask a student what their name is \- a method that just returns the value of an instance variable is a common type of method called a **getter** (it "gets" a value). Similarly, methods that just update the value of an instance variable are called **setters** (they "set" a value).

Suppose we had a main method that used the Student class:

```
public static void main(String[] args) {  
  Student ta = new Student("Jared");  
}
```

The `new` keyword calls the **constructor**, creating a `ta` local variable that points to a Student object with the name "Jared".

If we wanted to be able to ask a Student what their name is, we want to be able to write:

`String studentName = ta.getName();`

which means we'd need a method with the signature:

`public String getName()`

in the Student class. Since we're writing the Student class, we can be the change we want to see in the code:

```
public class Student {  
     // Instance variable declaration  
     private String name;  
     private int numClasses;

     // Constructor - initialize all instance variables  
     public Student(String name) {  
       this.name = name;  
       numClasses = 0;  
     }

     // Return this student's name  
     public String getName() {  
        return name;  
     }  
}
```

Here, the `getName` method refers to the instance variable `name` \- this is why a non-static method must be called on a specific instance of the class, so that the code knows what value to use for the `name` instance variable (as it turns out, not all students are named "Jared").

Now suppose we want a Student to be able to enroll in a class \- just as with getName(), it's often easier to picture this from the perspective of code that's using the Student class, and then add the implementation:

```
public static void main(String[] args) {  
  Student ta = new Student("Jared");  
  ta.enrollInClass();  
}
```

This method has no parameters or return value, so we'll add

```
public void enrollInClass() {  
}
```

to the Student class. This method should update the number of classes the Student is taking, which is stored in the numClasses instance variable:

```
public void enrollInClass() {  
   numClasses = numClasses + 1;  
}
```

We could also add a getter for numClasses:

```
public int getNumClasses() {  
   return numClasses;  
}
```

Keep in mind that every Student has their own name and number of classes \- if we wrote the following program:

```
public static void main(String[] args) {  
  Student spring25Ta = new Student("Jared");  
  Student fall24Ta = new Student("Sanket");  
  spring25Ta .enrollInClass();  
  System.out.println(spring25Ta.getName() + " is enrolled in " + spring25Ta.getNumClasses() \+ " class(es)");  
    System.out.println(fall24Ta.getName() + " is enrolled in " + fall24Ta.getNumClasses() \+ " class(es)");  
}
```

it would print:

```
Jared is enrolled in 1 class(es)  
Sanket is enrolled in 0 class(es);
```

## Object Methods: toString

There are a few methods that every class has in Java, even if they aren't explicitly written out. These methods have a **default implementation** that technically works but is rarely useful. Often, you'll want to add your own implementation of these methods which will **override** the default implementation.

The first such method controls how String concatenation works with this class \- recall that a String can be combined with any object type using the \+ operator. Under the hood, this is calling a method on the non-String object called toString:

`public String toString()`

the default implementation is the name of the class plus a semi-unique code for the object, which is better than nothing, but not by much.

For our Student class, we can change the method to use the student's name instead:

```
public String toString() {  
  return name;  
}
```

Now we can update the main method from earlier to replace the getName() call with String concatenation on the Student object itself, since that will use our now-customized toString method:

```
public static void main(String[] args) {  
  Student spring25Ta = new Student("Jared");  
  Student fall24Ta = new Student("Sanket");  
  spring25Ta .enrollInClass();  
  System.out.println(spring25Ta + " is enrolled in " + spring25Ta.getNumClasses() + " class(es)");**  
  System.out.println(fall24Ta + " is enrolled in " + fall24Ta.getNumClasses() + " class(es)");**  
}
```

The toString is also how variables are displayed in the Variables view in an IDE - you've likely seen this in action with Binky.

## Optional Spellcheck for Overridden Methods

As with most aspects of programming, `toString` is extremely fussy about what it's named. A method called `tostring` will **not** override the default implementation, nor will `toString(boolean shouldCapitalize)`. If you want the compiler to double-check your formatting, you can add 

`@Override` 

just before the method \- this tells the compiler that you're trying to override some default behavior, and the compiler will create an error if that isn't what's happening. This isn't required, but it's a good idea, so our new Student toString() will look like:

```
@Override  
public String toString() {  
  return name;  
}
```
