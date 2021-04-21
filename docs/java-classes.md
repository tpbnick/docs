# Object Oriented Java

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
### Class Syntax 
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
### Constructors 
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
### Instance Fields
In our first example, we ended with printing an instance of `Store`, which looked something like `Store@6bc7c054`.  The first part, `Store`, refers to the class, and the second part, `@6bc7c054` refers to the instance's location in the computer's memory.  

We don't care about memory location, but our instances have no other characteristics!  When an object is created, the constructor sets the initial state of the obkect.  The *state* is made up of associated data that represents the characteristics of an object.  

We'll add data to an object by introducing *instance variables*, or *instance fields*.  

We want `Car` instances of different colors, so we declare a `#!java String color` instance field.  Often times, instance variables are described as a "has-a" relationship with the object.  For example, a `Car` "has-a" `color`.  Another way to think of that is that instance variables are nouns and adjectives associated with an object.  What qualities other than `color` might a car *have*?  

```java linenums="1"
public class Car {
  /*
  declare fields inside the class
  by specifying the type and name
  */
  String color;
 
  public Car() {
    /* 
    instance fields available in
    scope of constructor method
    */
  }
 
  public static void main(String[] args) {
    // body of main method
  }
}
```
The declaration is **within** the class and the instance variable will be available for assignment inside the constructor.  

Fields are a type of state each instance will possess.  One instance may have `"red"` as its `color`, another `"blue"`, etc.  It's the job of the constructor to give these instance fields initial value. 
### Contructor Parameters
To create objects with dynamic, individual states, we'll use a combination of the constructor method and instance fields.  

In order to assign a value to an instance variable, we need to alter our constructor method to include parameters so that it can access the data we want to assign to an instance.  We've already seen a parameter in the `#!java main()` method: `#!java String[] args`, but this is the first time we're using the parameter value within a method body.  

The `Car` constructor now has a parameter: `#!java String carColor:`:

```java linenums="1"
public class Car {
  String color;
  //constructor method with a parameter
  public Car(String carColor) {
    // parameter value assigned to the field
    color = carColor;
  }
  public static void main(String[] args){
    // program tasks
  }
}
```
When a `#!java String` value gets passed into `Car`, it is assigned to the parameter `carColor`.  Then, inside the constructor, `carColor` will be assigned as the value to the instance variable `color`.  

Our method also has a *signature* which defines the name and parameters of the method.  In the above example, the signature is `#!java Car(String carColor)`.
### Assigning Values to Instance Fields
Now that the constructor has a parameter, we must pass values into the method call.  These values are referred to as *arguments*; once they are passed in, they will be used to give the instance fields intial value.  

Here we create an instance, `ferrari`, in the `#!java main()` method with `"red"` as its `color` field:
```java linenums="1"
public class Car {
  String color;

  public Car(String carColor){
    // assign parameter value to instance field
    color = carColor;
  }

  public static void main(String[] args) {
    // parameter value supplied when calling the constructor
    Car ferrari = new Car("red");
  }
}
```
We pass the String value `"red"` to our constructor method call: `#!java new Car("red");`.  

The type of value given to the invocation **must match** the type declared by the parameter.  

Inside the constructor, the parameter `carColor` refers to the value passed in during the invocation `"red"`.  This value is assigned to the instance field `color`.  

`color` has already been declared, so we don't specify the type during assignment.  

The object, `ferrari`, holds the state of `color` as an instance field referencing the value `"red"`.  

We access the value of this field with the *dot operator* (`.`):
```java linenums="1"
/*
accessing a field:
objectName.fieldName
*/

ferrari.color;
// "red"
```
### Using Multiple Fields
Objects are not limited to a single instance field.  We can declare as many fields as are necessary for the requirements of our program.  

Let's change `Car` instances so they have multiple fields.  

We'll add a `#!java boolean isRunning`, that indicates if the car engine is on and an `#!java int velocity`, that indicates the speed at which the car is travelling.

```java linenums="1"
public class Car {
  String color;
  boolean isRunning;
  int velocity;

  public Car(String carColor, boolean carRunning, int milesPerHour) {
    color = carColor;
    isRunning = carRunning;
    velocity = milesPerHour;
  }

  public static void main(String[] args) {
    Car ferrari = new Car("red", true, 27);
    Car renault = new Car("blue", false, 70);

    System.out.println(renault.isRunning);
    // will print false
    System.out.println(ferrari.velocity);
    // will print 27
  }
}
```
The constructor now has multiple parameters to receive values for the new fields.  We still specify the type as well as the name for each parameter.  

**Ordering matters!**  We must pass values into the constructor invocation in the same order that they're listed in the parameters.  

```java linenums="1"
// values match types, no error
Car honda = new Car("green", false, 0);

// values do not match types, error!
Car junker = new Car(true, 42, "brown");
```
### Classes Review
Java is an object-orriented programming language where every program has at least one class.  Programs are often built from many classes and objects, which are the instances of a class.  

Classes define the state and behavior of their instances.  Behavior comes from methods defined in the class.  State comes from instance fields declared inside the class.  

Classes are modeled on the real-world things we want to represent in our program.  Later we will explore how a program can be made from multiple classes.  For now, our programs are a single class.  

```java linenums="1"
public class Dog {
  // instance field
  String breed;
  //constructor method
  public Dog(String dogBreed) {
    /*
    value of parameter dogBreed assigned to instance field breed
    */
    breed = dogBreed;
  }
  public static void main(String[] args) {
    /*
    create instance:
    use 'new' operator and invoke constructor
    */
    Dog dani = new Dog("border collie");
    /*
    fields are accessed using:
    the instance name, '.' operator, and the field name
    */
    dani.breed;
    // "border collie"
  }
}
```

## Introduction to Methods
A **method** is a block of code which only runs when it is called.  You can pass data, known as *parameters* into a method.  Methods are used to perform certain actions, and they are also known as **functions**.  

Methods are repeatable, modular blocks of code, used to accomplish specific tasks.  We have the ability to define our own methods that will take input, do something with it, and return the kind of output we want.  

*Method decomposition* is a way we can use methods to break fown a large problem into smaller, more manageable problems.  

Methods are very reusable.  Imagine we wrote a sandwich-making program that used 20 lines of code to make a single sandwich.  Our program would become very long very quickly if we were making multiple sandwiches.  By creating a `#!java makeSandwich()` method, we can make a sandwich anytime simply by calling it.  

We will be using the following code to build a method later on:
```java linenums="1"
public class SavingsAccount {
  
  int balance;
  
  public SavingsAccount(int initialBalance){
    balance = initialBalance;
  }
  
  public static void main(String[] args){
    SavingsAccount savings = new SavingsAccount(2000);
    
    //Check balance:
    System.out.println("Hello!");
    System.out.println("Your balance is "+savings.balance);
    
    //Withdrawing:
    int afterWithdraw = savings.balance - 300;
    savings.balance = afterWithdraw;
    System.out.println("You just withdrew "+300);
    
    //Check balance:
    System.out.println("Hello!");
    System.out.println("Your balance is "+savings.balance);
    
    //Deposit:
    int afterDeposit = savings.balance + 600;
    savings.balance = afterDeposit;
    System.out.println("You just deposited "+600);
    
    //Check balance:
    System.out.println("Hello!");
    System.out.println("Your balance is "+savings.balance);
    
    //Deposit:
    int afterDeposit2 = savings.balance + 600;
    savings.balance = afterDeposit2;
    System.out.println("You just deposited "+600);
    
    //Check balance:
    System.out.println("Hello!");
    System.out.println("Your balance is "+savings.balance);
    
  }       
}
```
### Defining Methods
If we were to define a `#!java checkBalance()` method for the Savings Account example above, it would look like the following:
```java linenums="1"
public void checkBalance(){
  System.out.println("Hello!");
  System.out.println("Your balance is " + balance);
}
```
The first line, `#!java public void checkBalance()`, is the method declaration.  It gives the program some information about the method:

- `#!java public` means that other classes can access this method.  

- The `#!java void` keyword means that there is no specific output from the method.  We will see methods that are not `#!java void` later in these notes, but for now, all of our methods will be `#!java void`.  

- `#!java checkBalance()` is the name of the method.  

Every method has its own unique *method signature* which is comprised of the method's name and its parameter type.  In this example, the method signature `#!java checkBalance()`.  

The two print statements are inside the *body* of the method, which is defined by the curly braces: `{` and `}`.  

Anything we can do in our `#!java main()` method, we can do in other methods!  All of the java tools we have learned, like the math and comparison operators, can be used to make interesting and useful methods.  

### Calling Methods
When we add a non-static method to a class, it becomes available to use on an object of that class.  In order to have our methods get executed, we must *call* the method on the object we created.  

Let's add a non-static `#!java startEngine()` method to our `Car` class from [earlier notes](#using-multiple-fields).  Inside the `#!java main()` method, we'll call `#!java startEngine()` on the `myFastCar` object:

```java linenums="1"
class Car {
 
  String color;
 
  public Car(String carColor) {
    color = carColor;
  }
 
  public void startEngine() {
    System.out.println("Starting the car!");
    System.out.println("Vroom!");
  }
 
  public static void main(String[] args){
    Car myFastCar = new Car("red");
    // Call a method on an object 
    myFastCar.startEngine();
    System.out.println("That was one fast car!");
  }
}
```
Let's take a closer look at the method call:
```java
myFastCar.startEngine();
```
First, we reference our object `myFastCar`.  Then, we use the *dot operator* (`.`) to call the method `#!java startEngine()`.  Noter that we must include parentheses `()` after our method name in order to call it.  

If we run the above program, we get the following output:
```
Starting the car!
Vroom!
That was one fast car!
```
Code generally runs in a top-down order where code execution starts at the top of a program and ends at the bottom; however, methods are ignored by the compiler unless they are being called.  

When a method is called, the compiler executes every statement contained within the method.  Once all method instructions are executed, the top-down order of execution continues.  This is why `Starting the car!` and `Vroom!` are outputted before `That was one fast car!`.  

