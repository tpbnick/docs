# Java Classes

## Introduction to Classes
All programs require one or more classes that act as a model for the world.  

For example, a program to track student test scores might have `Student`, `Course`, and `Grade` classes.  Our real-world concerns, students and their grades, are inside the program as classes.  

We represent each student as an *instance*, or *object*, of the `Student` class.  This is *object-oriented programming (OOP)* because programs are built around objects and their interactions.  An object contains a state and behavior.  

**Classes are a blueprint for objects**.  Blueprints detail the general structure.  For example, all students have an ID, all courses can enroll a student, etc.  

An instance is the thing itself.  *This* student has an ID of `42`, *this* course enrolled *that* student, etc.  

Let's review with another example, a savings account at a bank.  

What should a savings account know?  

- The balance of money available.  

What should a savings account do?  

- Deposit money.  

- Withdraw money.  

Imagine that two people have accounts that are instances of the `SavingsAccount` class.  They share behavior (the ability to deposit/withdraw) but have an individual state (their balances), and even with the same balance these accounts are separate entities.  

Let's put that same concept into a store class:

```java linenums="1"
public class Store {
  // instance fields
  String productType;
  int inventoryCount;
  double inventoryPrice;
  
  // constructor method
  public Store(String product, int count, double price) {
    productType = product;
    inventoryCount = count;
    inventoryPrice = price;
  }
  
  // main method
  public static void main(String[] args) {
    Store lemonadeStand = new Store("lemonade", 42, .99);
    Store cookieShop = new Store("cookies", 12, 3.75);
    
    System.out.println("Our first shop sells " + lemonadeStand.productType + " at " + lemonadeStand.inventoryPrice + " per unit.");
    
    System.out.println("Our second shop has " + cookieShop.inventoryCount + " units remaining.");
  }
}
```
Running the above code should give the following output:
```
Our first shop sells lemonade at 0.99 per unit.
Our second shop has 12 units remaining.
```
## Class Syntax 
The fundamental concept of object-oriented programming is the class.  A *class* is the set of instructions that describe how an instance can behave and what information it contains.  Java has pre-defined classes such as `#!java System`, which we have used previously to log text to our screen, but we also need to write our own classes for the custom needs of a program.  

Here is a definition of a Java class:  

```java linenums="1"
public class Car {
// scope of Car class starts after curly brace
 
  public static void main(String[] args) {
    // scope of main() starts after curly brace
 
    // program tasks
 
  }
  // scope of main() ends after curly brace
 
}
// scope of Car class ends after curly brace
```
This example defines a `#!java class` named `Car`.  `#!java public` is an *access level modifier* that allows **other** classes to interact with this class.  For now, all classes will be `#!java public`.  

This class has a `#!java main()` method, which lists the tasks performed by the program.  `#!java main()` runs when we execute the compiled **Car.class** file.  

## Constructors 
In order to create an object (an instance of a class), we need a constructor method.  The constructor is defined within the class.  

Let's take a look at the `Car` class with a constructor.  The constructor, `#!java Car()`, shares the same name as the class:

```java linenums="1"
public class Car {
  // Constructor method
  public Car() {
    // instructions for creating a Car instance
  }  
 
  public static void main(String[] args) {
    // body of main method
  }
}
```
To create an *instance*, we need to *call* or *invoke* the constructor within `#!java main()`.  The following example assigns a `Car` instance to the variable `ferrari`:

```java linenums="1"
public class Car {
 
  public Car() {
    // instructions for creating a Car instance
  }
 
  public static void main(String[] args) {
    // Invoke the constructor
    Car ferrari = new Car(); 
  }
}
```