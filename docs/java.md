# Java Basics

## Quick Links  

* [Java Documentation](https://docs.oracle.com/en/java/)  

* [The Java Tutorials (Oracle)](https://docs.oracle.com/javase/tutorial/index.html)  

* [Java Cheat Sheet (PDF)](https://programmingwithmosh.com/wp-content/uploads/2019/07/Java-Cheat-Sheet.pdf)  

* [Java in a Nutshell - A Desktop Quick Reference (2019) (PDF)](https://nicklyss.com/media/uploads/2021/04/Java-in-a-Nutshell-A-Desktop-Quick-Reference.pdf)

* [The Java Workshop - A practical, no-nonsense guide to Java. (2019) (PDF)](https://nicklyss.com/media/uploads/2021/04/The-Java-Workshop-A-practical-no-nonsense-guide-to-Java.pdf)

* [Java Basics Tutorial](https://www.tutorialspoint.com/java/index.htm)

## Introduction  

Java is a high-level programming language originally developed by Sun Microsystems and released in 1995.

* Object Oriented − In Java, everything is an Object. Java can be easily extended since it is based on the Object model.

* Platform Independent − Unlike many other programming languages including C and C++, when Java is compiled, it is not compiled into platform specific machine, rather into platform independent byte code. This byte code is distributed over the web and interpreted by the Virtual Machine (JVM) on whichever platform it is being run on.

* Simple − Java is designed to be easy to learn. If you understand the basic concept of OOP Java, it would be easy to master.

* Secure − With Java's secure feature it enables to develop virus-free, tamper-free systems. Authentication techniques are based on public-key encryption.

* Architecture-neutral − Java compiler generates an architecture-neutral object file format, which makes the compiled code executable on many processors, with the presence of Java runtime system.

* Portable − Being architecture-neutral and having no implementation dependent aspects of the specification makes Java portable. Compiler in Java is written in ANSI C with a clean portability boundary, which is a POSIX subset.

* Robust − Java makes an effort to eliminate error prone situations by emphasizing mainly on compile time error checking and runtime checking.

### Java Syntax  

To start writing Python, open up a file with the `.java` file extension.  

Before running a Java program, you must run it through the included compiler by running the command `javac example.java`.  This will compile your code.  If there are no errors in the code, the command prompt will take you to the next line, where you can run the program with `java example`.  If there **are** errors, they will be displayed when you compile the code.

#### Variables

In Java, there are different types of variables, for example:

* `String` - stores text, such as "Hello". String values are surrounded by double quotes  
* `int` - stores integers (whole numbers), without decimals, such as 123 or -123  
* `float` - stores floating point numbers, with decimals, such as 19.99 or -19.99  
* `char` - stores single characters, such as 'a' or 'B'. Char values are surrounded by single quotes  
* `boolean` - stores values with two states: true or false   

Examples:
```java linenums="1"
int myNum = 5;
float myFloatNum = 5.99f;
char myLetter = 'D';
boolean myBool = true;
String myText = "Hello";
```

#### Conditionals 

Java has the following conditional statements:

* Use `if` to specify a block of code to be executed, if a specified condition is true  
* Use `else` to specify a block of code to be executed, if the same condition is false  
* Use `else if` to specify a new condition to test, if the first condition is false  
* Use `switch` to specify many alternative blocks of code to be executed  

**Loops** 

Two varieties: while and for 

The while loop loops through a block of code as long as a specified condition is true:

```java linenums="1"
int i = 0;
while (i < 5) {
  System.out.println(i);
  i++;
}
```
When you know exactly how many times you want to loop through a block of code, use the for loop instead of a while loop:

```java linenums="1" 
for (int i = 0; i < 5; i++) {
  System.out.println(i);
}
```  

#### Methods (functions)

A method is a block of code which only runs when it is called.

You can pass data, known as parameters, into a method.

Methods are used to perform certain actions, and they are also known as functions.

Why use methods? To reuse code: define the code once, and use it many times.

```java linenums="1"
public class Main {
  static void myMethod() {
    System.out.println("I just got executed!");
  }

  public static void main(String[] args) {
    myMethod();
  }
}

// Outputs "I just got executed!"
```  

#### Classes/Objects  

Java is an object-oriented programming language.

Everything in Java is associated with classes and objects, along with its attributes and methods. For example: in real life, a car is an object. The car has attributes, such as weight and color, and methods, such as drive and brake.

A Class is like an object constructor, or a "blueprint" for creating objects. 

To create a class, use the keyword `class`:

```java linenums="1"
public class Main {
  int x = 5;
}
```  

In Java, an object is created from a class. We have already created the class named MyClass, so now we can use this to create objects.

To create an object of MyClass, specify the class name, followed by the object name, and use the keyword new:

```java linenums="1"
public class Main {
  int x = 5;

  public static void main(String[] args) {
    Main myObj = new Main();
    System.out.println(myObj.x);
  }
}
```

## First Program  
Simple "Hello World" program:

```java linenums="1"
public class HelloWorld {
  public static void main(String[] args) {
    System.out.println("Hello World");
  }
}
```  

