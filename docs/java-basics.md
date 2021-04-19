# Java Basics

## Hello World
Java runs on different platforms, but programmers write it the same way.  Let's explore some rules for writing Java.

On the [First Program](https://docs.nicklyss.com/java/#first-program) section on the Java Basics page, we saw the **HelloWorld.java** file.  Java files have a **.java** extension.  Some programs are one file, others have hundreds of files!  

Inside **HelloWorld.java** we have a *class*:

```java linenums="1"
public class HelloWorld{

} 
```
We will talk about classes more in the future, but for now think of them as a **single** concept.  

The `HelloWorld` concept is: Hello World Printer.  Other class concepts could be: Bicycle, or: Savings Account.  

We marked the domain of this concept using curly braces: `{}`.  Syntax inside the curly braces is part of the class.  

Each file has one primary class named after the file.  Our class name: `HelloWorld` and our filename: **HelloWorld**.  Every word is capitalized.  

Inside the class we made a `#!java main()` *method* which lists our program tasks:

```java linenums="1"
public static void main(String[] args) {

}
```
Like classes, we used curly braces to mark the beginning and end of a method.  

`#!java public`, `#!java static`, and `#!java void` are syntax we will learn about on future pages.  `#!java String[] args` is a placeholder for information we want to pass into our program.  This syntax is necessary for the program to run but more advanced than we need to explain at the moment.  

Our program also displayed the text `"Hello World"` on the screen.  This was accomplished using a print statement:

```java linenums="1"
System.out.println("Hello World");
```

## Print Statements

Let's take a closer look at the print statement from above:

```java linenums="1"
System.out.println("Hello World");
```
Print statements output information to the screen (also referred to as the output terminal).  Let's break this line of code down a little more.  Don't worry if some of the terms here are new to you.

- `System` is a built-in Java class that contains useful tools for our programs.

- `out` is short for "output".  

- `println` is short for "print line".  

We can use `#!java System.out.println()` whenever we want the program to create a new line on the screen after outputting a value:  

```java linenums="1"
System.out.println("Hello World");
System.out.println("Today is a great day to code!");
```  

After `"Hello World"` is printed, the output terminal creates a new line for the next statement to be outputted.  This program will print each statement on a new line like so:
```
Hello World
Today is a great day to code!
```  

We also can output information using `#!java System.out.print()`.  Notice the we're using `#!java print()`, not `#!java println()`.  Unlike `#!java System.out.println()`, this type of print statement outputs everything on the same line.  For example:
```java linenums="1"
System.out.print("Hello ");
System.out.print("World");
```  
The above code will have the following output:
```
Hello World
```  
In this example, if we were to use `#!java print()` or `#!java println()` again, the new text will print immediately after `World` on the same line.  It's important to remember where you left your program's "cursor".  If we use `#!java println()` the cursor is moved to the next line.  If we use `#!java print()` the cursor stays on the same line.  

## Commenting Code

Writing code is an exciting process of instructing the computer to complete tasks.  Code is also read by people, and we want our intentions to be clear to humans just like we want our instructions to be clear to the computer.  

Fortunately, we are not limited to writing syntax to perform a task.  We can also write *comments*, notes to human readers of our code.  These commments are not executed, so there's no need for valid syntax within a comment.  

When comments are short we use the single-line syntax: `//`.

```java linenums="1"
// The following code does X
```
When comments are long we use the multi-line syntax: `/*` and `*/`.  

```java linenums="1"
/*
The following code does X
Expected input is the following: X and Y
*/
```
Another type of commenting option is the Javadoc comment which is represented by `/**` and `*/`.  Javadoc comments are used to create documentation for [APIs](https://docs.nicklyss.com/api).  When writing Javadoc comments, remember that they will eventually be used in the documentation that your users might read, so make sure to be especially thoughtful when writing these comments.  

Javadoc comments are typically written before the declaration of fields, methods, and classes:

```java linenums="1"
/**
* The following class accomplishes the following task...
*/
```
Here's how a comment would look in a complete program:
```java linenums="1"
/**
* The following class shows what a comment would look like in a program.
*/
public class CommentExample {
  // I'm a comment inside the class
  public static void main(String[] args) {
    // I'm a comment inside a method
    System.out.println("This program has comments!");
  }
}
```
Comments are different from printing to the screen, when we use `#!java System.out.println()`.  These comments **won't** show up in our terminal, they're only for people who read our code in the text editor.  

## Semicolons and Whitespace

As we saw with the comments above, reading code is just as important as writing code.  We should write code that is easy for other people to read.  Those people can be co-workers, or even yourself!  

Java does not interpret *whitespace*, the areas of the code without syntax, but humans can use whitespace to read code more effeciently and with less difficulty.  

Functionally, these two code samples are identical:

```java linenums="1"
System.out.println("Java");System.out.println("Lava");System.out.println("Guava");
```

```java linenums="1"
System.out.println("Java");
 
System.out.println("Lava");
 
System.out.println("Guava");
```
These will both print the same text to the screen, but which would humans prefer to read?  Imagine if there were hundreds of lines of code!  Whitespace would be essential.  

Java **does** interpret semicolons.  Semicolons are used to markt the end of a *statement*, one line of code that performs a single task.  

The only statements we've seen so far are `#!java System.out.println("My message!");`.  

Let's contrast statements with the curly brace, `{}`.  Curly braces mark the scope of our classes and methods.  There are no semicolons at the end of a curly brace.  

## Compiling & Catching Errors

Java is a *compiled* programming language, meaning the code we write in a **.java** file is transformed into *byte code* by a compiler before it is executed by the Java Virtual Machine on your computer.  

A compiler is a program that translates "human-friendly" programming languages into other programming languages (machine code) that computers can execute.  

![!Java Compiler Process](https://nicklyss.com/media/uploads/2021/04/javacompiler.png)  

The compiling process catches mistakes **before** the computer runs our code.  

The Java compiler runs a series of checks while it transforms our code.  Code that does not pass these checks will not be compiled.  For example, with a file called **Example.java**, we would compile it with the terminal command:

```
javac Example.java
```
A successful compilation produces a **.class** file: **Example.class**, that we execute with the terminal command:
```
java Example
```
An unsuccessful compilation produces a list of errors, which are helpful for fixing the program.  No **.class** file is made until the errors are corrected and the compile command is run again.  


