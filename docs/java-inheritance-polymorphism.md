# Inheritance & Polymorphism
## Inheritance in Practice
So how do we define a child class so that it inherits from a parent class?  

We use the keyword `#!java extends` like this:
```java linenums="1"
class Shape {
    // shape class members
}

class Triangle extends Shape {
    // additional Triangle class members
}
```
Now `Triangle` has inherited traits from `Shape`, meaning it copied over class members from `Shape`.  When we use inheritance to extend a subclass from a superclass, we create an "is-a" relationship from the subclass to the superclass.  For example, an object of `Triangle` *is* a member of the `Shape` class; however an object of `Shape` is not necessarily an object of `Triangle`.  

Until now, we've only covered working with one class and one file.  However, most Java programs utilize multiple classes, each of which requires its own file.  Only one file needs a `#!java main()` method - this is the file we run.  

Note: the various classes in our Java package - even though they are in different files - will have access to each other, so we can instantiate one class inside another.  

## Inheriting the Constructor
If the class inherits its paren'ts fields and methods, does it also inherit the constructor?  Let's take a look at how the `#!java super()` constructor works!

Let's say `Shape` has a `numSides` field that is set by passing an integer into the constructor.  If we're instantiating a `Triangle`, we would want that number to always be `3`, so we'd want to modify the constructor to automatically assign `numSides` with a value of `3`.  

Can we do that?

As it happens, Java has a trick up its sleeve just for this occasion: using the `#!java super()` method, which acts like the parent constructor inside the class constructor:
```java linenums="1"
class Triangle extends shape{

    Triangle(){
        super(3);
    }

    // additional Triangle class members
}
```
By passing `3` to `#!java super()`, we are making it possible to instantiate a `Triangle` without passing in a value for `numSides`.  

Meanwhile, `#!java super(3)` (behaving as `#!java Shape(3)`) will shoulder the responsibility of setting `numSides` to `3` for our `Triangle` object.  It's like we called `#!java Shape(3)`.  

It is also possible to write a constructor without making a call to any `#!java super()` constructor:
```java linenums="1"
class Triangle extends Shape{

    Triangle(){
        this.numSides = 3;
    }

    // additional Triangle class methods
}
```
In this situation, Java secretly calls the parent class' no-argument constructor (`#!java super()`).  So in this specific example, the `#!java Triangle()` constructor first calls the `#!java Shape()` constructor.  That `#!java Shape()` takes care of whatever business it needs to take care of.  And then after that is complete, we go in and set `#!java this.numSides` to `3`.  

If you're writing a constructor of a child class, and don't explicitly make a call to a constructor to a parent class using `#!java super`, it's important to remember that Java will automatically (and secretly) call `#!java super()` as the first line of your child class constructor.  

## Parent Class Aspect Modifiers
You may recall that Java class members use `#!java private` and `#!java public` access modifiers to determine whether they can be accessed from outside the class.  So does a child class inherit its parent's `#!java private` members?  

Well, no.  But there is another access modifier we can use to keep a parent class member accessible to its child classes and to files in the package it's contained in - and otherwise private: `#!java protected`.  

| Modifier           | Class              | Package            | Child Class        | Global             |
|--------------------|--------------------|--------------------|--------------------|--------------------|
| `#!java public`    | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| `#!java protected` | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :x:                |
| no modifier        | :heavy_check_mark: | :heavy_check_mark: | :x:                | :x:                |
| `#!java private`   | :heavy_check_mark: | :x:                | :x:                | :x:                |  

Here's what `#!java protected` looks like in use:
```java linenums="1"
class Shape{

    protected double perimeter;
}

// any child class of Shape can access perimeter
```
In addition to access modifiers, there's another way to establish how child classes can interact with inherited parent class members: using the `#!java final` keyword.  If we add `#!java final` before a parent class method's access modifier, we disallow any child classes from changing that method.  This is helpful in limiting bugs that might occur from modifying a particular method.  

## Introducing Polymorphism
In Java, if `Orange` is a `Fruit` through inheritance, you can use `Orange` in the same contexts as `Fruit` like this:
```java linenums="1"
String makeJuice(Fruit fruit){

    return "Apple juice and " + fruit.squeeze();

}

// inside main()
Orange orange = new Orange();
System.out.println(juicer.makeJuice(orange));
```
Wait, how does that work?

This is because Java incorporates the object-oriented programming principle of *polymorphism*.  Polymorphism, which derives from Greek meaning "many forms", allows a child class to share the information and behavior of its parent class while also incorporating its own functionality.  

The main advantages of polymorphic programming:

- Simplifying syntax  

- Reducing cognitive overload for devlopers  

These benefits are particularly helpful when we want to develop our own Java packages for other developers to import and use.  

![!Polymorphism](https://cdn.nickplatt.dev/files/Docs/polymorphism.png)

For example, the built-in operator `#!java +` can be used for both `#!java double`s and `#!java int`s.  To the computer, the `#!java +` means something like `#!java addDouble()` for the other, but the creators of Java (and other languages) didn't want to burden us developers with recalling each individual method.  

Note that the reverse situation is not true; you cannot use generic parent class inheritance where a child class instance is required.  So an `Orange` can be used as a `Fruit`, but a `Fruit` cannot be used as an `Orange`.  

## Method Overriding
One common use of polymorphism with Java classes is something we mentioned earlier - *Overriding* parent class methods in a child class.  Like the `#!java +` operator, we can give a single method slightly different meanings for different classes.  This is useful when we want our child method to have the same name as a parent class method but behave a bit differently in some way.  

Let's say we have a `BankAccount` class that allows us to print the current balance.  We want to build a `CheckingAccount` class that inherits the functionality of a `BankAccount` but with a modified `#!java printBalance()` method.  We can do the following:
```java linenums="1"
class BankAccount{
    protected double balance;

    public BankAccount(double balanceIn){
        balance = balanceIn;
    }

    public void printBalance() {
        System.out.println("Your account balance is $" + balance);
    }
}

class CheckingAccount extends BankAccount{
    
    public CheckingAccount(double balance){
        super(balance);
    }

    @Override
    public void printBalance(){
        System.out.println("Your checking account balance is $" + balance);
    }
}
```
Notice that in order to properly override `#!java printBalance()`, in `CheckingAccount` the method has the following in common with the corresponding method `BankAccount`:  

- Method name  

- Return type  

- Number and type of parameters  

You may also have noticed the `#!java @Override` keyword above `#!java printBalance()` in `CheckingAccount`.  This annotation informs the compiler that we want to override a method in the parent class.  If the method doesn't exist in the parent class, we'll get a helpful error when we compile the program.  

## Using a Child Class as its Parent Class
An important facet of polymorphism is the ability to use a child class object where an object of its parent class is expected.  

One way to do this explicitly is to instantiate a child class object as a member of the parent class.  We can instantiate a `CheckingAccount` object as a `BankAccount` object like this:
```java
BankAccount nicksAccount = new CheckingAccount(5000.00);
```
We can use `nicksAccount` as if we were an instance of `BankAccount`, in any situation where a `BankAccount` object is expected.  (This would be true even if `nicksAccount` was instantiated as a `CheckingAccount`, but using the explicit child as parent syntax is most helpful when we want to declare objects in bulk.)

It is imporant to note that the compiler considers `nicksAccount` to be any old `BankAccount`.  But because method overriding is handled at runtime, if we call `#!java printBalance()`, we'll see something `CheckingAccount` specific:
```
Your checking account balance is $5000.00
```
This is because at runtime, `nicksAccount` is recognized as the `CheckingAccount` it is.  So, what if `CheckingAccount` has a method `#!java transferToSavings()` that `BankAccount` does not have?  Can `nicksAccount` still use that method?  

Well, no.  The compiler believes that `nicksAccount` is just a `BankAccount` that doesn't have some fancy child class `#!java transferToSavings()` method, so it would return an error.  

## Child Classes in Arrays and `ArrayList`s
Usually, when we create an array or an `ArrayList`, the list items all need to be the same type.  But polymorphism puts a new spin on what is considered the same type...  

In fact, we can put instances of different classes that share a parent class together in an array or `ArrayList`!  For example, let's say we have a `Monster` parent class with a few child classes: `Vampire`, `Werewolf`, and `Zombie`.  We can set up an array with instances of each:
```java linenums="1"
Monster dracula, wolfman, zombie1;

dracula = new Vampire();
wolfman = new Werewolf();
zombie1 = new Zombie();
 
Monster[] monsters = {dracula, wolfman, zombie1};
```
We can even iterate through the list of items - regardless of subclass - and perform the same action with each item:
```java linenums="1"
for (Monster monster : monsters) {

    monster.attack();
}
```
In the code above, we are able to call `#!java attack()` on each monster in `monsters` despite the fact that, in the for-each loop, `monster` is declared as the parent class type `Monster`.  

## Child Classes in Method Parameters
When we call a method that contains parameters, the arguments we place in our method call must match the parameter type.  Polymorphism gives us a little more flexibility with the arguements we can use.  

If we use a superclass reference as a method parameter, we can call the method using subclass reference arguments!  

For example, imagine the class `ScaryStory`, whose constructor takes in a reference to the `Monster` class:

```java linenums="1"
class ScaryStory {
    Monster monster;
    String setting;

    public ScaryStory(Monster antagonist, String place){
        monster = antagonist;
        setting = place;
    }

    public static void tellStory(){
        System.out.println("Once upon a time, " + monster.name + " was at " + setting + " looking to scare some mortals.");
    }

    public static void main(String[] args) {
        Monster dracula;
        dracula = new Vampire("Dracula");
        ScaryStory countDracula = new ScaryStory(dracula, "Dracula Castle");
        countDracula.tellStory();
    }
}
```
In the `#!java main()` method, we used a reference of the class `Vampire` as our argument even though the constructor requested an object of class `Monster`.  This is allowed because `Vampire` is a subclass of the `Monster` class.  

## Review of Inheritance and Polymorphism

- A Java class can inherit fields and methods from another class.  

- Each Java class requires its own file, but only one class in a Java package needs a `#!java main()` method.  

- Child classes inherit the parent constructor by default, but it’s possible to modify the constructor using `#!java super()` or override it completely.  

- You can use `#!java protected` and `#!java final` to control child class access to parent class members.  

- Java’s OOP principle of polymorphism means you can use a child class object like a member of its parent class, but also give it its own traits.  

- You can override parent class methods in the child class, ideally using the `@Override` keyword.  

- It’s possible to use objects of different classes that share a parent class together in an array or `ArrayList`.  