# Debugging
When we are writing Java programs, the compiler is our first line of defense against errors.  It can catch syntax errors.  

*Syntax errors* represent grammar errors in the use of the programming language.  They are the easiest to find and correct.  The compiler will tell you where it got into trouble, and its best guess as to what you did wrong.  

Some common syntax errors are:  

- Misspelled variable and method names  

- Omitting semicolons `;`  

- Omitting closing parenthesis `)`, square bracket `]`, or curly brace `}`  

Here is an example of a syntax error message:
```
Debug.java:5: error: ';' expected
  int year = 2021
                  ^
1 error
```
Usually the error is on the exact line indicated by the compiler, or the line just before it; however, if the problem is incorrectly nested braces, the actual error may be at the beginning of the nested block.  

## Run-time Errors
If our program has no compile-time errors, it will run.  This is where the "fun" really starts.  

Errors which happen during program execution (run-time) after successful compilation are called run-time errors.  *Run-time* errors occur when a program with no compile-time errors asks the computer to do something that the coputer is unable to reliably do.  

Some common run-time errors:

- Division by zero also known as a division error   

- Trying to open a file that doesn't exist  

There is no way for the compiler to know about these kinds of errors when the program is compiled.  

Here is an example of a run-time error message:
```
Exception in thread "main"
java.lang.ArithmeticException: / by zero
        at Debug.main(Debug.java:8)
```
## Exceptions
Java uses *exceptions* to handle errors and other exceptional events.  Exceptions are the conditions that occur at runtime and may cause the termination of the program.  

When an exceptions occurs, Java displays a message that includes thame of the exception, the line of the program where the exception occurred, and a *stack trace*.  The stack trace includes:

- The method that was running  

- The method that invoked it  

- The method that invoked that one  

- and so on...  

Make sure to examine each method involved in the exception.  

Some common exceptions are:  

- `ArithmeticException`: Something went wrong during an arithmetic operation; for example, division by zero.  

- `NullPointerException`: You tried to access an instance variable or invoke a method on an object that is currently `null`.  

- `ArrayIndexOutOfBoundsException`: The index you are using is either negative or greater than the last index of the array (i.e., `array.length-1`).  

- `FileNotFoundException`: Java didn’t find the file it was looking for.  

## Exception Handling
Exception handling is an essential feature of Java programming that allows us to use run-time error exceptions to make our debugging process a little easier.  

One way to handle exceptions is using the `#!java try`/`#!java catch`:  

- The `#!java try` statement allows you to define a block of code to be tested for errors while it is being executed.  

- The `#!java catch` statement allows you to define a block of code to be executed if an error occurs in the try block.  

The `#!java try` and `#!java catch` keywords come in pairs, though you can also catch several types of exceptions in a single block:
```java linenums="1"
try {
    // block of code to try
} catch (NullPointerException e) {
    // print error message like this:
    System.err.println("NullPointerException: " + e.getMessage());
    // or handle the error another way here
}
```
Notice how we used `#!java System.err.println()` here instead of `#!java System.out.println()`.  `#!java System.err.println()` will print out the standard error and the text will be in red.  

You can also chain exceptions together:
```java linenums="1"
try {
    // block of code to try
} catch (NullPointerException e){
    // code to handle a NullPointerException
} catch (ArithmeticException e){
    // code to handle an ArithmeticException
}
```

## Logic Errors
Sometimes programs still do not do what we want them to do or no output is produced.  These types of errors which provide incorrect output, but appears to be error-free, are called *logic errors*. Logic errors occur when there is a design flaw in your program. These are some of the most common errors that happen to beginners and also usually the most difficult to find and eliminate.

Because logical errors solely depend on the logical thinking of the programmer, your job now is to figure out why the program didn’t do what you wanted it to do.

Some common logic errors:

- Program logic is flawed  

- Some “silly” mistake in an `if` statement or a `for`/`while` loop  

## Debugging Techniques
If you have examined the code thoroughly, and you are sure the compiler is compiling the right source file, it is time for desperate measures:

1. Divide and conquer: Comment out or temporarily delete half the code to isolate an issue.  

If the program compiles now, you know the error is in the code you deleted. Bring back about half of what you removed and repeat.
If the program still doesn’t compile, the error must be in the code that remains. Delete about half of the remaining code and repeat.
Tip: In most code editors, one can highlight a block of code and use the keyboard shortcut ctrl + / to comment it out.

2. Print statements for the rescue: Use `#!java System.out.println()` to check variable/return values at various points throughout the program.  

A lot of the time with logic errors, there was a flawed piece of logic, a miscalculation, a missing step, etc. By printing out the values at different stages of the execution flow, you can then hopefully pinpoint where you made a mistake.
