# Access, Encapsulation, & Scope
## The `public` Keyword
The `public` and `private` keywords are very important within Java.  These keywords are defining what parts of our code have *access* to other parts of our code.  

We can define the access of many different parts of our code including instance variables, methods, constructors, and even a class itself.  If we choose to declare these as `public` this means that any part of our code can interact with them - even if that code is in a different class!  

The way we declare something to be `public` is to use the `public` keyword in the declaration statement.  In the code block belowm, we have a public class, constructor, instance variables, and method.  Notice the five different uses of `public`:  
```java linenums="1"
public class Dog{
    public String name;
    public int age;

    public Dog(String input_name, int input_age){
        name = input_name;
        age = input_age;
    }

    public void speak(){
        System.out.println("Arf! Arf! My name is " + name + " and I am a good dog!");
    }
}
```
Since everything about a `Dog` is public, any other class can access anything about a `Dog`.  For example, let's say there was a `DogSchool` class.  Any method of the `DogSchool` class could make a new `Dog` using the `public` `Dog` constructor, directly access that `Dog`'s instance variables, and directly use that `Dog`'s methods:  
```java linenums="1"
public class DogSchool{
    public void makeADog(){
        Dog cujo = new Dog("Cujo", 7);
        System.out.println(cujo.age);
        cujo.speak();
    }
}
```
Notice that the `DogSchool` class and the `#!java makeADog()` method are also public.  This means that if some other class created a `DogSchool`, they would have access to these methods as well!  We have public methods calling public methods!  

One final thing to note is that for the purposes of this lesson, we'll almost always make our classes and constructors `#!java public`.  While you can set them to `#!java private`, it's fairly uncommon to do so.  Instead, we'll focus on why you might make your instance variables and methods `#!java private`.

## The `private` Keyword and Encapsulation  
When a Class' instance variable or method is marked as `#!java private`, that means that you can only access those structures from elsewhere inside that same class.  Let's look back at our `DogSchool` example:  
```java linenums="1"
public class DogSchool{
 
  public void makeADog(){
    Dog cujo = new Dog("Cujo", 7);
    System.out.println(cujo.age);
    cujo.speak();
  }
}
```  
`makeADog` is trying to directly access `Dog`'s `.age` variable.  It's also trying to use the `#!java .speak()` method.  If those are marked as `#!java private` in the `Dog` class, the `DogSchool` class won't be able to do that.  Other methods within the `Dog` class would be able to us `#!java .age` or `#!java .speak()` (for example, we could use `#!java cujo.age` within the `Dog` class), but other classes won't have access.  

## Accessor and Mutator Methods
When writing classes, we often make all of our instance variables `private`.  However, we still might want some other classes to have access to them, we just don't want those classes to know the *exact* variable name.  To give other classes access to a private instance variable, we would write an *accessor method* (sometimes also known as a "getter" method).  
```java linenums="1"
public class Dog{
    private String name;

    // other methods and constructors

    public String getName(){
        return name;
    }
}
```
Even though the instance variable `name` is `#!java private`, other classes could call the `#!java public` method `#!java getName()` which returns the value of that instance variable.  Accessor methods will always be `#!java public`, and will have a return type of the instance variable they're accessing.  

Similarly, `#!java private` instance variables often have mutator methods (sometimes known as "setters").  These methods allow other classes to reset the value stored in `private` instance variables.  
```java linenums="1"
public class Dog{
    private String name;

    // Other methods and constructors

    public void setName(String newName){
        name = newName;
    }

    public static void main(String[] args){
        Dog myDog = new Dog("Cujo");
        myDog.setName("Lassie");
    }
}
```
Mutator methods, or "setters", often are `void` methods - they don't return anything, they just reset the value of an existing variable.  Similarly, they often have one parameter that is the same type as the variable they're trying to change.  

## Scope: Local Variables
In addition to access modifiers like `#!java public` and `#!java private`, the *scope* of the variable also determines what parts of your code can access that variable.  

The *scope* of a variable is determined by where the variable is declared.  For example, because instance variables are declared inside a class but outside any methods or constructors, all methods and constructors are within the scope of that variable.  For example, in the code block below, constructors and methods of the `Dog` class are using the `Dog` instance variables like `name` and `age`:  
```java linenums="1"
class Dog{
    public String name;
    public int age;
    public int weight;

    public Dog(){
        name = "Dani";
        age = 5;
        weight = 30;
    }

    public void speak(){
        System.out.println("My name is " + name);
    }
}
```
However, if we have a variable declared inside a method, that variable can only be used inside that method.  The same is true for parameters.  The scope of those parameters is only the method they're associated with.  If you try to use a parameter outside the function it's defined in, you'll get an error.  These variables are often called local variables.  Note that we don't use `public` or `private` when declaring local variables.  

This idea of scope extends to conditionals and loops as well.  If you declare a variable inside the body of a conditional or in a loop, that variable can only be used inside that structure.  This also includes the variable you're using as your looping value.  For example, consider the following block of code:
```java linenums="1"
for(int i=0; i < 10; i++){
    // you can use i here
}
// i is out of scope here
```
You can only use `i` between the curly braces of the for loop.  In general, whenever you see curly braces, be aware of the scope.  If a variable is defined inside curly braces, and you try to use that variable outside those curly braces, you will likely see an error!  

## Scope: The `this` Keyword
Often times when creating classes, programmers will create local variables with the same name as instance variables.  For example, consider the code block below:
```java linenums="1"
public class Dog{
  public String name;
 
  public Dog(String inputName){
    name = inputName;
  }
 
  public void speakNewName(String name){
    System.out.println("Hello, my new name is" + name);
  }
 
  public static void main(String[] args){
    Dog myDog = new Dog("Winston");
    myDog.speakNewName("Darla"); // Prints "Darla" - "Winston" ignored
 
  }
}
```
We have an instance variable named `name`, but the method `speakNewName` has a parameter named `name`. So when the method tries to print `name`, which variable will be printed? By default, Java refers to the local variable `name`. So in this case, the value passed to the parameter will be printed and not the instance variable.  

If we wanted to access the instance variable and not the local variable, we could use the `#!java this` keyword.
```java linenums="1"
public class Dog{
  public String name;
 
  public Dog(String inputName){
    name = inputName;
  }
 
  public void speakNewName(String name){
    System.out.println("Hello, my new name is" + this.name);
  }
 
  public static void main(String[] args){
    Dog a = new Dog("Fido");
    Dog b = new Dog("Odie");
 
    a.speakNewName("Winston");
    // "Fido", the instance variable of Dog a is printed. "Winston" is ignored
 
    b.speakNewName("Darla");
    // "Odie", the instance variable of Dog b is printed. "Darla" is ignored.
  }
}
```
The `this` keyword is a reference to the current object. We used `#!java this.name` in our `#!java speakNewName()` method. This caused the method to print out the value stored in the instance variable `name` of whatever `Dog` Object called `#!java speakNewName()`. (Note that in this somewhat contrived example, the local variable name used as a parameter gets completely ignored).

Oftentimes, you’ll see constructors have parameters with the same name as the instance variable. For example, you might see something like:
```java linenums="1"
public Dog(String name){
    this.name = name;
}
```
You can read this as “set `#!java this` `Dog`'s instance variable `name` equal to the variable passed into the constructor”. While this naming is a common convention, it can also be confusing. There’s nothing wrong with naming your parameters something else to be more clear. Sometimes you will see something like:
```java linenums="1"
public Dog(String inputName){
  this.name = inputName;
}
```
This is now a little clearer — we’re setting the `Dog`'s instance variable name equal to the `name` we give the constructor.

Finally, mutator methods also usually follow this pattern:
```java linenums="1"
public void setName(String name){
  this.name = name;
}
```
We reset the instance variable to the value passed into the parameter.

Throughout the rest of this lesson, we’ll use `#!java this.` when referring to an instance variable. This isn't always explicitly necessary — if there's no local variable with the same name, Java will know to use the instance variable with that name. That being said, it is a good habit to use `#!java this.` when working with your instance variables to avoid potential confusion.  

## Using `this` With Methods
We've seen how the `this` works with variables, but we can also use the `#!java this` with methods.  

Recall how we've been calling methods up to this point:
```java linenums="1"
public static void main(String][] args){
    Dog myDog = new Dog("Odie");
    myDog.speak();
}
```
Here we're creating an instance of a `Dog` and using that `Dog` to call the `#!java speak()` method.  However, when defining methods, we can also use the `this` keyword to call other methods.  Consider the code block below:
```java linenums="1"
public class Computer{
  public int brightness;
  public int volume;
 
  public void setBrightness(int inputBrightness){
    this.brightness = inputBrightness;
  }
 
  public void setVolume(int inputVolume){
    this.volume = inputvolume;
  }
 
  public void resetSettings(){
    this.setBrightness(0);
    this.setVolume(0);
  }
}
```
Take a look at `#!java resetSettings()` method in particular.  This method calls other methods from the class.  But it needs an object to call those methods! Rather than create a new object (like we did with the `Dog` named `myDog` earlier), we use `#!java this` as the object. What this means is that the object that calls `#!java resetSettings()` will be used to call `#!java setBrightness(0)` and `#!java setVolume(0)`.
```java linenums="1"
public static void main(String[] args){
  Computer myComputer = new Computer();
  myComputer.resetSettings();
}
```
In this example, calling `myComputer.resetSettings()` is as if we called `myComputer.setBrightness(0)` and `myComputer.setVolume(0)`. `#!java this` serves as a placeholder for whatever object was used to call the original method.

## Other Private Methods
Now that we've seen how methods can call other methods using `this.`, let's look at a situation where you micht want to use `#!java private` methods.  Oftentimes, `#!java private` methods are helper methods - that is to say that they're methods that other, bigger methods use.  

For example, for our `CheckingAccount` example, we might want a public method like `#!java getAccountInformation()` that prints information like the name of the account owner, the amount of money in the account, and the amount of interest the account will make in a month.  That way, another class, like a `Bank`, could call that public method to get all of that information quickly.  

Well, in order to get that information, we might want to break that larger method into several helper methods.  For example, inside `#!java getAccountInformation()`, we might want to call a function called `#!java calculateNextMonthInterest()`.  That helper method should probably be `#!java private`.  There's no need for a `Bank` to call these smaller helper methods - instead, a `Bank` can call one `#!java public` method, and rely on that method to do all of the complicated work by calling smaller `#!java rivate` methods.  

## Access, Encapsualtion, & Scope Review

- The `public` and `private` keywords are used to define what parts of code have access to other classes, methods, constructors, and instance variables.  

- Encapsulation is a technique used to keep implementation details hidden from other classes. Its aim is to create small bundles of logic.  

- The `this` keyword can be used to designate the difference between instance variables and local variables.  

- Local variables can only be used within the scope that they were defined in.  

- The `this` keyword can be used to call methods when writing classes.  

## Static Methods Refresher
In these notes, we're going to dive into how to create classes with our own static methods and static variables.  To begin, let's brush up on static methods.  

Static methods are methods that belong to an entire class, not a specific object of the class.  Static methods are clled using the class name and the `.` operator.  We've seen a couple static methods already!  

```java linenums="1"
double randomNumber = math.random();
// stores a random decimal between 0 and 1 in randomNumber

double number = String.valueOf("2.5");
// transforms the String "2.5" into a double
```
In the first example. `#!java random()` is a static method that belongs to the `Math` class.  We didn't need to create a `Math` object (like `#!java Math myMathObject = new Math()`) in order to use that method.  We could just call it using the class name.  

Similarly, `#!java valueOf()` is a static method of the `#!java String` class.  Given a `#!java String` as an input, this method will turn that `#!java String` into a `#!java double`.  Again, we don't need to create a `#!java String` object in order to call this method - we use the class itself to call it.  

Finally, notice that our `#!java main()` methods have been `#!java static` this whole time.  When Java runs your program, it calls that main method of your class - `#!java YourClassName.main()`.  

## Static Variables
We'll begin writing our own static methods soon, but before we do, let's take a look at static variables.  Much like static methods, you can think of *static variables* as belonging to the class itself instead of belonging to a particular object of the class. 

Just like with static methods, we can access static variables by using the name of the class and the `.` operator.  Finally, we declare static variables by using the `#!java static` keyword during declaration.  This keyword usually comes after the variable's access modifier (`#!java public` or `#!java private`).  

When we put this all together, we might end up with a class that looks something like this:
```java linenums="1"
public class Dog{

    // static variables
    public static String genus = "Canis";

    // instance variables
    public int age;
    public String name;

    public Dog(int inputAge, String inputName){
        this.age = inputAge;
        this.name = inputName;
    }
}
```
Since all dogs share the same genus, we could use a static variable to store that information for the entire class.  However, we want each dog to have it's own unique `name` and `age`, so those aren't `#!java static`.  We could now access this static variable in a `#!java main()` function, like so:
```java linenums="1"
public class Dog{
    // variables, constructors, and methods defined here

    public static void main(String[] args){
        System.out.println(Dog.genus); // prints Canis
    }
}
```
Unlike static methods, you can still access static variables from a specific object of the class.  However, no matter what object you use to access the variable, the value will always be the same.  You can think of it as all objects of the class sharing the same variable.  
```java linenums="1"
public static void main(String[] args){
    Dog snoopy = new Dog(3, "Snoopy");
    Dog ringo = new Dog(5, "Ringo");

    System.out.println(Dog.genus); // prints Canis
    System.out.println(snoopy.genus); // prints Canis
    System.out.println(ringo.genus); // prints Canis
}
```
## Modifying Static Variables
Now that we've created a couple of static variables, let's start to edit them.  The good news is that editing static variables is similar to editing any other variable.  Whether you're writing code in a constructor, a non-static method, or a static method, you have access to static variables.  

Often times, you'll see static variables used to keep track of information about all objects of a class.  For example, our variable `numATMs` is keep track of the total number of `ATM`s in the system.  Therefore, every time an `ATM` is created (using the constructor), we should increase that variable by `1`.  If we could somehow destroy the `ATM`, the method that destroys it should decrease `numATMs` static variable by `1`.  

Similarly, we have a variable names `totalMoney`.  This variable is keeping track of all money across all ATMs.  Whenever we remove money from an ATM using the non-static `withdrawMoney()` method, we should modify the `money` instance variable for that particular ATM as well as the `totalMoney` variable.  In doing so, all ATMs will know how much money is in the system.  

## Writing Your Own Static Methods
Now that we have seen how static variables work, let's look into how to write our own static methods.  

Let's get the syntax out of the way first - just like with variables, to create a static method, use the `#!java static` keyword in the method's definition.  Just like with variables, this keyword usually comes after `#!java public` or `#!java private`.  
```java linenums="1"
public static void myFirstStaticMethod(){
    // code goes here
}
```
Often times, you'll see static methods that are accessors or mutators for static variables.  
```java linenums="1"
public static int getMyStaticVariable(){
    return myStaticVariable;
}

public static void setMyStaticVariable(int newValue){
    myStaticVariable = newValue;
}
```
One important rule to note is that static methods can't interact with non-static instance variables.  

To wrap our mind's around this, let's consider why we use `#!java this` when working with non-static instance variables.  Let's say we have a `#!java Dog` class with a non-static instance variable named `age`.  If we have a line of code like `#!java this.age = 5;`, that means we're setting the `age` of a specific `Dog` equal to `5`. However, if `age` were static, that would mean that the variable belongs to the entire class, not just a specific object.  

The `#!java this` keyword can't be used by a static method since static methods are associated with an entire class, not a specific object of that class.  If you try to mix `#!java this` with a static method, you'll see the error message `non-static variable this cannot be referenced from a static context`.

## Static Variables Review  

- Static methods and variables are associated with the class as a whole, not objects of the class.  

- Static methods and variables are declared as static by using the `#!java static` keyword upon declaration.  

- Static methods cannot interact with non-static instance variables. This is due to static methods not having a `#!java this` reference.  

- Both static methods and non-static methods can interact with static variables.