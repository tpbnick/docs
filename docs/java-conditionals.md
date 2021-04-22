# Conditionals/Control Flow
Imagine we're writing a program that enrolls students in courses.  

- ***If*** a student has completed the prerequisites, ***then*** they can enroll in a course.  

- ***Else***, they need to take the prerequisite courses.  

For example, a student cannot take Physics II without first completing Physics I.  

We represent this kind of decision-making in our program using *conditional* or *control flow* statements.  Before this point, our code runs line-by-line from the top down, but conditional statements allow us to be selective in which portions will run.  

Conditional statements check a `#!java boolean` condition and run a *block* of code depending on the condition.  Curly braces mark the scope of a conditional block similar to a method or class.  

Here's a complete conditional statement:
```java linenums="1"
if (true) {
    System.out.println("Hellow World!");
}
```
If the condition is `#!java true`, then the block is run, which results in `Hello World!` being printed.  

But suppose the condition is different:
```java linenums="1"
if (false) {
    System.out.println("Hello World!");
}
```
If the condition is `#!java false`, then the block does not run.  

This code is also called *if-then* statements: "If `(condition)` is `#!java true`, then do something".  

## If-Then Statement
The *if-then* statement is the most simple control flow we can write.  It tests an expression for truth and executes some code based on it.  

```java linenums="1"
if (flip == 1) {
    System.out.println("Heads!");
}
```  

- the `#!java if` keyword marks the beginning of the conditional statement, followed by parentheses `()`.  

- The parentheses hold a `#!java boolean` datatype.  

For the condition in parentheses we can also use variables that reference a boolean, or comparisons that evaluate to a boolean.  

The boolean condition is followed by opening and closing curly braces that mark a block of code.  This block runs if, and only if, the boolean is `#!java true`.  

```java linenums="1"
boolean isValidPassword = true;

if (isValidPassword) {

    System.out.println("Password Accepted!");
}

// prints "Password accepted!"

int numberOfItemsInCart = 9;

if (numberOfItemsInCart > 12) {
    System.out.println("Express checkout not available");
} 

// nothing is printed
```
If a conditional is brief we can omit the curly braces entirely:
```java linenums="1"
if (true) System.out.println("Brevity is the soul of wit");
```

## If-Then-Else
We've seem how to conditionally execute one block of code, but what if there are two possible blocks of code we'd like to execute?  

Let's say *if* a student has the required prerequisite, *then* they enroll in the selected course, *else* they're enrolled in the prerequisite course instead.  

We create an alternate conditional branch with the `#!java else` keyword:  
```java linenums="1"
if (hasPrerequisite) {
    // enroll in course
} else {
    // enroll in prerequisite
}
```
This conditional statement ensures that exactly one code block will be run.  If the condition `#!java hasPrerequisite`, is `#!java false`, the block after `#!java else` runs.  

There are now two separate code blocks in our conditional statement.  The first block runs if the condition evaluates to `#!java true`, the second block runs if the condition evaluates to `#!java false`.  

This code is also called an *if-then-else* statement:  

- If *condition* is true, then do something.  

- Else, do a different thing.  

## If-Then-Else-If
The conditional structure we've learned can be chained together to check as many conditions as are required by our program.  

Imagine our program is now selecting the appropriate course for a student.  We'll check their submission to find the correct course enrollment.  

The conditional statement now has multiple conditions that are evaluated from the top down:

```java linenums="1"
String course = "Theatre";

if (course.equals("Biology")) {
    // enroll in Biology course
} else if (course.equals("Algebra")) {
    // enroll in Algebra course
} else if (course.equals("Theatre")) {
    // enroll in Theatre course
} else {
    System.out.println("Course not found!");
}
``` 
**The first** condition to evaluate to `#!java true` will have that code block run.  Here's an example demonstrating the order:
```java linenums="1"
int testScore = 72;

if (testScore >= 90){
    System.out.println("A");
} else if (testScore >= 80) {
    System.out.println("B");
} else if (testScore >= 70) {
    System.out.println("C");
} else if (testScore >= 60) {
    System.out.println("D");
} else {
    System.out.println("F");
}
```
This chained conditional statement has two conditions that evaluate to `#!java true`.  Because `#!java testScore >= 70` comes before `#!java testScore >= 60`, only the earlier code block is run.  

**Note:** Only one of the code blocks will run.  

